# Contributing

Thanks for helping improve pfSense Dashboards.

## AppInspect

Run AppInspect against the packaged archive, not the repo root.

```bash
tar \
  --exclude="pfsense-dashboards/.git" \
  --exclude="pfsense-dashboards/.github" \
  --exclude="pfsense-dashboards/.gitignore" \
  --exclude="pfsense-dashboards/.claude" \
  --exclude="pfsense-dashboards/.DS_Store" \
  -czf pfsense-dashboards.tgz -C .. pfsense-dashboards

splunk-appinspect inspect pfsense-dashboards.tgz --data-format json \
  --output-file appinspect.json
```

## Packaging

The GitHub Actions release workflow builds a `.tgz` with the same excludes.
If you create archives locally, keep the same exclude list so AppInspect passes.
