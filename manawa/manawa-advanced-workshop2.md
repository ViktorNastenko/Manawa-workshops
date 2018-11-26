## Prerequisite :

You will need the oc cli (Openshift Command Line Interface) installed on your laptop to initialize your Openshift project.

You can find the instructions to install it bellow.
* For Windows: https://blog.openshift.com/installing-oc-tools-windows/
* For OS X:
  * Option 1:

  If you have Homebrew (https://brew.sh/) installed:

  Open a new terminal and enter this command:
  `brew install openshift-cli`
  * Option 2:

  Open a new terminal and enter the following commands.
  ```
  wget https://github.com/openshift/origin/releases/download/v3.10.0-rc.0/openshift-origin-client-tools-v3.10.0-rc.0-c20e215-mac.zip

  unzip -a openshift-origin-client-tools-v3.10.0-rc.0-c20e215-mac.zip

  mv ./oc /usr/local/bin/
  ```


* For Linux:
```
wget https://github.com/openshift/origin/releases/download/v3.10.0-rc.0/openshift-origin-client-tools-v3.10.0-rc.0-c20e215-linux-64bit.tar.gz

tar -xvzf openshift-origin-client-tools-v3.10.0-rc.0-c20e215-linux-64bit.tar.gz

mv openshift-origin-client-tools-v3.10.0-rc.0-c20e215-linux-64bit/oc /usr/local/bin
```


## Step 1 : Clone workshop-manawa-advanced from Github repo
1. git clone https://github.com/adeo/manawa-advanced-workshop.git
```
$ git clone https://github.com/adeo/manawa-advanced-workshop.git
```



