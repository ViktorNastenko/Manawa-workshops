

You will need the oc cli (Openshift Command Line Interface) installed on your laptop to initialize your Openshift project.

  

# 1. Install oc binary

You need at least oc version >= 3.10

You can find the instructions to install it bellow.

## For Windows: 
[https://blog.openshift.com/installing-oc-tools-windows/](https://blog.openshift.com/installing-oc-tools-windows/)

## For OS X:

**Option 1:**

If you have Homebrew (https://brew.sh/) installed:
Open a new terminal and enter this command

```
   $ brew install openshift-cli
```

**Option 2:**

Open a new terminal and enter the following commands.

```
   $ wget https://github.com/openshift/origin/releases/download/v3.10.0/openshift-origin-client-tools-v3.10.0-dd10d17-mac.zip
```

```
    $ unzip -a openshift-origin-client-tools-v3.10.0-dd10d17-mac.zip
```

```
    $ mv ./oc /usr/local/bin/
```
  
  

## For Linux:
```
    $ wget https://github.com/openshift/origin/releases/download/v3.10.0/openshift-origin-client-tools-v3.10.0-dd10d17-linux-64bit.tar.gz
```

```
    $ tar -xvzf openshift-origin-client-tools-v3.10.0-dd10d17-linux-64bit.tar.gz
```

```
    $ mv openshift-origin-client-tools-v3.10.0-dd10d17-linux-64bit/oc /usr/local/bin
```
  

# 2. Setup your CICD pipeline

**Create a new repository on Github**

Once it is created go in the settings of your repository and click on "Collaborators & teams". 

Add the team "workshop-manawa-cicd" with write access to your repository. The team "workshop-manawa-cicd" as the maintainer role. This role is necessary to allow Gitlab to be synced with your repository.

![Add team]({% image_path screens/github-add-team.png %})


**Clone Github repository**

This repository contains the demo app we are going to deploy during the workshop.

```
    #$ git clone https://github.com/adeo/software-factory-demo.git
    $ git clone https://github.com/adeo/manawa-workshop-cicd-demoapp.git
```

**Create your own Github repository**

Create a new repository on Github

Once it is created go in the settings of your repository and click on "Collaborators

```
#$ cd software-factory-demo
$ cd manawa-workshop-cicd-demoapp
```

```
$ rm -rf .git
```

```
$ git init
```

```
$ git remote add origin your_github_repo
```

**Create a Gitlab pipeline - sync Gitlab with Github (external repository)**

Crea

**Push the demo app code on your own repository**

TODO


# 3. Artifactory (Docker registry + other features)

## Personal account 

The Software Factory currently handles the creation of Artifactory accounts.

Got to the [Software Factory Slack channel](https://adeo-tech-community.slack.com/messages/CCKQPKA6Q)
Ask for an Artifactory account
We will handle the rest for you 

## Service account

Get your team's Artifactory service account credentials.
Ask your team's admin. If you have asked your teammates and still don't know who it is, you can ask us on the [Software Factory Slack channel](https://adeo-tech-community.slack.com/messages/CCKQPKA6Q) who the admin is.


You're done for this step.