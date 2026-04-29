---
name: file-upload-system
description: "Set up S3/R2 file upload infrastructure with presigned URLs, image optimization, and security validation. Use when adding file uploads to an application, configuring cloud storage (AWS S3, Cloudflare R2, DigitalOcean Spaces), or implementing secure direct-to-storage uploads."
user-invocable: true
triggers:
  - add file uploads
  - setup S3 uploads
  - configure R2 storage
  - implement presigned URLs
  - file upload component
---

# File Upload System

Set up a complete file upload system with S3/R2 SDK, upload components, presigned URLs, image optimization, and security validation.

## When to Use

- Adding file upload functionality to a web application
- Configuring cloud storage with AWS S3, Cloudflare R2, or DigitalOcean Spaces
- Implementing secure direct-to-storage uploads via presigned URLs
- Building image upload with resize, compress, and thumbnail generation

## Quick Start

```bash
python3 scripts/setup_uploads.py
```

This installs `@aws-sdk/client-s3` and `@aws-sdk/s3-request-presigner`, then generates `lib/s3.ts` with the S3 client configuration.

## Workflow

### 1. Configure Storage Provider

Set environment variables for the chosen provider:

| Provider | Region Var | Endpoint Override |
|----------|-----------|-------------------|
| AWS S3 | `AWS_REGION` | None needed |
| Cloudflare R2 | `AWS_REGION=auto` | `S3_ENDPOINT=https://<account>.r2.cloudflarestorage.com` |
| DigitalOcean Spaces | `AWS_REGION=<region>` | `S3_ENDPOINT=https://<region>.digitaloceanspaces.com` |

### 2. Choose Upload Pattern

**Direct Upload (presigned URLs)** — Client uploads directly to S3. Fastest, no server load, best for large files.

**Server Upload** — Client sends to server, server forwards to S3. More control and validation, good for small files.

See `references/upload_patterns.md` for detailed comparison.

### 3. Add Upload Component

Use the provided React component template at `templates/upload.tsx` as a starting point:

```tsx
import { FileUpload } from './templates/upload';
// Renders file input with upload button and loading state
```

### 4. Implement Security

- Validate file types (allowlist MIME types)
- Set size limits per upload
- Use presigned URLs with short expiration
- Scan uploaded content if handling user-generated files

## Bundled Resources

| Path | Purpose |
|------|---------|
| `scripts/setup_uploads.py` | Install dependencies and generate S3 client config |
| `templates/upload.tsx` | React file upload component with state management |
| `references/upload_patterns.md` | Comparison of upload patterns (direct vs server) |

## Time Saved

- **Manual setup**: ~2 hours
- **With this skill**: ~30 minutes
- **Savings**: ~1.5 hours per project

## Related Skills

- **api-endpoint-builder** — Build the upload API endpoint
- **testing-framework** — Test upload flows
- **deployment-automation** — Deploy with storage configuration
