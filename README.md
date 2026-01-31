# SecureAPI Documentation

This repository contains the product documentation for the SecureAPI platform.

## 📚 Documentation

The documentation is automatically published to GitHub Pages:
- **Live Documentation:** https://rasheed-fabrichq.github.io/fabric-auto-release-notes-docs/

## 🔄 Auto-Update System

This repository is automatically updated when code changes are merged in the main codebase:
1. Code PR merged in [fabric-auto-release-note-creator-and-document-updater](https://github.com/rasheed-fabrichq/fabric-auto-release-note-creator-and-document-updater)
2. GitHub Action analyzes changes using Claude AI
3. Documentation update PR is automatically created here
4. Product manager reviews and merges the updates
5. GitHub Pages publishes the updated documentation

## 📁 Repository Structure

```
docs/
├── index.md              # Documentation home page
├── authentication.md     # Authentication guide
└── billing.md           # Billing and pricing guide
```

## 🚀 Local Development

To preview documentation locally:

```bash
# Clone the repository
git clone https://github.com/rasheed-fabrichq/fabric-auto-release-notes-docs.git
cd fabric-auto-release-notes-docs

# View the markdown files in your editor
# Or use a markdown previewer
```

## 🤖 Automated Updates

Documentation updates are managed by:
- **Source:** Changes detected in code repository
- **Analysis:** Claude AI compares code changes with current docs
- **Review:** Human approval required before publishing
- **Publishing:** GitHub Pages auto-deploys on merge to main
