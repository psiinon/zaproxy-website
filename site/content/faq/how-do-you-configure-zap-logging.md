---
title: "How do you configure ZAP logging?"
type: faq
category: Howtos
weight: 4
---

ZAP logs to a file called "zap.log" in the ZAP ['home'
directory](/faq/what-is-the-default-directory-that-zap-uses/).

The logging is configured by the
[log4j.properties](https://github.com/zaproxy/zaproxy/blob/develop/zap/src/main/resources/org/zaproxy/zap/resources/log4j.properties)
file in the same directory.

By default the 'main' logging levels are set to "INFO" by these 2 lines:

{{< terminal "log4j.properties" >}}
log4j.logger.org.parosproxy.paros=INFO
log4j.logger.org.zaproxy.zap=INFO
{{< /terminal >}}

Changing these to "DEBUG" (and restarting ZAP) will _significantly_ increase
the amount of logging performed:

{{< terminal "log4j.properties" >}}
log4j.logger.org.parosproxy.paros=DEBUG
log4j.logger.org.zaproxy.zap=DEBUG
{{< /terminal >}}

Logging can be selectively enabled using a [Stand Alone script](/docs/desktop/addons/script-console/#script-types) while ZAP is
running (the example below is a JavaScript script):

{{< terminal "enable_debug_logging.js" >}}
// The following will enable DEBUG logging for the API
org.apache.log4j.Logger.getLogger("org.zaproxy.zap.extension.api.API").setLevel(org.apache.log4j.Level.DEBUG);
// The following will enable DEBUG logging for the SessionFixation scanner
org.apache.log4j.Logger.getLogger("org.zaproxy.zap.extension.ascanrulesBeta.SessionFixation").setLevel(org.apache.log4j.Level.DEBUG);
{{< /terminal >}}
