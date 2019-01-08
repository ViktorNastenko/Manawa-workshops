Edit your `.gitlab-ci.yml` file. Copy and paste the section `openshift-deploy:`


    variables:
      APP_VERSION: 0.0.1
      JFROG_USER: <YOUR JFROG SVC ACCOUNT>
      JFROG_REPO: <YOUR JFROG REPOSITORY>
      BUILD_IMAGE: <YOUR JFROG REPOSITORY>/hello-world
      MANAWA_USER: <YOUR MANAWA SVC USER>
      MANAWA_PROJECT: <YOUR MANAWA PROJECT>
      MANAWA_URL: https://manawa.euw3-gcp1.adeo.cloud/
      APP_RELEASE_NAME: flask-hello-world
      VAULT_NAMESPACE: <YOUR VAULT NAMESPACE>
      VAULT_ADDR: https://vault.factory.adeo.cloud
     
    stages:
      - build
      - deploy
     
    build:
      stage: build
      image: docker
      before_script:
        - echo "${VAULT_PAYLOAD}" > payload.json
        - apk add jq
        - apk add curl
        - VAULT_TOKEN=$(curl -s -k -X POST -H "X-Vault-Namespace:${VAULT_NAMESPACE}" --data @payload.json ${VAULT_ADDR}/v1/auth/approle/login|jq -r '.auth.client_token')
        - JFROG_TOKEN=$(curl -s -k -H "X-Vault-Token:${VAULT_TOKEN}" -H "X-Vault-Namespace:${VAULT_NAMESPACE}" -X GET ${VAULT_ADDR}/v1/secret/data/workshop/jfrog/token | jq -r '.data.data.JFROG_TOKEN')
        - docker info
        - docker login -u ${JFROG_USER} -p ${JFROG_TOKEN} ${JFROG_REPO}
      script:
        - docker build -t ${BUILD_IMAGE} .
        - docker tag ${BUILD_IMAGE} ${BUILD_IMAGE}:${APP_VERSION}
        - docker tag ${BUILD_IMAGE} ${BUILD_IMAGE}:latest
        - docker push ${BUILD_IMAGE}:${APP_VERSION}
        - docker push ${BUILD_IMAGE}:latest
        - docker rmi ${BUILD_IMAGE}:latest ${BUILD_IMAGE}:${APP_VERSION}
      tags:
        - adeo
        - docker
        - images
     
    openshift-deploy:
      stage: deploy
      image: centos
      before_script:
        - echo "${VAULT_PAYLOAD}" > payload.json
        - yum install -y epel-release
        - yum install -y jq
        - VAULT_TOKEN=$(curl -s -k -X POST -H "X-Vault-Namespace:${VAULT_NAMESPACE}" --data @payload.json ${VAULT_ADDR}/v1/auth/approle/login|jq -r '.auth.client_token')
        - MANAWA_TOKEN=$(curl -s -k -H "X-Vault-Token:${VAULT_TOKEN}" -H "X-Vault-Namespace:${VAULT_NAMESPACE}" -X GET ${VAULT_ADDR}/v1/secret/data/workshop/manawa/token | jq -r '.data.data.MANAWA_TOKEN')
        - yum install -y centos-release-openshift-origin311
        - yum install -y origin-clients
        - yum install -y wget openssl
        - wget https://storage.googleapis.com/kubernetes-helm/helm-v2.11.0-linux-amd64.tar.gz
        - tar -zxvf helm-v2.11.0-linux-amd64.tar.gz
        - mv linux-amd64/helm /usr/local/bin/helm
        - mv ./helm/app-name ./helm/${APP_RELEASE_NAME}
        - sed -i "s/app-name/${APP_RELEASE_NAME}/" ./helm/${APP_RELEASE_NAME}/values.yaml
        - sed -i "s/app-name/${APP_RELEASE_NAME}/" ./helm/${APP_RELEASE_NAME}/Chart.yaml
        - sed -i "s/MANAWA_USER/$MANAWA_USER/" ./helm/${APP_RELEASE_NAME}/values.yaml
        - sed -i "s/IMAGE_TAG/$APP_VERSION/" ./helm/${APP_RELEASE_NAME}/values.yaml
      script:
        - oc login --insecure-skip-tls-verify "$MANAWA_URL" --token="$MANAWA_TOKEN"
        - oc project $MANAWA_PROJECT
        - export TILLER_NAMESPACE=$MANAWA_PROJECT
        - helm init --client-only --service-account $MANAWA_USER
        - helm dependency update helm/${APP_RELEASE_NAME}
        - export DEPLOYS=$(helm ls | grep $APP_RELEASE_NAME | wc -l)
        - if [ ${DEPLOYS} -eq 0 ]; then helm install --name=${APP_RELEASE_NAME} helm/${APP_RELEASE_NAME}; else helm upgrade ${APP_RELEASE_NAME} helm/${APP_RELEASE_NAME}; fi
      tags:
        - adeo
        - docker
        - images


Once this is done your code to your repository

```
git add --all
```

```
git commit -m "adding deployment stage in gitlab pipeline"
```

```
git push origin master
```