

You will need the oc cli (Openshift Command Line Interface) installed on your laptop to initialize your Openshift project.

  

# Install oc binary

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
  

# Setup your CICD pipeline

**Clone Github repository**

```
    $ git clone https://github.com/adeo/software-factory-demo.git
```

**Create your own Github repository**

```
$ cd software-factory-demo
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

TODO

**Push the demo app code on your own repository**

TODO


# Artifactory (Docker registry + other features)

## Personal account 

The Software Factory currently handles the creation of Artifactory accounts.

Got to the [Software Factory Slack channel](https://adeo-tech-community.slack.com/messages/CCKQPKA6Q)
Ask for an Artifactory account
We will handle the rest for you 

## Service account

Get your team's Artifactory service account credentials.
Ask your team's admin. If you have asked your teammates and still don't know who it is, you can ask us on the [Software Factory Slack channel](https://adeo-tech-community.slack.com/messages/CCKQPKA6Q) who the admin is.


You're done for this step.