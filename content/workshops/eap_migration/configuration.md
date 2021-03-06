---
title: Configuring JBoss EAP
workshops: eap_migration
workshop_weight: 40
layout: lab
---

## Configuring JBoss EAP

The purpose of this lab is to review the different management modes for JBoss EAP (standalone vs. domain) as well as the modular architecture of JBoss EAP.

### Management Modes: Standalone vs. Domain

A JBoss EAP 7 installation can be run in two operating modes: *standalone server* and *managed
domain*, as illustrated by the following figure:

{{< figure src="../images/standalone_vs_domain.png" title="Standalone vs. Domain Mode" >}}

#### Domain

To have the ability of managing multiple server instances, possibly deployed into multiple hosts, from a centralized location, JBoss EAP 7 can be provisioned in a managed domain. 

A domain controller process acts as the central management control point, communicating with the various host controllers in the managed domain. All of the hosts share a common management policy and the domain controller ensures that each server instance is configured according to that policy.

Each host in a domain has a host controller. Exactly one of the host controllers in a domain is designated as the domain controller. That is, the domain controller is also a host controller. The domain controller is also referred to as the master, and the other hosts controllers in the domain are referred to as slaves. Nothings prevents a domain controller having its own server instances, but having it as a dedicated administration host controller, as suggested by the previous figure, is a common practice.

#### Standalone

Standalone server mode represents a single server instance with a single configuration file named `standalone.xml`. It has the full operational capability of JBoss EAP 7 that domain mode has (including clustering, etc.) but lacks centralized management. 

### Modules in JBoss EAP 
JBoss EAP 7 is based on a core infrastructure provided by the WildFly project that, among other tasks, manages the loading and activation of modules, following the architecture provided by the JBoss Modules project. A module basically provides code (Java Classes) to be used by JBoss EAP services and/or by applications.

The following figure shows the main components inside EAP 7. It shows, on the upper half, components that are part of the WildFly Core project (the EAP core), most of them modules themselves. The lower half shows modules provided by other JBoss community projects, that are integrated into the WildFly Full project and then productized and supported by Red Hat as JBoss
EAP 7.

{{< figure src="../images/eap_modules.jpg" title="JBoss EAP Modular Architecture" >}}

#### Modules/Extensions and Subsystems

A module that provides features and capabilities to the application server is called an extension. An extension does not simply provide code, but also provides a way of managing that functionality, consisting of one or mode subsystems, that allows the extension to be configured by the core.

#### Profiles

Subsystems can be grouped into profiles, which provide a set of functionality given a target use case. The out-of-the-box profiles are described in the image below:

{{< figure src="../images/eap_profiles.jpg" title="JBoss EAP Profiles" >}}

A high-level description of the profiles follows:

1. `default`: The most commonly used subsystems, including logging, security, datasources, infinispan, weld, webservices, and ejb3. The default implements not only the Java EE Web Profile, but also most of the Java EE Full Profile.
2. `ha`: Contains the exact same subsystems as the default profile, with the addition of clustering capabilities, provided mainly by the jgroups subsystem.
3. `full`: Similar to the default profile, but notably adds the messaging (messaging-activemq) and a few other less used subsystems.
4. `full-ha`: Same as the full profile, but with the addition of clustering capabilities.

### Managing JBoss EAP

There are three ways of managing JBoss EAP:

1. Administrative Console: Using a browser, this web-based application allows a System Administrator to manage most of the capabilities of your standalone or managed domain deployments.
2. Command Line Interface (CLI): Using a terminal window, the CLI offers a management model for viewing and modifying attributes and for performing operations, including batch operations, on a standalone server or a managed domain. The CLI includes user-friendly features like contextual auto-complete, built-in documentation of server configuration attributes, and command execution history.
3. XML File: The settings of a standalone server or a managed domain are maintained in XML-based configuration files which can be modified directly.

No matter which technique is used to modify a configuration setting, all changes are synchronized to the XML configuration files.

#### Administrative Console

To access the JBoss EAP 7 management console, launch the web browser and navigate to `http://localhost:9990`. Login using the credentials you created during the installation process (u: `admin`, pw: `Redhat1!`). The welcome screen should look like:

{{< figure src="../images/admin_console.jpg" title="JBoss EAP Administrative Console" >}}

Next, navigate to the JVM Status page. The JVM (Java Virtual Machine) is responsible for managing the amount of memory used by the application server and deployed applications, as well as to manage classloading. In this step, you will read the metrics obtained from the JVM, using the EAP management console. View the JVM Status page of the EAP management console. Navigate to `Runtime > Standalone Server > JVM` and click the View button to view the JVM details.

{{< figure src="../images/jvm_status.jpg" title="JBoss EAP JVM Status Page" >}}

Next, try viewing the logs. The JBoss EAP server logs are stored in the local filesystem, but sometimes due to filesystem
access restrictions, the administrator may need to access it via a web console.

Click the blue <<Back link on the top left corner of the JVM Status page to go back and navigate to (Runtime > Standalone Server > Log Files) and click the View button to view the log viewer.

Select the server.log entry in the table displayed and click the View button to view the server logs.

#### Command Line Interface 

The Command Line Interface, or CLI for short, to manage and configure JBoss EAP instances remotely from a command line, including writing scripts for repetitive tasks.

Some of the benefits of using the CLI include:
- Manage servers without the need of a GUI, which introduces the possibility of automation.
- Commands can be written in a separate file and executed as a batch, allowing you to write scripts for common tasks.
- The Management Console has limitations, but the CLI configures almost every aspect of the XML configuration files.

The CLI is started by running the `jboss-cli.sh` script in the bin folder of the JBoss EAP installation. This script does not require any arguments and if arguments are not provided, it will start in disconnected mode:

```
# $JBOSS_HOME/bin/jboss-cli.sh
[disconnected /]
```

The connect command is responsible for connecting to the server. If no argument is provided, it will try to connect to the default host (localhost) using the default port (9990).

```
[disconnected /] connect localhost:9990
```

TO DO...

#### XML File

### Logging into the Administrative Console

#### Changing a Configuration

