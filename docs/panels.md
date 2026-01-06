# Panel Reference

This document describes purpose and wiring for key panels that use summary lookups
or opinionated filters. It is a quick guide for troubleshooting and tuning.

## pfSense Overview

### Block Rate vs 7d Avg
- Purpose: Compare current block rate to a 7-day baseline to highlight spikes.
- Data source: `pfsense_baseline_block_rate.csv` (hourly summary lookup).
- Summary search: `pfSense - Baseline Block Rate (7d)` in `default/savedsearches.conf`.
- Time range: Uses dashboard time picker for the current window.

### Start Here (Top Signals)
- Purpose: A compact, high-signal summary for quick triage.
- Signals: Block rate delta, unique sources delta, count of new external blocked sources.
- Data source: Summary lookups + live 24h search for new external blocked sources.
- Time range: Uses dashboard time picker for deltas; 24h window for new external sources.

### Unique Sources vs 7d Avg
- Purpose: Compare current unique source rate (per hour) to a 7-day baseline.
- Data source: `pfsense_baseline_unique_sources_hourly.csv` (hourly summary lookup).
- Summary search: `pfSense - Baseline Unique Sources Per Hour (7d)` in `default/savedsearches.conf`.
- Time range: Uses dashboard time picker for the current window.

### New External Blocked Sources (Last 24h)
- Purpose: Surface new, high-signal external sources that are getting blocked.
- Filters: external IPs only, `action=blocked`, minimum hits >= 10.
- Data source: `pfsense_known_sources_prev7d.csv` (sources from prior 7d, excluding last 24h).
- Summary search: `pfSense - Known Sources (Prev 7d, Exclude Last 24h)` in `default/savedsearches.conf`.
- Time range: Hard-coded to last 24h (does not follow the page time picker).

### New Internal Talkers (Last 24h)
- Purpose: Identify new internal hosts or misconfigured clients.
- Filters: RFC1918/ULA sources only, minimum hits >= 5.
- Data source: `pfsense_known_sources_prev7d.csv` (sources from prior 7d, excluding last 24h).
- Summary search: `pfSense - Known Sources (Prev 7d, Exclude Last 24h)` in `default/savedsearches.conf`.
- Time range: Hard-coded to last 24h (does not follow the page time picker).

## pfSense DNSBL

### New Blocked Domains (Last 24h)
- Purpose: Highlight newly blocked domains that were not seen in the prior 7 days.
- Filters: Uses dashboard tokens; minimum blocks >= 5.
- Data source: `pfsense_known_dnsbl_domains_prev7d.csv`.
- Summary search: `pfSense - Known DNSBL Domains (Prev 7d, Exclude Last 24h)`.
- Time range: Hard-coded to last 24h.

## pfSense IP Block

### New Blocked Destinations (Last 24h)
- Purpose: Surface destination IPs first seen in the last 24h.
- Filters: Uses dashboard tokens; minimum blocks >= 5.
- Data source: `pfsense_known_iplog_dests_prev7d.csv`.
- Summary search: `pfSense - Known IP Block Destinations (Prev 7d, Exclude Last 24h)`.
- Time range: Hard-coded to last 24h.
