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

### Basic check before we get started
```console
oc login https://oc.tlk.im:443 --token=#TOKEN#
```

```console
oc status
```

```console
oc project workshop
```

### Deploy first application on OpenShift

#### S2I builder image

Follow [README.md](https://github.com/platform-guild/platform-s2i-springboot) to import S2I builder image into the online catalog.   

#### Build service with S2I builder image
Create Zipkin server from zipkin-server/template.yaml. 
    
There are two ways. Either to create via ```oc```,
```console
oc create -f openshift/zipkin-server/template.yaml \
    -p PROJECT_NAME=workshop \ 
    -p APP_NAME=zipkin-server \
    -p GIT_SOURCE_URL=https://github.com/platform-guild/openshift-workshop.git \
    -p GIT_SOURCE_REF=master \
    -p APP_PORT=9000 \
    -p APP_ENV=dev
```
or to create via the web console as below,   
![Console way](images/console-template-to-create.png)

#### Build Pipeline

```console
oc create 
```
> this is

#### Reach service out 
```console
oc expose service
```

```console

```
#### Auto triggering
- Define your ```Secret``` before actually doing it.
    ```console
    oc create -f openshift/github-webhook-secret.yaml
    ```
- Update ```BuildConfig``` to allow auto build triggering when there is new change is checked in codebase,
    ```yaml
    triggers: 
        - type: "GitHub"
          github:
            secret: "sti-builder-secret"
    ```


### Template on OpenShift
```console
oc create -f zipkin-server-template.yaml
```
```console
oc process zipkin-server-template.yaml | oc create -f -
```

### Best practices
#### Use of Labels
```console
oc delete -all --selector="app=zipkin-server"
```

## Workshop -- part 2

### Scale up & down

### Rollback

### Logging & Monitoring

Go to [HOWTO.md](HOWTO.md) for how to configure and build the projects.