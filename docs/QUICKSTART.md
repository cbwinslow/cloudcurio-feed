# Quick Start Guide: File Management Workflow

This guide will help you get started with the cloudcurio.cc file management workflow in just a few minutes.

## Prerequisites

Before using the workflow, ensure you have:

- ✅ A cloudcurio-feed instance deployed to Cloudflare Pages
- ✅ All required secrets configured in GitHub repository settings
- ✅ At least one item published in your microfeed instance

If you haven't set up your instance yet, follow the [main installation guide](../README.md#-installation).

## Step 1: Verify Your Setup

1. Go to your repository's [Settings → Secrets → Actions](../../settings/secrets/actions)
2. Confirm these secrets are present:
   - `CLOUDFLARE_API_TOKEN`
   - `CLOUDFLARE_ACCOUNT_ID`
   - `CLOUDFLARE_PROJECT_NAME`
   - `R2_ACCESS_KEY_ID`
   - `R2_SECRET_ACCESS_KEY`
   - `R2_PUBLIC_BUCKET` (optional)

## Step 2: Run Your First Sync

1. Navigate to [Actions → File Management and Knowledge Base Sync](../../actions/workflows/file-management.yml)
2. Click the **"Run workflow"** button
3. Keep the default settings:
   - Operation: `full-sync`
   - Environment: `production`
4. Click **"Run workflow"** to start

## Step 3: Monitor the Workflow

Watch the workflow progress:

1. Click on the running workflow in the Actions tab
2. Observe the steps:
   - ✅ Checkout repository
   - ✅ Setup Node.js
   - ✅ Install dependencies
   - ✅ Sync files to knowledge base
   - ✅ Generate blog posts
   - ✅ Upload artifacts

The workflow typically completes in 2-3 minutes.

## Step 4: Review the Results

After the workflow completes:

1. Click on the workflow run
2. Scroll down to the **"Artifacts"** section
3. Download the `file-management-report-*` artifact
4. Extract and review:
   - `file-manifest-*.json` - List of all synced files
   - `blog-metadata-*.json` - Generated blog post data

## Step 5: View the Summary

Check the workflow summary for a quick overview:

- Operation performed
- Environment used
- Timestamp
- Status of completed operations

## What's Next?

### Automatic Syncs

The workflow will now automatically run:

- **Daily at 2:00 AM UTC** - Scheduled sync
- **When you push to main** - On content changes

You don't need to manually trigger it unless you want an immediate sync.

### Using the Generated Data

The workflow outputs JSON files that you can use to:

1. **Build a search index** - Use file manifests for search functionality
2. **Display content** - Show blog posts on your website
3. **Track changes** - Monitor what files have been added or modified
4. **Generate reports** - Analyze your content library

### Customizing Operations

Instead of `full-sync`, you can run specific operations:

- **`sync-files`** - Only sync files, skip blog generation
- **`generate-blog-posts`** - Only generate blog posts, skip file sync

## Troubleshooting

### Workflow Failed

**Check the logs:**
1. Click on the failed workflow run
2. Click on the failed step
3. Review the error message

**Common issues:**
- Missing or invalid secrets → Check repository settings
- R2 bucket not found → Verify `R2_PUBLIC_BUCKET` configuration
- API token expired → Generate a new Cloudflare API token

### No Files Found

**Possible causes:**
- No content published in microfeed yet
- R2 bucket is empty
- Wrong bucket name in configuration

**Solution:**
1. Log into your microfeed admin dashboard
2. Upload some content
3. Run the workflow again

### Need Help?

- 📖 Read the [detailed documentation](FILE_MANAGEMENT_WORKFLOW.md)
- 🐛 Check existing [GitHub issues](../../issues)
- 💬 Create a [new issue](../../issues/new) for help

## Tips for Success

1. **Start Small**: Run a manual sync first to verify everything works
2. **Check Artifacts**: Always review the generated JSON files
3. **Monitor Scheduled Runs**: Keep an eye on daily syncs for any issues
4. **Keep Secrets Updated**: Rotate API tokens and keys regularly
5. **Document Custom Changes**: If you modify the workflow, document your changes

## Example Use Cases

### Use Case 1: Building a Blog
1. Create blog posts in microfeed admin dashboard
2. Run workflow with `generate-blog-posts` operation
3. Download the blog metadata artifact
4. Use the JSON data to populate your website

### Use Case 2: Content Search
1. Upload various media files through microfeed
2. Run workflow with `sync-files` operation
3. Download the file manifest artifact
4. Build a search index from the manifest data

### Use Case 3: Daily Content Updates
1. Set up the workflow (already done!)
2. Let it run automatically every day
3. Your knowledge base stays synchronized automatically
4. Focus on creating content, not managing infrastructure

## Next Steps

- ✅ You've completed the quick start!
- 📚 Explore the [full documentation](FILE_MANAGEMENT_WORKFLOW.md)
- 🚀 Start publishing content and let the workflow handle the rest
- 🎯 Customize the workflow for your specific needs

---

**Questions?** Check the [FAQ section](FILE_MANAGEMENT_WORKFLOW.md#troubleshooting) or create an issue.
