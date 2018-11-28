# Ionoid IoT Apps Format

Ionoid IoT Platform supports simple IoT Apps that can run on any Linux and
integrated with Ionoid.

Ionoid IoT Apps take [Snapcraft](https://docs.snapcraft.io/) the universal
app store for Linux as a reference, and build on top of it.


## Chapters

### 1. Getting Started

This section provides basic view on IoT Apps and how to deploy them.


Ionoid IoT Apps are apps that are self contained with all their metadata
included.

On your IoT Devices, Apps will be installed in directory:
```
/data/apps/store/
```

For every application, a directory will be created like this:
```
/data/apps/store/appname
```


### 2. IoT Apps Format

Ionoid IoT Apps format is really simple it contains some metadata that
defines the application and how it is run. Apps are tarball files in
format of `.tar` or any other format that is supported by Ionoid IoT
Platform.


As an example lets take the current hello world example that is
available here: [IoT Apps Golang Hello
World](https://console.cloud.google.com/storage/browser/public.opendevices.io/apps)

[Hellow World IoT App Example:](https://console.cloud.google.com/storage/browser/public.opendevices.io/apps)

```
* app.yaml      : App Basic information.

* meta/         : Meta directory that contains extra App metadata (Optional).

* bin/          : Binary directory where the App may reside.

* ...           : Rest of the App file system and other dependencies files.
```

If you are using another supported format, then the `app.yaml` will be
automatically created.


#### 2.1 App.yaml Format

Every App has an **app.yaml** file that contains the basic following
information:

(the `#` beginnig means this line is a comment)

```
# Name of APP must be Alphanumeric and can contain the following
# special characters "_", "." and "-".
# Minimum 2 charactes, up to 64 characters.
name: appname

# Version of App
version: 1.0

# Description of App
description: My App

# List of Applications inside the same IoT App, the final IoT
# App can include one app entry or several apps.
apps:
        hello-world:
                command:        /bin/hello-world
        hello-world-2:
                command:        /bin/hello-world-2
        bash-command:
                command:        /bin/echo "hello-world from echo"
                stop-command:   /bin/echo "hello-world stopped"


# Health check special command to do health checking on your
# one or multiple apps
health-check:
                command:        /bin/health-check
```

The `apps` may contain several entries if you want to launch several IoT
Apps together, distribute them together, or share the running
environment. However we would recommend to always have one command per
App if you do not nead multiple Apps to be grouped together.


**HEALTH CHECK NOT SUPPORTED**

The `health-check` is a special directive that may allow you to do
health checks on your running apps. Right now it is **NOT SUPPORTED**.



So if we go back to our [Hellow World IoT App Example:](https://console.cloud.google.com/storage/browser/public.opendevices.io/apps)

The content of the `app.yaml` file would be:
```
name: hello-world
version: 1.0
apps:
        hello-world:
                command:        /bin/hello-world
```


#### 2.2 Example of Hellow World APP

If you are in the root directory of your compiled APP, you can use this
example to generating a tarball:

```bash
$ cd hello-world-armv7-v0.1
$ ls ./*
./app.yaml

./bin:
hello-world

$ cat app.yaml 
name: hello-world
version: 0.1

apps:
        hello-world:
                command: /bin/hello-world

$ tar -cvf ../hello-world-armv7-v0.1.tar *
```


### 3. Building IoT Apps

If you are using the native and simple format of ionoid IoT Apps, then
you can follow the following guide, otherwise skip to the one that
targets the format that you want.


#### 3.1 Building Simple Ionoid IoT Apps

We support several platform, please follow the appropriate platform
guide.


* [Build IoT Apps on Debian/Ubuntu Linux](../apps/build/build_on_debian_linux.rst)

* [Build IoT Apps on Fedora Linux](../apps/build/build_on_fedora_linux.rst)


* [Build IoT Apps on Windows]


* [Build IoT Apps on OSX]



#### 3.2 Build Snapcraft Snaps

TODO: document.


#### 3.3 Build Docker IoT Apps

TODO: document.
