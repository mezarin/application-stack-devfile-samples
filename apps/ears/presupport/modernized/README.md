# Devfile For Ear applications.
The devfiles provided show two ways of deploying an EAR packaged application.

**Notes**: 
- The sample devfiles are pre Open Liberty Maven Plugin support for multi module applications.
- The samples follow the director naming convention where the directory that constructs the ear file should be suffixed with **-ear** (i.e. application-ear). Any variations from this convention will require devfile udpates (customization of ear directory names where used). The provided sample devfiles also allow the ear directory to be named just 'ear'.

## Sample Devfiles

- **devfile-devMode.yaml** builds and uses devmode to dynamically process application updates.
- **devfile-exec-jar.yaml** packages the Liberty runtime and the application into an executable jar and runs the application using the generated jar.

## Pre-reqs

- ODO [CLI](https://odo.dev/docs/installing-odo/).
- Kubernetes Cluster (An OpenShift cluster is used for the procedure that follows)

## Procedure

1. Place one of the sample devfiles into the root of your application project.

```
cd <application project root dir>
```
```
curl -L https://raw.githubusercontent.com/mezarin/application-stack-devfile-samples/master/apps/ears/presupport/modernized/devfile-devMode.yaml -o devfile.yaml

or 

curl -L https://raw.githubusercontent.com/mezarin/application-stack-devfile-samples/master/apps/ears/presupport/modernized/devfile-exec-jar.yaml -o devfile.yaml
```

2. Create an application component using the chosen devfile.

```
odo create myearapp
```

3. Deploy the application.

```
odo push
```

4. Retrieve the URL to access th eapplication externally.

```
odo url list
```

Example output:
```
Found the following URLs for component myearapp
NAME     STATE      URL                                                      PORT     SECURE     KIND
ep1      Pushed     http://ep1-myearapp-gradle.apps.xxxxxxx.cp.fyre.ibm.com     9080     false      route

```

5. Access the application using the URL obtained on the previous step.

```
http://ep1-myearapp-gradle.apps.xxxxxxx.cp.fyre.ibm.com/hitcount
```
```
http://ep1-myearapp-gradle.apps.xxxxxxx.cp.fyre.ibm.com/snoop (See server.xml for authentication information)
```

## Sample Application
The included application is a modernized version of the Traditional WebSphere DefaultApplication.ear

### Source
[Modernized DefaultApplication.ear](https://github.com/WASdev/sample.DefaultApplication/tree/master/modernized)

#### What Changed
- The use of net.wasdev.wlp.maven.parent:liberty-maven-app-parent from parent pom was removed.
- Pom dependency versions were updated.