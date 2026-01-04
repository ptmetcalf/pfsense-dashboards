# Contributing

Thanks for helping improve pfSense Dashboards.

## AppInspect

Run AppInspect against the packaged archive, not the repo root.

```bash
python3 -m venv .venv-appinspect
source .venv-appinspect/bin/activate
pip install --upgrade pip
pip install splunk-appinspect
pip install splunk-packaging-toolkit

mkdir -p dist

tar \
  --exclude="pfsense-dashboards/.git" \
  --exclude="pfsense-dashboards/.github" \
  --exclude="pfsense-dashboards/.gitignore" \
  --exclude="pfsense-dashboards/.release-please-config.json" \
  --exclude="pfsense-dashboards/.release-please-manifest.json" \
  --exclude="pfsense-dashboards/.claude" \
  --exclude="pfsense-dashboards/.DS_Store" \
  --exclude="pfsense-dashboards/.venv-appinspect" \
  --exclude="pfsense-dashboards/dist" \
  -czf dist/pfsense-dashboards.tgz -C .. pfsense-dashboards

splunk-appinspect inspect dist/pfsense-dashboards.tgz --data-format json \
  --output-file dist/appinspect.json

slim validate dist/pfsense-dashboards.tgz
```

## Packaging

The GitHub Actions release workflow builds a `.tgz` with the same excludes.
If you create archives locally, keep the same exclude list so AppInspect passes.
