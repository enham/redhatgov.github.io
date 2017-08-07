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

#### Modules

#### Subsystems and Profiles

### Managing JBoss EAP

#### Administrative Console

#### Command Line Interface 

#### XML File

### Logging into the Administrative Console

#### Changing a Configuration

