# Installing OFBiz

OFBiz (Open for Business) is a free and open source ERP solution by
Apache, flexible enough to be used across any industries and business.

In this file of this gist, we will install OFBiz, with default setup.
This use embedded Apache Derby as database backend, and loaded with
default dataset included with the distribution.

## Prerequisites
- You need to have JDK 8 (not just JRE, but full JDK) installed on your
system. Most Linux distributions should provided OpenJDK 8 package, but
you can also install
[official JDK build from Oracle](https://www.oracle.com/technetwork/java/javase/downloads/index.html).
Also, ensure that JDK binaries are on `PATH` and JDK installation
directory is set on `JAVA_HOME`, as described in *Adding JDK to Shell*

## Creating OFBiz User
Create user dedicated to running OFBiz instance, separated from other
users. This way, if this account is compromised, it can be deleted along
with OFBiz instance.

On Debian-based systems:
```
# addgroup ofbiz-operator
# adduser --ingroup ofbiz-operator ofbiz
```

On other systems:
```
# groupadd ofbiz-operator
# useradd -g ofbiz-operator ofbiz
```

In subsequent sections in this file, and on other files in this gist,
all commands are run as `ofbiz` user. Switch user first:
```
# su ofbiz
```

## Adding JDK to Shell

As in other Java applications, OFBiz requires that `JAVA_HOME` is set
to JDK directory, and JDK binaries (such as `java`) are on `PATH`.

Append to `~/.bashrc` and `~/.bash_profile`:
```shell
export JAVA_HOME=/path/to/jdk8
export PATH=$PATH:$JAVA_HOME/bin
```
## Downloading OFBiz

Use `wget` to download OFBiz, then extract it to `/opt`. Change directory
if yours different. At the time of writing, the latest version is 16.11.05.
If you come from the future, see
[Download Page](https://ofbiz.apache.org/download.html) and substitute
links and files to latest version accordingly:
```
$ wget -c https://www-eu.apache.org/dist/ofbiz/apache-ofbiz-16.11.05.zip
# unzip apache-ofbiz-16.11.05.zip -d /opt
```
Rename directory to `ofbiz`, for easier reference:
```
# mv /opt/apache-ofbiz-16.11.05 /opt/ofbiz
```

Change ownership to `ofbiz` user:
```
# chown -R ofbiz:ofbiz-operator /opt/ofbiz
```

## Building and Running OFBiz

`cd` to OFBiz directory:
```
$ cd /opt/ofbiz
```

OFBiz is distributed as source code, with `gradle` as its build system.
In order to run OFBiz, it must be compiled first. As such, `gradlew`
(`gradle` wrapper script) will be utilized for compilation. This script
is also used to start and stop OFBiz instance.

Clean all residual artifacts, build OFBiz, and load default dataset. Since
this is the first time running OFBiz, `gradlew` will download `gradle`
and all build- and runtime dependencies needed by OFBiz, so it may take
some time:
```
$ ./gradlew cleanAll loadDefault
```

If the build succeed, you can now start OFBiz instance:
```
$ ./gradlew ofbiz
```

You can also run OFBiz as background service:
```
$ ./gradlew ofbizBackground
```

Finally, to stop OFBiz after using it:
```
$ ./gradlew "ofbiz --shutdown"
```

## systemd service
Most Linux systems/distributions are now run under systemd init system.
It would be nice if OFBiz can be run automatically when system boots and
stopped when system shuts down, without needing to login to `ofbiz`
user and executing `gradlew` manually. This is where systemd service
comes in.

Create `/etc/systemd/system/ofbiz.service` with following:
```ini
# OFBiz service

[Unit]
Description=OFBiz Service

[Service]
Type=simple

# environment variables
Environment="JAVA_HOME=/path/to/jdk8"
Environment="PATH=/path/to/jdk8/bin:/bin:/sbin:/usr/bin:/usr/sbin"

User=ofbiz
WorkingDirectory=/opt/ofbiz

# start and stop executables
# note that systemd requires specifying full/absolute path to executables
ExecStart=/opt/ofbiz/gradlew ofbiz
ExecStop=/opt/ofbiz/gradlew "ofbiz --shutdown"

[Install]
WantedBy=multi-user.target
```

Reload systemd daemon, then enable and start the service:
```
# systemctl daemon-reload
# systemctl enable ofbiz.service --now
```

The log, which is displayed to stdout when running `gradlew` manually,
is now on systemd journal, which can be viewed by:
```
# journalctl -u ofbiz.service
```

## Visit OFBiz from Your Browser
Head to *Web Tools Administration* on `https://localhost:8443/webtools`.
You should see the page that instructs you to login with user `admin`
and password `ofbiz`. If not, retrace the steps above to find out the
cause of your problem and resolve it.

## Conclusion
Now you have a working OFBiz instance on your system. In the next file
in this gist, NGINX will serve OFBiz as reverse proxy. Stay tuned!