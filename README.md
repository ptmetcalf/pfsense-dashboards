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
DNS hosts). These are backed by KV store collections in the TA app, so empty
collections are safe and upgrades do not wipe enrichment data.

1. Generate SPL commands using `ta-pfsense-plus/tools/pfsense-lookups.py` from the repo
   (the helper script is not intended to be run inside the installed Splunk app).
2. Paste the generated SPL into Splunk Search to populate the KV store
   collections (see the TA README for details).

Optional DNS host, interface map, rule map, and zone subnet enrichment lookups live in the TA app. Use
the lookup generator from the repo (for example, `tools/pfsense-lookups.py enrichment`) to produce
instance-specific SPL from a pfSense `config.xml` dump.

### Summary Lookups (Auto-populated)

Several panels use summary lookups that are populated by scheduled searches in
this app. These searches are disabled by default; enable them in
**Settings > Searches, Reports, and Alerts** to populate the KV collections.
They run daily, so after install allow a day or run them manually. If you do not
enable or run them, panels that depend on these lookups will show limited or
empty data. When running ad-hoc, use the lookup name (for example
`outputlookup pfsense_ip_seen`) to ensure the KV store collection in this app is
updated:

* pfSense - Baseline Block Rate (7d)
* pfSense - Baseline Unique Sources Per Hour (7d)
* pfSense - IP Seen (First/Last)
* pfSense - Known DNSBL Domains (Prev 7d, Exclude Last 24h)
* pfSense - Known IP Block Destinations (Prev 7d, Exclude Last 24h)

The IP-seen job scans the last 30 days (`dispatch.earliest_time = -30d@d`) to
avoid long runtimes on large datasets.

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
![pfSense Overview](appserver/static/screenshots/01-pfsense-overview.jpeg)

Detailed event view with full field visibility.
![pfSense Detail](appserver/static/screenshots/02-pfsense-detail.jpeg)

DNSBL blocked domains analysis.
![pfSense DNSBL](appserver/static/screenshots/03-pfsense-dnsbl.jpeg)

Suricata alerts and signatures view.
![pfSense Suricata](appserver/static/screenshots/04-pfsense-suricata.jpeg)

pfBlockerNG IP block events.
![pfSense IP Log](appserver/static/screenshots/05-pfsense-iplog.jpeg)

Statistical trends and insights.

Host-centric investigation view.
![pfSense Host Investigator](appserver/static/screenshots/06-pfsense-host-investigator.jpeg)

All sensitive data (IPs, hostnames, domains) has been sanitized for public distribution.

## Support

For issues or feature requests, please use the GitHub repository issue tracker.
