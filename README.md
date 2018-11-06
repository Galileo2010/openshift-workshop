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

Continue next step only when builder image is created successfully. You can check from web console.   

#### Build service with S2I builder image
Create Zipkin server from zipkin-server/build-deployment-config.yaml. 
    
There are two ways. Either to create via ```oc```,
```console
oc new-app -f openshift/zipkin-server/build-deployment-config.yaml \
    -p PROJECT_NAME=workshop \ 
    -p APP_NAME=zipkin-server \
    -p GIT_SOURCE_URL=https://github.com/platform-guild/openshift-workshop.git \
    -p GIT_SOURCE_REF=master \
    -p APP_PORT=9000 \
    -p APP_ENV=dev
```
> ```new-app``` usually 

or to create via the web console as below,   
![Console way](images/console-template-to-create.png)
#### 
```console
oc get buildconfig

oc start-build zipkin-server
```
#### Access service
```console
oc expose service zipkin-server --hostname=workshop.apps.tlk.im --port=9000 -l app=zipkin-server
```

### Deploy service with CI/CD pipeline
#### Create service from template
```console
oc create -f openshift/service/template.yaml
```

#### Auto triggering
* Define your ```Secret``` before actually doing it.
    ```console
    oc create -f openshift/github-webhook-secret.yaml
    ```
* Update ```BuildConfig``` to allow auto build triggering when there is new change is checked in codebase,
    ```yaml
    triggers: 
        - type: "GitHub"
          github:
            secret: "sti-builder-secret"
    ```


### Best practices
#### Use of Labels
```console
oc delete all --selector="app=zipkin-server"
```
#### Template on OpenShift
```console
oc process -f openshift/service/template.yaml
```
> This is to

```console
oc process --parameters -f openshift/service/template.yaml
```
> This is to 

```console
oc process -f zipkin-server-template.yaml | oc create -f -
```
> To create objects by giving pre-defined template

```console
oc create -f openshift/service/template.yaml
```
> To upload template 

## Workshop -- part 2

### Scale up & down

### Rollback

### Service registration & discovery

### Logging & Monitoring

Go to [HOWTO.md](HOWTO.md) for how to configure and build the projects.