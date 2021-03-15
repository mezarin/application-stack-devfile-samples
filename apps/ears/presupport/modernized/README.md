# Devfile For Ear applications.
The devfiles provided show two ways of deploying an EAR packaged application.

**Note**: 
- The sample devfiles are pre Open Liberty Maven Plugin support for multi module applications.
- The samples follow the convention that the directory that constructs the ear file should be suffixed with **-ear** (i.e. application-ear). Any variations from this convention will require devfile udpates. The sample devfiles that are provided are more linient in that it will allow for directories that just end in **\*ear** to accomodate those that are named just 'ear'.

## Sample Devfiles

- **devfile-devMode.yaml** builds and uses devmode to dynamically process application updates.
- **devfile-exec-jar.yaml** packages the Liberty runtimem and the application into an executable jar and runs the application using the generated jar.

## Procedure

1. Rename and place the devifile of your choice into the root of your project

```
cd <application project root dir>
```
```
cp .../devfile-<choose-one>.yaml devfile.yaml
```

2. ***Optional:*** if the directory building the ear file does not end in ***ear***, open the devfile and replace the following:
- Replace ***\*ear*** entries with the name of the directory in your project that builds the ear file.

3. Create an application component using the chosen devfile.

```
odo create myearapp
```

4. Deploy the application.

```
odo push
```

## Sample app
Modernized Traditional WebSphere DefaultApplication.ear

### Source
The [modernized](https://github.com/WASdev/sample.DefaultApplication/tree/master/modernized) version of application in this repository: https://github.com/WASdev/sample.DefaultApplication

#### What Changed
- Removed the use of net.wasdev.wlp.maven.parent:liberty-maven-app-parent from parent pom.
- Modified pom dependency versions.