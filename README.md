# Platform Capability Building Workshop - OpenShift

## Prerequisites
* Git
* OpenShift CLI ([Downloading Source](https://github.com/openshift/origin/releases/))
  * Download  
  ```console 
  cd ~/downloads && wget https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
    ```
  * Uncompress file and add in PATH
  ```console
  mkdir ~/openshift-cli
  cd ~/downloads && tar xvf openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz -C ~/openshift-cli --strip-components 1
  ``` 
  * Add ```oc``` in PATH. You can either
  ```console
  export PATH=#USER_HOME#/openshift-cli:$PATH
  ``` 
  , or (only when permission is sufficient)
  ```console
  cp ~/openshift-cli/oc /usr/bin  
  cp ~/openshift-cli/kubectl /usr/bin
  ```


## Workshop -- part 1


```console
oc project openshift-workshop
```

```console
oc status
```
## Workshop -- part 2

```console
oc 
```

Go to [HOWTO.md](HOWTO.md) for how to configure and build the projects.