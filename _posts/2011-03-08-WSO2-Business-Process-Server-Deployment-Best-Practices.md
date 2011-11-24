---
layout: post
title: WSO2 Business Process Server Deployment Best Practices
author: Milinda Pathirage
time: 8th March 2011 
comments: true
---

Default distribution of [WSO2 BPS](http://wso2.com/products/business-process-server) comes with embedded H2 database as [BPEL](http://docs.oasis-open.org/wsbpel/2.0/CS01/wsbpel-v2.0-CS01.html) engine’s persistence storage and other settings which are suitable for use in a development setup. But when you are going to production with WSO2 BPS, there are several configurations you need to change according to your production requirements. These configurations will change based on how much requests WSO2 BPS is going to handle per second, your auditing and monitoring requirements, performance requirements and nature of your process. Following are the main things you should do before go into production with WSO2 BPS.

Some of the below mention configurations are true for Apache ODE, but the way we configure Apache ODE is little bit different from WSO2 BPS. In addition to that below mention configuration are valid from WSO2 BPS 2.0.2 onwards. Configuration mechanisms of older WSO2 BPS versions are different.

* [Configure external database server](http://wso2.org/project/bps/2.0.2/docs/user_guide.html#Configuring-Ext-DS) like MySQL as your persistence storage instead of embedded H2 database. You may experience slight performance gain for simple BPEL processes with H2 database, but when it comes to multiple concurrent requests and complex processes H2 can’t server your performance needs.
* [Configure multi-threaded Http connection manager connection pool settings](http://wso2.org/project/bps/2.0.2/docs/user_guide.html#Using-Multi-Threaded-HTTP) to suits to your BPEL processes. There are two configurations in Http connection manager. One is max total connections and other is max total connection per host. These settings will depend on number of concurrent requests BPS needs to handle and number of external service calls in involve per process instance.
* [Configure BPEL process persistence](http://wso2.org/project/bps/2.0.2/docs/user_guide.html#Add-Set-In-memory-execution). If you are implementing process with request-response interaction model use in-memory processes instead of persistence processes. Whether to use in-memory or persisted processes will mainly depends on your business use-case.
* [Configure even-filtering](http://wso2.org/project/bps/2.0.2/docs/user_guide.html#Using-Events) at process and scope level. You can save lot of database resources by reducing number of events generated.
* Using process-to-process communication. If you are calling one BPEL process from another BPEL process deployed in the same BPS instance, it’s better to use process-to-process communication to reduce overhead introduce by additional network calls.
* Also make sure to configure process instance cleanup. Large number of process instance data will be accumulated in the BPEL engine persistence storage if you persisted processes, so to reduce performance overhead introduce by database size you should configure instance cleanup.
