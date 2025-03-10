# ArgoCD Configuration Guide for Application Deployment

## Overview
This document provides step-by-step instructions on how to configure applications in ArgoCD. It uses `example-app` as a reference. Follow these steps to configure and deploy applications in ArgoCD in case of updates or new deployments.

---

## Application Configuration
### General Settings
- **Application Name:** `example-app`
- **Project Name:** `default`
- **Sync Policy:** `Manual`
  - Syncing must be manually triggered to deploy updates.

- **Sync Policy:** `Automatic`
  - Enable self heal.
- **Set Deletion Finalizer:** Not enabled.
- **Sync Options:**
  - `Skip Schema Validation` - Skips schema validation during deployment.
  - `Auto-Create Namespace` - Ensures the namespace is created before deployment.
  - `Prune Last` - Deletes obsolete resources after applying updates.
  - `Apply Out of Sync Only` - Ensures only out-of-sync resources are updated.
  - `Respect Ignore Differences` - Preserves configured ignored differences.
  - `Server-Side Apply` - Uses Kubernetes server-side apply method.
- **Prune Propagation Policy:** `background`
- **Replace Mode:** Enabled
  - Uses `kubectl replace/create`, which may recreate resources if needed.
  - Could reset replicas to minimum, potentially causing load on pods.
- **Retry:** Enabled for automatic retry in case of failure.

---

## Source Configuration
- **Repository URL:** `https://github.com/example-org/example-app.git`
- **Path:** `your path`
- **Included File:** `example.yaml`
- **Excluded Files:** None

---

## Destination Configuration
- **Cluster URL:** `https://kubernetes.default.svc`
- **Namespace:** `dev`


## Notes
- Sync must be manually triggered since `manual` sync policy is set.
- Replacing resources may cause pods to restart and lead to temporary service unavailability.
- Ensure all configurations in `frontend.yaml` are up to date before syncing.
- Namespace `development` should exist in the cluster or be auto-created if missing.

---

This guide ensures consistency and smooth deployments for `example-app` and similar applications in ArgoCD.
