---
title: JBoss EAP Installation
workshops: eap_migration
workshop_weight: 30
layout: lab
---

## JBoss EAP Installation

The purpose of this lab is to describe the various methods of installing JBoss EAP 7 as well as to perform a sample installation.

### Installation Methods

There are several different ways to install JBoss EAP. Each method is best used in certain situations. Below is a brief overview of each type of installation, and links to the sections that cover the relevant installation processes.

- [ZIP Installation][zip]:  JBoss EAP 7 is distributed as a zip file that can be extracted and executed on an operating system with Java 8 installed. It contains all the libraries, configuration files, and scripts needed to start EAP. Out of the box, it installs a default configuration of EAP with may require post-installation customization to suit your environment/use case.
- [JAR (Graphical) Installation][jar]: The JAR installer is a graphical, Java-based installation wizard that provides you a step-by-step way of customizing your JBoss EAP steup. It requires Java 8 to be installed. It can be run using either the graphical interface (default) or a text-based console. You can also supply an XML response file pre-populated with all the options for the installation.
- [RPM Installation][rpm]: (Note: The RPM installation method is only relevant for Red Hat Enterprise Linux). JBoss EAP 7 is available asn RPM package for users with a subscription to the JBoss Enterprise Application Platform sub-channel. The RPMs can be installed using the yum command.

JBoss EAP is also available as a Docker container for deployment on [OpenShift][xpaas].

### Installing JBoss EAP

For the purposes of this workshop, we will be using the graphical installer.

#### Using the Graphical Installer
To install EAP, enter the following command:

```
$ java -jar jboss-eap-7.0.0-installer.jar
```
The following screenshot shows the EAP installer in GUI mode:

{{< figure src="../images/installer_license.jpg" title="JBoss EAP 7 GUI Installer" >}}

Please follow the wizard accordingly:

1. License Agreement: Accept the License Agreement.
2. Installation Path: Accept the default installation path of `/home/student/EAP-7.0.0` (henceforth in this workshop referred to as `JBOSS_HOME`).
3. Component Selection: Accept the defaults.
4. Create an Administrative User: Accept the default username of `admin`, for the purposes of this lab use the password `Redhat1!`.
5. Installation Overview: Review installation details.
6. Component Installation: Wait for completion.
7. Configure Runtime Environment: Accept the `Perform default configuration` option.
8. Configure Server: Wait for completion.
9. Shortcut Configuration: Accept the defaults.
10. Installation Complete!

#### Setting JBOSS_HOME

You need to set an environment variable called `JBOSS_HOME` pointing to the JBoss EAP
installation directory. It will be used by various scripts to locate where JBoss EAP is installed.

Similarly, change the `PATH` variable to run JBoss EAP scripts in the `JBOSS_HOME/bin` folder
from any directory. In order to set these variables, open `/home/student/.bashrc`
with your preferred text editor and add the following lines at the end of the file:

```
JBOSS_HOME=/opt/jboss-eap-7.0
PATH=$PATH:$JBOSS_HOME/bin
export JBOSS_HOME PATH
```

### Navigating your JBoss EAP Installation

A default JBoss EAP installtation has the following folders in `JBOSS_HOME`:

{{< figure src="../images/eap_installation.jpg" title="JBoss EAP 7 Installation Directories" >}}

Some of the main folders include:
- `bin`: Contains scripts used for starting EAP in managed domain and standalone server, start
the management CLI and other utility functions for developers
- `standalone` and `domain`: Contains configuration and data files for running JBoss EAP in either operational mode
- `modules`: Contains most of the code that implement Java EE services in JBoss EAP.

### Staring JBoss EAP
Shell scripts and Windows batch scripts are provided to start JBoss EAP 7 as either a standalone
server or in domain mode. They are `standalone.sh` and `domain.sh` and are found under the
`bin` folder in the JBoss EAP installation directory (`JBOSS_HOME`). A description of the two operating modes can be found in the next lab.

For the purposes of this workshop, we will be using standalone mode. To start JBoss EAP in standalone mode, run the following command:

```
$ ${JBOSS_HOME}/bin/standalone.sh
```
Once the startup is complete, you should see the following message:

{{< figure src="../images/jboss_startup.png" title="JBoss EAP Startup Console" >}}

JBoss EAP 7 starts up very fast! This should happen in only a few seconds.

### Verifying the Installation

[zip]: https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/installation_guide/installing_jboss_eap#zip_installation
[jar]: https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/installation_guide/installing_jboss_eap#installer_installation
[rpm]: https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/installation_guide/installing_jboss_eap#rpm_installation
[xpaas]: https://www.openshift.com/container-platform/middleware-services.html
