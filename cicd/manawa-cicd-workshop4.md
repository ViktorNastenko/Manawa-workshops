GitLab offers a [continuous integration](https://about.gitlab.com/gitlab-ci/) service. You can configure a [Gitlab CI](https://docs.gitlab.com/ee/ci/pipelines.html) pipeline using a [.gitlab-ci.yml](https://docs.gitlab.com/ee/ci/yaml/README.html) file placed at the root of your repository. Gitlab will then read this file on every push and execute on every step defined in it.

In the following example, we will build a docker image and then push the resulting build (called an artifact) it to Artifactory. 


-----------

    variables:
      # Prepare variables
      # These can be hard coded as they are accessible by anyone anyway
      APP_VERSION: 0.0.1
      JFROG_USER: <YOUR JFROG SVC ACCOUNT> # e.g svc-adeo-software-factory
      JFROG_REPO: <YOUR JFROG REPOSITORY> # e.g adeo-docker-adeo-software-factory-dev.jfrog.io
      BUILD_IMAGE: <YOUR JFROG REPOSITORY>/hello-world
 

    #Set up build process using stages
    stages:
      - build


    build:
      stage: build
      before_script:
        - docker info
        - docker login -u ${JFROG_USER} -p ${JFROG_TOKEN} ${JFROG_REPO}
      script:
        - docker build -t ${BUILD_IMAGE} .
        - docker tag ${BUILD_IMAGE} ${BUILD_IMAGE}:${APP_VERSION}
        - docker tag ${BUILD_IMAGE} ${BUILD_IMAGE}:latest
        - docker push ${BUILD_IMAGE}:${APP_VERSION}
        - docker push ${BUILD_IMAGE}:latest
        - docker rmi ${BUILD_IMAGE}:latest ${BUILD_IMAGE}:${APP_VERSION}
      # Select the Runners allowed to run this project using tags
      tags:
        - adeo
        - docker
        - images

-----------

And remember, [Gitlab CI can do a ton more](https://docs.gitlab.com/ee/ci/yaml/README.html)
