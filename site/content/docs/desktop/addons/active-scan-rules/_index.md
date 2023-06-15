---
# This page was generated from the add-on.
title: Active Scan Rules
type: userguide
weight: 1
cascade:
  addon:
    id: ascanrules
    version: 55.0.0
---

# Active Scan Rules

The following release status active scan rules are included in this add-on:

## .env Information Leak

Checks for web accessible .env files which may leak sensitive information (such as usernames, passwords, API or APP keys, etc.). Environment files come in many flavors but mostly they are KEY=VALUE formatted.   
This rule checks for how servers deliver them by default; NGINX returns them as binary/octet-stream content-type Apache just returns the text with no content-type. This rule also check for content length over 500 characters to try and exclude larger, possibly intentional, files.

Latest code: [EnvFileScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/EnvFileScanRule.java)

## .htaccess Information Leak

Checks for web accessible .htaccess files which may leak sensitive information (such as usernames, error handling, redirects, directory listing settings, etc.).

Latest code: [HtAccessScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/HtAccessScanRule.java)

## Buffer Overflow

Looks for indicators of buffer overflows in compiled code. It does this by putting out large strings of input text and look for code crash and abnormal session closure.

Latest code: [BufferOverflowScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/BufferOverflowScanRule.java)

## Cloud Metadata Attack

Attempts to abuse a misconfigured NGINX server in order to access the instance metadata maintained by cloud service providers such as AWS, GCP, Azure, and Alibaba.  
Most of these services provide metadata via an internal unroutable IP address '169.254.169.254' ('100.100.100.200' for Alibaba) - this can be exposed by incorrectly configured NGINX servers and accessed by using this IP address in the Host header field.

Latest code: [CloudMetadataScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/CloudMetadataScanRule.java)

## Code Injection

This rule submits PHP and ASP attack strings as values for URL parameters in a request and examines the response to see if those values have been evaluated by the server. First, requests are constructed and sent containing injected PHP instructions to print a token. In the event of a match between the token and the content of the response body, the scanner raises an alert and returns immediately. If there aren't any matches, the scanner will construct requests with several injected ASP strings that instruct the server to write the product of two randomly generated integers in the response. If the body of the response matches the product, an alert is raised.

Latest code: [CodeInjectionScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/CodeInjectionScanRule.java)

## Command Injection

This rule submits \*NIX and Windows OS commands as URL parameter values to determine whether or not the web application is passing unchecked user input directly to the underlying OS. The injection strings consist of meta-characters that may be interpreted by the OS as join commands along with a payload that should generate output in the response if the application is vulnerable. If the content of a response body matches the payload, the scanner raises an alert and returns immediately. In the event that none of the error-based matching attempts return output in the response, the scanner will attempt a blind injection attack by submitting sleep instructions as the payload and comparing the elapsed time between sending the request and receiving the response against a heuristic time-delay lower limit. If the elapsed time is greater than this limit, an alert is raised with medium confidence and the scanner returns immediately.   
Post 2.5.0 you can change the length of time used for the blind injection attack by changing the `rules.common.sleep` parameter via the Options 'Rule configuration' panel.

Latest code: [CommandInjectionScaRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/CommandInjectionScaRule.java)

## Cross Site Scripting (Reflected)

This rule starts by submitting a 'safe' value and analyzing all of the locations in which this value occurs in the response (if any).   
It then performs a series of attacks specifically targeted at the location in which each of the instances occurs, including tag attributes, URL attributes, attributes in tags which support src attributes, html comments etc.   
Note:   
This rule only scans HTTP PUT requests at LOW threshold.  
If the alert threshold is set to LOW, XSS injection located in a JSON response results in a LOW risk and LOW confidence alert is raised. For other response content-types a LOW confidence alert is raised.  
If the alert threshold is set to either MEDIUM or HIGH, XSS injection located in non-HTML responses do not generate alerts.  

Latest code: [CrossSiteScriptingScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/CrossSiteScriptingScanRule.java)

## Cross Site Scripting (persistent)

This rule starts by submitting a unique 'safe' value and then spiders the whole application to find all of the locations in which the value occurs.  
It then performs a series of attacks in the same way that the 'reflected' version does but in this case checks all of the target locations in other pages.  
Note:   
This rule only scans HTTP PUT requests at LOW threshold.  
If an XSS injection is located in a JSON response a LOW risk and LOW confidence alert is raised.  

Latest code: [PersistentXssPrimeScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/PersistentXssPrimeScanRule.java),
[PersistentXssSpiderScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/PersistentXssSpiderScanRule.java),
[PersistentXssScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/PersistentXssScanRule.java)

## CRLF Injection

