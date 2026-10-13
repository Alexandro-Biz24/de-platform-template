# Bronze bucket access policy

- **Bucket:** `gs://NOM-DU-BUCKET-GROUPE`
- **Region:** `europe-west1`
- **Access model:** Uniform bucket-level access
- **Status:** Proposed — not yet applied
- **Last reviewed:** 2026-10-12

## Planned IAM bindings

| Principal | Role | Scope | Reason |
|---|---|---|---|
| `group:GROUP-DATA-ENGINEERING@albertschool.com` | `roles/storage.objectAdmin` | Entire bucket | Allows project members to upload, verify and manage Bronze objects during development |
| `serviceAccount:bronze-writer-g01@data-engineering-a.iam.gserviceaccount.com` | `roles/storage.objectCreator` | Entire bucket | Allows the ingestion pipeline to create new immutable Bronze objects without deleting existing data |
| `serviceAccount:bronze-writer-g01@data-engineering-a.iam.gserviceaccount.com` | `roles/storage.objectViewer` | Entire bucket | Allows the ingestion pipeline to detect existing objects and verify uploads |
| `serviceAccount:bronze-reader-g01@data-engineering-a.iam.gserviceaccount.com` | `roles/storage.objectViewer` | Entire bucket | Provides read-only access for BigQuery and authorised analytical workloads |
| `group:PLATFORM-ADMINS@albertschool.com` | `roles/storage.admin` | Entire bucket | Allows authorised administrators to manage IAM, lifecycle and bucket configuration |

## Access principles

- Access follows the principle of least privilege.
- The ingestion service account can create and verify objects but cannot delete them.
- Analytical workloads receive read-only access.
- Administrative access is restricted to the platform administrators.
- No object is publicly accessible.
- Uniform bucket-level access is enabled.
- Individual service-account keys are not downloaded; impersonation is preferred.
- Prefixes such as `bronze/` are organisational paths and are not independent security boundaries.

## Sensitive data

The source export contains passwords, card numbers, CVVs, names, addresses, telephone numbers and email addresses.

Direct analytical access to these fields must not be granted. Passwords, card numbers and CVVs must be excluded from future analytical ingestion or isolated in a separately protected storage area.

## Current limitation

These bindings have not yet been applied because the team does not currently have permission to create service accounts or modify IAM policies. The policy will be applied and verified when the required permissions are granted.