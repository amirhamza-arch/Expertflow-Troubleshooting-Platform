# Troubleshooting Log

> Central archive for all troubleshooting outputs, errors, debug logs, and diagnostic sessions.

---

## Session: 2026-06-08

### Summary
Initial session focused on downloading Expertflow documentation, identifying deployment guides, and documenting WhatsApp integration steps for EFCX 5.1.0.

### Issues Encountered
| # | Issue | Resolution |
|---|-------|-----------|
| 1 | `wget` not available on Windows Git Bash | Switched to `curl` with parallel download (`curl -Z`) |
| 2 | Parallel download via `xargs -P` was slow | Replaced with native `curl --parallel-max 50` for 6,982 URLs |
| 3 | Some files had naming conflicts (directory vs file without extension) | Fixed by appending `.html` extension to all paths |
| 4 | Permission errors moving large directories | Used `git mv` for tracked files, `cp -r` + `rm` for untracked |
| 5 | `docs/expertflow-site/cx/4.5.1` could not be removed | Device busy — skipped and cleaned remaining files |

### Key Findings
- **Total docs downloaded:** ~9,100 files (~531 MB)
- **Key doc for WhatsApp:** `deployment/expertflow-site/cx/4.5.1/meta-whatsapp-cloud-api-configuration-deployment-g.html`
- **Key doc for deployment:** `deployment/expertflow-site/cx/5.1.0/deployment-guide.html`
- **Connector service name:** `cx-channels-whatsapp-connector-svc` (Helm-based)

### Commands Used
```bash
# Download all docs
curl -Z --parallel-max 50 --config /tmp/curl_config.txt

# Verify connector service
kubectl -n expertflow get svc | grep whatsapp-connector

# Search for specific terms
grep -ri "whatsapp-connector" deployment/expertflow-site/cx/
```

---

*Add new troubleshooting sessions below.*
