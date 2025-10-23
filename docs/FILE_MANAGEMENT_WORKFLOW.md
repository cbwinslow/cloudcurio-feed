# File Management and Knowledge Base Workflow

This document describes the file management workflow for cloudcurio.cc that helps manage files and generate blog posts from the microfeed CMS.

## Overview

The File Management workflow provides automated tools to:
- **Sync files** from Cloudflare R2 to a general knowledge base
- **Generate blog posts** automatically from managed content
- **Schedule automatic syncs** to keep content up-to-date
- **Track file changes** and generate reports

## Workflow Triggers

The workflow can be triggered in three ways:

### 1. Manual Trigger
Navigate to [Actions → File Management and Knowledge Base Sync](../../actions/workflows/file-management.yml) and click "Run workflow".

**Available Options:**
- **Operation**: Choose what to run
  - `sync-files`: Only sync files to knowledge base
  - `generate-blog-posts`: Only generate blog posts
  - `full-sync`: Run both operations (default)
- **Target Environment**: Choose deployment environment
  - `production`: Production environment (default)
  - `preview`: Preview/staging environment

### 2. Automatic on Content Changes
The workflow automatically runs when you push changes to `main` branch that affect:
- `public/**` - Public assets
- `functions/**` - API and admin functions
- `edge-src/**` - Edge application code

### 3. Scheduled Sync
The workflow runs automatically every day at 2:00 AM UTC to keep the knowledge base synchronized.

## What the Workflow Does

### File Synchronization (`sync-files`)

This operation:
1. Connects to your Cloudflare R2 bucket
2. Catalogs all media files (images, audio, video, documents)
3. Generates a file manifest with metadata
4. Creates a sync report for tracking

**Output:** 
- File manifest JSON in artifacts
- Sync status report

### Blog Post Generation (`generate-blog-posts`)

This operation:
1. Scans the managed files in the knowledge base
2. Extracts metadata and content
3. Generates blog post metadata
4. Creates structured data for your website

**Output:**
- Blog post metadata JSON in artifacts
- Generation status report

### Full Sync (`full-sync`)

Runs both operations in sequence for a complete update.

## Required Secrets

The workflow requires the following GitHub secrets to be configured:

| Secret | Description | How to Get |
|--------|-------------|------------|
| `CLOUDFLARE_API_TOKEN` | API token for Cloudflare | [Create token](https://dash.cloudflare.com/profile/api-tokens) with Pages and D1 edit permissions |
| `CLOUDFLARE_ACCOUNT_ID` | Your Cloudflare account ID | Found in dashboard URL: `dash.cloudflare.com/[account-id]` |
| `CLOUDFLARE_PROJECT_NAME` | Your Pages project name | The name you chose during setup |
| `R2_ACCESS_KEY_ID` | R2 access key | [Create from R2 dashboard](https://dash.cloudflare.com/r2) |
| `R2_SECRET_ACCESS_KEY` | R2 secret key | Generated with access key |
| `R2_PUBLIC_BUCKET` | R2 bucket name | Optional, defaults to project name |

See the main [README.md](../README.md#step-2-put-some-secrets-on-your-forked-repo) for detailed instructions on obtaining these secrets.

## Workflow Outputs

Each workflow run generates artifacts containing:

1. **File Manifests** (`.github/reports/`)
   - JSON files with timestamp
   - List of all synced files
   - Metadata and file information
   - Sync status and statistics

2. **Blog Post Metadata** (`.github/blog-posts/`)
   - JSON files with timestamp
   - Generated blog post data
   - Content metadata
   - Publication status

**Retention**: Artifacts are kept for 30 days.

## Usage Examples

### Example 1: Manual File Sync
1. Go to [Actions → File Management and Knowledge Base Sync](../../actions/workflows/file-management.yml)
2. Click "Run workflow"
3. Select `sync-files` operation
4. Select `production` environment
5. Click "Run workflow"

### Example 2: Generate Blog Posts
1. Go to [Actions → File Management and Knowledge Base Sync](../../actions/workflows/file-management.yml)
2. Click "Run workflow"
3. Select `generate-blog-posts` operation
4. Select `production` environment
5. Click "Run workflow"

### Example 3: Complete Sync and Generation
1. Go to [Actions → File Management and Knowledge Base Sync](../../actions/workflows/file-management.yml)
2. Click "Run workflow"
3. Select `full-sync` operation (default)
4. Select `production` environment
5. Click "Run workflow"

## Viewing Results

After a workflow run:

1. **Check the Summary**: Click on the workflow run to see the summary with operation status
2. **Download Artifacts**: Scroll to the bottom and download the report artifacts
3. **Review Logs**: Click on individual steps to see detailed logs

## Integration with cloudcurio.cc

The workflow is designed to work seamlessly with cloudcurio.cc:

### File Management
- All files uploaded through the microfeed admin dashboard are tracked
- Files are organized by category (images, audio, video, documents)
- Each file gets a unique identifier for the knowledge base

### Knowledge Base
- File manifests provide structured data about all content
- Metadata includes file type, size, upload date, and associated items
- Can be consumed by other systems for search and indexing

### Blog Post Generation
- Automatically creates blog post metadata from microfeed items
- Includes title, description, content, and media attachments
- Structured format ready for website integration

## Customization

To customize the workflow for your needs:

1. **Edit the workflow file**: `.github/workflows/file-management.yml`
2. **Modify operations**: Add custom scripts in the workflow steps
3. **Extend outputs**: Add additional artifact generation
4. **Add notifications**: Integrate with Slack, Discord, or email

## Troubleshooting

### Common Issues

**Problem**: Workflow fails with authentication error
- **Solution**: Check that all secrets are correctly configured in repository settings

**Problem**: No files are being synced
- **Solution**: Verify R2 bucket configuration and that media files exist

**Problem**: Blog posts not generating
- **Solution**: Ensure microfeed items exist and have proper metadata

### Getting Help

If you encounter issues:
1. Check the workflow logs for error messages
2. Review the [main README](../README.md) for setup instructions
3. Verify all secrets are configured correctly
4. Check Cloudflare dashboard for API token permissions

## Security Considerations

- Never commit secrets to the repository
- Use GitHub environments for production/preview separation
- Regularly rotate API tokens and access keys
- Review workflow permissions periodically

## Future Enhancements

Potential improvements:
- [ ] AI-powered blog post content generation
- [ ] Automatic image optimization
- [ ] Multi-language support
- [ ] Integration with external CMS platforms
- [ ] Advanced search indexing
- [ ] Content recommendation engine

## Related Documentation

- [Main README](../README.md) - Setup and installation
- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages/)
- [Cloudflare R2 Docs](https://developers.cloudflare.com/r2/)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
