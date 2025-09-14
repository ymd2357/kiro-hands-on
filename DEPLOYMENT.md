# Deployment Documentation

## Overview

This repository uses GitHub Actions to automatically deploy release content when new GitHub releases are published. The deployment workflow is designed to handle static documentation content and deploy it to a target FTP server.

## Workflow Triggers

The deployment workflow (`release-deploy.yml`) is triggered by:

1. **Automatic**: When a new GitHub release is published
2. **Manual**: Via workflow dispatch with configurable options

## Required GitHub Repository Secrets

The following secrets must be configured in the repository settings (Settings > Secrets and variables > Actions):

| Secret Name | Description | Example |
|-------------|-------------|---------|
| `FTP_SERVER` | FTP server hostname or IP address | `ftp.example.com` |
| `FTP_USERNAME` | FTP username for authentication | `deploy_user` |
| `FTP_PASSWORD` | FTP password for authentication | `secure_password` |
| `FTP_SERVER_DIR` | Target directory on FTP server | `/public_html/kiro-hands-on/` |

## Deployment Process

### 1. Build Phase
- Checks out the repository code
- Sets up Node.js environment
- Installs npm dependencies
- Runs `npm run build:readme` to generate complete documentation
- Prepares deployment content including:
  - `README.md` (main documentation)
  - `README.full.md` (generated complete documentation)
  - `package.json` (project metadata)
  - `docs/` directory (detailed learning materials)
  - `.vscode/` settings (for development consistency)

### 2. Validation Phase
- Verifies all required files are present
- Validates that `README.full.md` was built correctly
- Confirms deployment content is ready

### 3. Deployment Phase
- **Dry Run**: Always performed first to preview changes
- **Production Deployment**: Uploads content to FTP server
- **Post-deployment Verification**: Confirms successful deployment

## Deployment Modes

### Automatic Deployment (Release Trigger)
When a new GitHub release is published:
1. Workflow automatically triggers
2. Performs dry run to validate content
3. Proceeds with production deployment
4. Provides deployment confirmation

### Manual Deployment (Workflow Dispatch)
Manual deployment options:
- **Dry Run**: Preview deployment without making changes
- **Deploy**: Perform actual deployment to production
- **Release Tag**: Specify which release to deploy (optional)

## File Exclusions

The following files/directories are excluded from deployment:
- `.git*` (Git metadata)
- `node_modules/` (npm dependencies)
- `.DS_Store` (macOS system files)
- `Thumbs.db` (Windows system files)

## Rollback Strategy

### Immediate Rollback Options
1. **Re-deploy Previous Release**: Use workflow dispatch to deploy a previous release tag
2. **Manual FTP Management**: Direct FTP access to restore previous content
3. **Emergency Rollback**: Create a new release with previous content

### Rollback Process
1. Identify the last known good release tag
2. Use workflow dispatch with the previous release tag
3. Set deploy_mode to 'deploy'
4. Monitor deployment logs for successful completion

## Monitoring and Troubleshooting

### Deployment Status
- Check the Actions tab in GitHub repository
- Review workflow run logs for detailed information
- Monitor deployment notifications in workflow output

### Common Issues and Solutions

#### Build Failures
- **Issue**: `npm run build:readme` fails
- **Solution**: Check package.json scripts and file dependencies

#### FTP Connection Issues
- **Issue**: Cannot connect to FTP server
- **Solution**: Verify FTP_SERVER, FTP_USERNAME, and FTP_PASSWORD secrets

#### Missing Files
- **Issue**: Required files not found during validation
- **Solution**: Ensure all source files are committed to the repository

#### Permission Errors
- **Issue**: FTP upload fails due to permissions
- **Solution**: Verify FTP user has write permissions to FTP_SERVER_DIR

### Debug Mode
To enable verbose logging:
1. The workflow already includes `log-level: verbose` for FTP operations
2. Check the "Pre-deployment validation" step for file verification
3. Review the "Post-deployment verification" step for deployment confirmation

## Security Considerations

### Credential Management
- All sensitive information is stored as GitHub repository secrets
- Secrets are never exposed in workflow logs
- FTP credentials are encrypted and only accessible during deployment

### Access Control
- Production deployments require the `production` environment
- Environment protection rules can be configured for additional security
- Workflow permissions are limited to necessary operations only

### File Security
- No sensitive files are included in deployment
- Build artifacts are automatically cleaned up after deployment
- Deployment content is validated before upload

## Assumptions and Design Decisions

### Technology Choices
- **FTP Deployment**: Chosen based on static content nature and existing patterns from mmark repository
- **Node.js Build Process**: Required for generating complete documentation via `npm run build:readme`
- **GitHub Actions**: Standard CI/CD platform with good integration and security features

### Deployment Strategy
- **Static Content**: Assumes target environment serves static files (HTML, Markdown, JSON)
- **FTP Protocol**: Assumes target server supports FTP for file transfer
- **Directory Structure**: Maintains source repository structure in deployment

### Environment Assumptions
- Target FTP server supports standard FTP protocol
- Deployment directory has appropriate write permissions
- Static file serving capability on target environment

## Maintenance

### Regular Tasks
1. **Secret Rotation**: Periodically update FTP credentials
2. **Workflow Updates**: Keep GitHub Actions versions current
3. **Dependency Updates**: Update npm dependencies as needed

### Monitoring
- Review deployment logs regularly
- Monitor for failed deployments
- Verify deployed content accessibility

### Updates
- Test workflow changes in a fork or separate branch
- Use dry-run mode to validate changes before production deployment
- Document any configuration changes in this file

## Support

For issues related to:
- **Workflow Configuration**: Check this documentation and workflow file comments
- **FTP Server Issues**: Contact server administrator
- **GitHub Actions**: Refer to GitHub Actions documentation
- **Build Process**: Review package.json and source files

## Version History

- **v1.0**: Initial release deployment workflow
  - FTP-based deployment
  - Automatic release triggers
  - Manual deployment options
  - Comprehensive validation and error handling
