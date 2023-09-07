---
type: page
title: Automation Framework
date: "2021-03-09"
tags: 
- guide
---
The new Automation Framework will in time replace the Command Line and Packaged Scan options.
It allows you to control ZAP via one YAML file and provides more flexibility while not being tied to any specific container technology.

The Automation Framework is included with the latest version of ZAP as well as the stable docker image.
The framework is plugable and many of the existing add-ons have been enhanced to support it.

### Updating Add-ons

The [addOns](/docs/desktop/addons/automation-framework/job-addons/) job has been found to cause
problems when updating add-ons which are defined in the current plan. This job has been depreciated and no longer does anything.

From 2.12 you can use the standard ZAP [command line](/docs/desktop/cmdline/) 
options with the AF `-autorun` option:

* `-addoninstall <addOnId>` to install an add-on
* `-addonuninstall <addOnId>` to uninstall an add-on
* `-addonupdate` to update all add-ons

You can use `-addoninstall` and `-addonuninstall` as many times as you need:

```bash
./zap.sh -addonupdate\
    -addoninstall example-1 \
    -addoninstall example-2 \
    -addonuninstall example-3 \
    -cmd -autorun zap.yaml <any other ZAP options>
```

### Framework Overview

For details of how to get started with the framework see the main [framework help page](/docs/desktop/addons/automation-framework/).

The framework supports:

* [environment](/docs/desktop/addons/automation-framework/environment/) - which defines all of the applications the plan can act on
* [Authentication](/docs/desktop/addons/automation-framework/authentication/) - all of the authentication mechanisms supported by ZAP
* [Job Tests](/docs/desktop/addons/automation-framework/tests/) - which can be used to validate the outcome of jobs

The full set of jobs currently supported by the framework and other add-ons are:

* [activeScan](/docs/desktop/addons/automation-framework/job-ascan/) - runs the active scanner
* [alertFilter](/docs/desktop/addons/alert-filters/automation/) - alert filter configuration, provided with the [Alert Filters](/docs/desktop/addons/alert-filters/) add-on
* [delay](/docs/desktop/addons/automation-framework/job-delay/) - waits for a specified time or until a condition is met
* [graphql](/docs/desktop/addons/graphql-support/automation/) - GraphQL schema import, provided with the [GraphQL](/docs/desktop/addons/graphql-support/) add-on
* [import](/docs/desktop/addons/import-export/automation/) - allows you to import HAR(HTTP Archive File), ModSecurity2 Logs, ZAP Messages or a file containing URLs locally
* [openapi](/docs/desktop/addons/openapi-support/automation/) - OpenAPI definition import, provided with the [OpenAPI](/docs/desktop/addons/openapi-support/) add-on
* [passiveScan-config](/docs/desktop/addons/automation-framework/job-pscanconf/) - passive scan configuration
* [passiveScan-wait](/docs/desktop/addons/automation-framework/job-pscanwait/) - waits for the passive scanner to finish processing the current queue
* [replacer](/docs/desktop/addons/replacer/automation/) - replace strings in requests and responses
* [report](/docs/desktop/addons/report-generation/automation/) - report generation, provided with the [Report Generation](/docs/desktop/addons/report-generation/) add-on
* [requestor](/docs/desktop/addons/automation-framework/job-requestor/) - sends specific requests to targets
* [script](/docs/desktop/addons/script-console/automation/) - adds, removes and runs scripts
* [soap](/docs/desktop/addons/soap-support/automation/) - SOAP WSDL import, provided with the [SOAP](/docs/desktop/addons/soap-support/) add-on
* [spider](/docs/desktop/addons/automation-framework/job-spider/) - runs the traditional spider
* [spiderAjax](/docs/desktop/addons/ajax-spider/automation/) - runs the ajax spider, provided with the [Ajax Spider](/docs/desktop/addons/ajax-spider/) add-on

For details of future changes planned see the [tracker issue](https://github.com/zaproxy/zaproxy/issues/6461).
