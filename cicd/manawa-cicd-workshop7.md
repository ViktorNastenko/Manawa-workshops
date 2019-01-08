Edit your `.gitlab-ci.yml` file and replace its content by the code bellow:


    variables:
      APP_VERSION: 0.0.1
      JFROG_USER: <YOUR JFROG SVC ACCOUNT>
      JFROG_REPO: <YOUR JFROG REPOSITORY>
      BUILD_IMAGE: <YOUR JFROG REPOSITORY>/hello-world
      MANAWA_USER: <YOUR MANAWA SVC USER>
      MANAWA_PROJECT: <YOUR MANAWA PROJECT>
      MANAWA_URL: https://manawa.euw1-gcp-poc.adeo.cloud/
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
        - docker push ${BUILD_IMAGE}:${APP_VERSION}
      tags:
        - adeo
        - docker
        - images
     


Once you copied and modified the variables in your gitlab-ci config file you can push the code to your Github repository and verify your Gitlab pipeline is working.

```
$ git add --all
```

```
$ git commit -m "adding build stage in gitlab pipeline"
```

```
$ git push origin master
```

If you go back to Gitlab inside your repository. You shoud have something similar to the following screenshot when clicking on CI / CD --> Pipelines in the left menu.

![CICD Pipeline with one step]({% image_path 
screens/pipeline-with-one-step.png %})