This rule submits various CRLF special characters preceding an injected "Set-Cookie" header as a parameter to the server. If the response contains an identical Set-Cookie header, an alert is raised and the scanner returns immediately.

Latest code: [CrlfInjectionScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/CrlfInjectionScanRule.java)

## Directory Browsing

This rule checks to see if a request will provide access to a directory listing by examining the response body for patterns used with Apache, IIS and other web server software.

Latest code: [DirectoryBrowsingScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/DirectoryBrowsingScanRule.java)

## ELMAH Information Leak

Tests to see if the Error Logging Modules and Handlers (elmah.axd) HTTP Module is available. Although this module is handy for developers and other stakeholders it can also leak a significant amount of information which a security analyst or malicious individual may be interested in.  

The ELMAH scan rule targets Microsoft based technologies: IIS, Windows, ASP, and MSSQL.  
Files are only reported if they contain the text "Error Log for" unless a LOW alert threshold is set.

Latest code: [ElmahScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/ElmahScanRule.java)

## External Redirect

This rule submits a variety of URL redirect strings as parameter values in a request, then examines the headers and bodies of responses to determine whether or not a redirect occurred and of what type. The cause of redirect is searched for in the "Location" and "Refresh" header fields, as well as by HTML meta tags and Javascript in the body of the response. An alert is raised including the redirection type and the scanner returns immediately.

Latest code: [ExternalRedirectScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/ExternalRedirectScanRule.java)

## Format String Error

Looks for indicators of format string handling errors in compiled code. It does this by putting out strings of input text based upon characters compiled C code anticipates to produce formatted output and look for code crash and abnormal session closures.

Latest code: [FormatStringScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/FormatStringScanRule.java)

## GET for POST

This scan rule takes `application/x-www-form-urlencoded` POST requests, changes the parameters from POST to GET and resubmits the request. If the GET response is the same as the original POST response then an alert is raised. While this does not necessarily represent a security weakness unto itself it may indicate that other attacks or weaknesses can be expanded or simplified. (Such as a POST based Cross-Site Scripting (XSS) attack being changed to GET.)

Latest code: [GetForPostScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/GetForPostScanRule.java)

## Heartbleed OpenSSL Vulnerability

Detects if the web server is vulnerable to the Heartbleed OpenSSL Vulnerability, by exploiting it. For further details refer to CVE-2014-0160.

Latest code: [HeartBleedActiveScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/HeartBleedActiveScanRule.java)

## Hidden File Finder

