# training-s2i-java
This is training guide for deploying java application to Openshift using s2i (source to image) method.

## Building and Deploying Java Application on Openshift

1. From Git source code
2. From Local source code
3. From Binary artifact
4. From Registry

### Prerequisite
 1. Download oc tools (windows)
    * https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-windows.zip
    Maven installation on local machine
 2. Login to Openshift via Console
    * ``` oc login $OCP_MASTER_URL```
 3. Create new project (if needed)
    * ``` oc new-project $PROJECT_NAME```
 4. Choose project
	  * ``` oc project $PROJECT_NAME```

### Deploy Java Apps from GitHub

 1. Create new java apps
    *  ```oc new-app openshift/java:8~$GIT_URL```
    
    Example: 
    *  ```oc new-app openshift/java:8~https://github.com/erfinfeluzy/training-rest-notif-jms```
    
    **Note:**
      * use java:8 on openshift image stream

 2. Expose service to Route
    * ``` oc expose svc/$SERVICE_NAME ```
    
    Example:
    * ``` oc expose svc/training-rest-notif-jms ```

### Deploy Java Apps from Binary

 1. Create build config & set base image

    * ``` oc new-build --name=$APP_NAME openshift/java:8 --binary=true ```

 2. Upload jar
    * ``` oc start-build $APP_NAME --from-file="$BINARY_FILE " --follow ```

 3. Create new application

    * ``` oc new-app $APP_NAME ```

 4. Expose service to Route
    * ``` oc expose svc/$SERVICE_NAME ```
    
    Example:
    * ``` oc expose svc/training-rest-notif-jms ```



