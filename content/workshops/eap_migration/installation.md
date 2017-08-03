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
To install EAP, enter the following command:

```
$ java -jar jboss-eap-7.0.0-installer.jar
```
The following screenshot shows the welcome screen for the EAP installer in GUI mode:


#### Using the Graphical Installer

#### Staring and Stopping JBoss EAP

#### Logging into the Administrative Console

[zip]: https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/installation_guide/installing_jboss_eap#zip_installation
[jar]: https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/installation_guide/installing_jboss_eap#installer_installation
[rpm]: https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/installation_guide/installing_jboss_eap#rpm_installation
[xpaas]: https://www.openshift.com/container-platform/middleware-services.html