This scan rule checks for various web accessible files which may leak administrative, configuration, or credential information. The original included set of payloads were based on [Snallygaster](https://github.com/hannob/snallygaster) by Hanno Böck. Such payloads are verified by checking response code, and content. If the response code is 200 (Ok) then additional content checks are performed to increase alert confidence. If the response code is 401 (Unauthorized) or 403 (Forbidden) or the content checks are un-successful then an alert is raised with lower confidence (at HIGH Threshold). **Note:** If the Custom Payloads addon is installed you can add your own hidden file paths (payloads) in the Custom Payloads options panel. For custom payloads only the response status code is checked. If there is a requirement to include a content check then it is also possible to add payloads to the `json/hidden_files.json` file in ZAP's user directory (in which case they will be treated as included payloads).

The following describes the fields of the JSON entries.


    {
      "path":"some/path/without/leading/slash.ext",
      "content":["content you want to find in responses"],
      "not_content":["content you do not want the response to have"],
      "binary":"\\x01\\x00",
      "links":["https://example.com/relevant/reference.html,"https://other.example.org/"],
      "type":"short_identifier",
      "source":"attribution_not_used_by_output_or_checks"
    }

Details worth noting:

* The only field that is required is path.
* The fields content, not_content, and links can have multiple quoted, comma separated values (arrays of strings).
* Checks of binary content are based on starting position 0 (ex: startsWith not contains).

The following is an example JSON entry:


    {
      "path":"CVS/root",
      "content":[":"],
      "not_content":["<"],
      "type":"cvs_dir",
      "source":"snallygaster"
    }

Latest code: [HiddenFilesScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/HiddenFilesScanRule.java)

## Padding Oracle

This rule attempts to manipulate the padding of encrypted strings to trigger an error response indicating a likely padding oracle vulnerability. Such a vulnerability can affect any application or framework that uses encryption improperly, such as some versions of ASP.net, Java Server Faces, and Mono.

Latest code: [PaddingOracleScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/PaddingOracleScanRule.java)

## Parameter Tampering

This rule submits requests with parameter values known to cause errors to be displayed to the user if handled improperly. Responses are checked to make sure that they return a server error status code, then compared with a normal HTTP response to make sure it does not raise an alert if the bad parameter has no effect on output. Finally, the content of the response body is compared against various patterns that may be found in Java servlet, Microsoft VBScript, OLE DB, JET, PHP and Tomcat errors. If a match is found, an alert is raised and the scanner returns immediately.

Latest code: [ParameterTamperScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/ParameterTamperScanRule.java)

## Path Traversal

This rule attempts to access files and directories outside of the web document root by constructing various combinations of pathname prefixes and local file targets for Windows and \*NIX systems as well as Java servlets. If the body of the response matches a pattern corresponding to the current target file an alert is raised and the scanner returns immediately. If none of the common local file targets succeed, path traversal is attempted using the filename in the URL. As long as submitting an arbitrary filename does not return an OK status code but the real filename does, an alert is raised and the scanner returns immediately.

Note: This scan rule has one check that is excluded at High Alert Threshold.

Latest code: [PathTraversalScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/PathTraversalScanRule.java)

## Remote Code Execution - CVE-2012-1823

Detect CVE-2012-1823 to perform Remote Code Execution on a PHP-CGI based web server.

Latest code: [RemoteCodeExecutionCve20121823ScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/RemoteCodeExecutionCve20121823ScanRule.java)

## Remote File Include

This rule submits a series of requests with external URLs as parameter values and looks for a match between the response body and the title of the page hosted at those URLs. If there is a match between the expected string and the response body, and the header returned a status code of 200, an alert is raised and the scanner returns immediately.

Latest code: [RemoteFileIncludeScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/RemoteFileIncludeScanRule.java)

## Server Side Include

This rule checks to see what OS the server is running on, then sends requests with a corresponding HTML SSI directive as a parameter value. If the response body matches a pattern indicating the SSI was successful, an alert is raised and the scanner returns immediately.

Latest code: [ServerSideIncludeScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/ServerSideIncludeScanRule.java)

## Source Code Disclosure - CVE-2012-1823

Exploit CVE-2012-1823 to disclose server-side PHP source code on a PHP-CGI based web server.  
Only analyzes responses that are text based (HTML, JSON, XML, etc.), in order to avoid false positives which may occur with image or other binary content.  
JavaScript responses are only analyzed when a LOW alert threshold is set.

Latest code: [SourceCodeDisclosureCve20121823ScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SourceCodeDisclosureCve20121823ScanRule.java)

## Source Code Disclosure - /WEB-INF

Exploit the presence of an unprotected /WEB-INF folder to download and decompile Java classes, to disclose Java source code.

Latest code: [SourceCodeDisclosureWebInfScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SourceCodeDisclosureWebInfScanRule.java)

## SQL Injection

This scanner scans for SQL Injection vulnerabilities in an RDBMS-independent fashion, by attacking url parameters and form parameters with fragments of valid and invalid SQL syntax, using error based, boolean based, Union based, and stacked query SQL Injection techniques.   
This scanner may be able to fingerprint the RDBMS if the application throws a known RDBMS specific SQL error message.   
This scanner does not exploit any RDBMS specific techniques, and so is the best SQL injection scanner to use as a starting point.

Latest code: [SqlInjectionScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SqlInjectionScanRule.java)

## SQL Injection - Hypersonic (Time Based)

This rule uses Hypersonic-specific SQL syntax to attempt to induce time delays in the SQL statement called by the page.  
If the unmodified query is not affected by a time delay, and the modified query's delay can be controlled, it is indicative of a time-based SQL Injection vulnerability in a Hypersonic SQL database.   
This rule is time sensitive, and should only be used in an attempt to find stubborn and un-obvious SQL injection vulnerabilities in a suspected Hypersonic database.   
For this reason, the number of active scan threads should be set to the minimum when using this scan rule, to minimise load on the web server, application server, and database, in order to avoid false positives caused by load delays rather than by SQL injection delays.   
The rule tests only for time-based SQL injection vulnerabilities.  

Post 2.5.0 you can change the length of time used for the attack by changing the `rules.common.sleep` parameter via the Options 'Rule configuration' panel.

Latest code: [SqlInjectionHypersonicScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SqlInjectionHypersonicScanRule.java)

## SQL Injection - MsSQL

This active scan rule attempts to inject MsSQL specific sleep commands into parameter values and analyzes the server's response time to see if the sleep is effectively executed on the server (indicating a successful SQL injection attack).

Latest code: [SqlInjectionMsSqlScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SqlInjectionMsSqlScanRule.java)

## SQL Injection - MySQL (Time Based)

This rule uses MySQL-specific SQL syntax to attempt to induce time delays in the SQL statement called by the page.  
If the unmodified query is not affected by a time delay, and the modified query's delay can be controlled, it is indicative of a time-based SQL Injection vulnerability in a MySQL database.   
This rule is time sensitive, and should only be used in an attempt to find stubborn and un-obvious SQL injection vulnerabilities in a suspected MySQL database.   
For this reason, the number of active scan threads should be set to the minimum when using this scan rule, to minimise load on the web server, application server, and database, in order to avoid false positives caused by load delays rather than by SQL injection delays.   
The rule tests only for time-based SQL injection vulnerabilities.  

Post 2.5.0 you can change the length of time used for the attack by changing the `rules.common.sleep` parameter via the Options 'Rule configuration' panel.

Latest code: [SqlInjectionMySqlScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SqlInjectionMySqlScanRule.java)

## SQL Injection - Oracle (Time Based)

This scan rule uses Oracle-specific SQL syntax to attempt to induce time delays in the SQL statement called by the page.  
If the unmodified query is not affected by a time delay, and the modified query's delay can be controlled, it is indicative of a time-based SQL Injection vulnerability in a Oracle SQL database.   
This rule is time sensitive, and should only be used in an attempt to find stubborn and un-obvious SQL injection vulnerabilities in a suspected Oracle database.   
For this reason, the number of active scan threads should be set to the minimum when using this rule, to minimise load on the web server, application server, and database, in order to avoid false positives caused by load delays rather than by SQL injection delays.   
The scan rule tests only for time-based SQL injection vulnerabilities.  

Note that this rule does not currently allow you to change the length of time used for the timing attacks due to the way the delay is caused.

Latest code: [SqlInjectionOracleScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SqlInjectionOracleScanRule.java)

## SQL Injection - PostgreSQL (Time Based)

This rule uses PostgreSQL-specific SQL syntax to attempt to induce time delays in the SQL statement called by the page.  
If the unmodified query is not affected by a time delay, and the modified query's delay can be controlled, it is indicative of a time-based SQL Injection vulnerability in a PostgreSQL database.   
This scan rule is time sensitive, and should only be used in an attempt to find stubborn and un-obvious SQL injection vulnerabilities in a suspected PostgreSQL database.   
For this reason, the number of active scan threads should be set to the minimum when using this scan rule, to minimise load on the web server, application server, and database, in order to avoid false positives caused by load delays rather than by SQL injection delays.   
The rule tests only for time-based SQL injection vulnerabilities.  

Post 2.5.0 you can change the length of time used for the attack by changing the `rules.common.sleep` parameter via the Options 'Rule configuration' panel.

Latest code: [SqlInjectionPostgreScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SqlInjectionPostgreScanRule.java)

## SQL Injection - SQLite

This active scan rule attempts to inject SQLite specific commands into parameter values and analyzes the server's responses to see if the commands were effectively executed on the server (indicating a successful SQL injection attack).

Latest code: [SqlInjectionSqLiteScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/SqlInjectionSqLiteScanRule.java)

## Trace.axd Information Leak

Tests to see if Trace Viewer (trace.axd) is available. Although this component is convenient for developers and other stakeholders it can leak a significant amount of information which a security analyst or malicious individual may be interested in.  

The trace.axd scan rule targets Microsoft based technologies: IIS, Windows, ASP, and MSSQL.

Latest code: [TraceAxdScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/TraceAxdScanRule.java)

## User Agent Fuzzer

This active scan rule checks for differences in response based on fuzzed User Agent (eg. mobile sites, access as a Search Engine Crawler). The rule compares the response statuscode and the hashcode of the response body with the original response.  
**Note:** If the Custom Payloads addon is installed you can add your own User Agent strings (payloads) in the Custom Payloads options panel.

Latest code: [UserAgentScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/UserAgentScanRule.java)

## XSLT Injection

This scan rule checks for certain responses induced by injecting XSL transformations.   
It attempts to obtain those responses with payloads which may induce: error responses, disclosure of library/framework vendor name, remote port scanning, or command execution.

Latest code: [XsltInjectionScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/XsltInjectionScanRule.java)

## XXE

This component attempts to identify applications which are subject to XML eXternal Entity (XXE) attacks. Applications which parse XML input may be subject to XXE when weakly or poorly configured parsers handle XML input containing reference to an external entity such as a local file, HTTP requests to internal or tertiary systems, etc. The number of tags which are tested individually depends on the strength of the rule.  

This scan rule will only run if the OAST add-on is installed and available. It is also recommended that you test that the Callbacks service in the OAST add-on is correctly configured for your target site. If the target system cannot connect to the Callback Address then some XXE vulnerabilities will not be detected.

Latest code: [XxeScanRule.java](https://github.com/zaproxy/zap-extensions/blob/main/addOns/ascanrules/src/main/java/org/zaproxy/zap/extension/ascanrules/XxeScanRule.java)
