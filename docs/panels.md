# Panel Reference

This document describes purpose and wiring for key panels that use summary lookups
or opinionated filters. It is a quick guide for troubleshooting and tuning.

Summary lookups are populated by scheduled searches in `default/savedsearches.conf`.
These searches are disabled by default, so enable or run them manually if the
summary panels show empty results.

## pfSense Overview

### Block Rate vs 7d Avg
- Purpose: Compare current block rate to a 7-day baseline to highlight spikes.
- Data source: `pfsense_baseline_block_rate` (daily summary lookup).
- Summary search: `pfSense - Baseline Block Rate (7d)` in `default/savedsearches.conf`.
- Time range: Uses dashboard time picker for the current window.

### Unique Sources vs 7d Avg
- Purpose: Compare current unique source rate (per hour) to a 7-day baseline.
- Data source: `pfsense_baseline_unique_sources_hourly` (daily summary lookup).
- Summary search: `pfSense - Baseline Unique Sources Per Hour (7d)` in `default/savedsearches.conf`.
- Time range: Uses dashboard time picker for the current window.

### New External Blocked Sources (Last 48h)
- Purpose: Surface external sources that were first seen in the last 48h and are currently being blocked.
- Filters: external IPs only, `action=blocked`, minimum hits >= 10.
- Data source: `pfsense_ip_seen` (summary lookup of first/last seen per source).
- Summary search: `pfSense - IP Seen (First/Last)` in `default/savedsearches.conf`.
- Time range: Hard-coded to last 48h (does not follow the page time picker).

### New Internal Talkers (Last 48h)
- Purpose: Identify internal sources first seen in the last 48h.
- Filters: RFC1918/ULA sources only, minimum hits >= 5.
- Data source: `pfsense_ip_seen` (summary lookup of first/last seen per source).
- Summary search: `pfSense - IP Seen (First/Last)` in `default/savedsearches.conf`.
- Time range: Hard-coded to last 48h (does not follow the page time picker).

## pfSense DNSBL

### New Blocked Domains (Last 24h)
- Purpose: Highlight newly blocked domains that were not seen in the prior 7 days.
- Filters: Uses dashboard tokens; minimum blocks >= 5.
- Data source: `pfsense_known_dnsbl_domains_prev7d`.
- Summary search: `pfSense - Known DNSBL Domains (Prev 7d, Exclude Last 24h)`.
- Time range: Hard-coded to last 24h.

## pfSense IP Block

### New Blocked Destinations (Last 24h)
- Purpose: Surface destination IPs first seen in the last 24h.
- Filters: Uses dashboard tokens; minimum blocks >= 5.
- Data source: `pfsense_known_iplog_dests_prev7d`.
- Summary search: `pfSense - Known IP Block Destinations (Prev 7d, Exclude Last 24h)`.
- Time range: Hard-coded to last 24h.
