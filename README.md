# pfSense Dashboards

Splunk dashboards for pfSense firewall, DNSBL, and pfBlockerNG IP block
activity, built for investigation and operational visibility.

## Requirements

* Splunk Enterprise 8.0+
* **TA-pfsense-plus** installed (required for field extractions)

## Install

1. Install from Splunkbase, or copy the app to `$SPLUNK_HOME/etc/apps/pfsense-dashboards`.
2. Restart or reload Splunk.

## Configuration

### Index Configuration

By default, dashboards search `index=pfsense`. To use a different index:

1. Create `$SPLUNK_HOME/etc/apps/pfsense-dashboards/local/macros.conf`
2. Add the following:

```
[pfsense_index]
definition = index=your_pfsense_index
```

3. Restart Splunk or refresh the app

### Data Requirements

* Firewall logs: `sourcetype=pfsense:filterlog`
* DNSBL data: `sourcetype=pfsense:dnsbl`
* IP block data: `sourcetype=pfsense:iplog`
* VPN logs: `sourcetype=pfsense:openvpn`
* DNS queries: `sourcetype=pfsense:unbound`
* IDS/IPS: `sourcetype=pfsense:suricata`

### Lookup Enrichment (Optional)

The dashboards can be enriched with optional pfSense lookups (rules, interfaces,
DNS hosts). The supported pattern is to copy the generated CSVs into the TA app
lookups directory so the dashboards can resolve them.

1. Generate the CSVs using `ta-pfsense-plus/tools/pfsense-lookups.py`.
2. Copy the CSVs into `$SPLUNK_HOME/etc/apps/ta-pfsense-plus/lookups/`.
3. Restart or reload Splunk.

Optional interface/zone/gateway enrichment lookups live in the TA app. See
`docs/panels.md` and use
`$SPLUNK_HOME/etc/apps/ta-pfsense-plus/tools/pfsense-lookups.py enrichment`
to generate instance-specific CSVs from a pfSense `config.xml` dump.

### Summary Lookups (Auto-populated)

Several panels use summary lookups that are populated by scheduled searches in
this app. These run hourly, so after install allow at least an hour or run them
manually via **Settings > Searches, Reports, and Alerts**. When running ad-hoc,
use the lookup name (for example `outputlookup pfsense_ip_seen`) to ensure the
CSV writes into this app:

* pfSense - Baseline Block Rate (7d)
* pfSense - Baseline Unique Sources Per Hour (7d)
* pfSense - IP Seen (First/Last)
* pfSense - Known DNSBL Domains (Prev 7d, Exclude Last 24h)
* pfSense - Known IP Block Destinations (Prev 7d, Exclude Last 24h)

The IP-seen job scans the full time range (`dispatch.earliest_time = 0`), so on
large datasets it may take longer to populate.

## Dashboards

### pfSense Overview
Main dashboard for filtering and analyzing firewall events. Includes filters for action, direction, transport protocol, and rule origin.

### pfSense Detail
Detailed view of individual firewall events with full field visibility.

### pfSense DNSBL
Dashboard for pfBlockerNG DNS blacklist activity, showing blocked domains, source IPs, and feed information.

### pfSense Suricata
Suricata IDS dashboard for alerts, signatures, and top talkers.

### pfSense IP Log
Dashboard for pfBlockerNG IP block events, tracking blocked IPs by feed and geolocation.

### pfSense Host
Host-centric view for investigating specific source or destination hosts.

## Contributing

See `CONTRIBUTING.md` for AppInspect and packaging steps.

## Screenshots

Main overview dashboard with filters and statistics.
![pfSense Overview](appserver/static/screenshots/01-pfsense-overview.png)

Detailed event view with full field visibility.
![pfSense Detail](appserver/static/screenshots/02-pfsense-detail.png)

DNSBL blocked domains analysis.
![pfSense DNSBL](appserver/static/screenshots/03-pfsense-dnsbl.png)

pfBlockerNG IP block events.
![pfSense IP Log](appserver/static/screenshots/04-pfsense-iplog.png)

Statistical trends and insights.

Host-centric investigation view.
![pfSense Host Investigator](appserver/static/screenshots/06-pfsense-host-investigator.png)

All sensitive data (IPs, hostnames, domains) has been sanitized for public distribution.

## Support

For issues or feature requests, please use the GitHub repository issue tracker.
