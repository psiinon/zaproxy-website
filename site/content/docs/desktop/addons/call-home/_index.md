---
# This page was generated from the add-on.
title: Call Home
type: userguide
weight: 1
cascade:
  addon:
    id: callhome
    version: 0.16.0
---

# Call Home

This add-on will be used for all "calls home".


It currently supports:

## Check For Updates

The Check for Updates call is used to find out the latest information about ZAP and the published add-ons. It is a mandatory add-on from ZAP 2.12.0 as this feature is used by the ZAP core.

## News

The News call is used to find out the latest news item about ZAP - this is displayed in the ZAP desktop Quick Start panel.

## Telemetry

The Telemetry call reports the add-ons being used and some of the ZAP internal statistics. It will never collect details of the sites ZAP is being used on, details of the vulnerabilities or any personal identifiable information (PII).


For more background see the blog post [ZAP Telemetry Plans](/blog/2021-10-25-zap-telemetry-plans/).

## Command Line option: -notel

If `-notel` is specified on the command line then no telemetry calls will be made. The other calls will not be affected. Telemetry calls will also not be made if the standard `-silent` ZAP command line option is used.

## Call Home Options Panel

This panel allows you to turn telemetry support on and off.


It also displays the last set of telemetry data transmitted.
The telemetry data is also logged at DEBUG level in the ZAP log file.
