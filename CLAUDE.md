# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a **MkDocs-based workshop documentation repository** for FortiAppSec Cloud training materials. It's built on the 40docs workshop template system and automatically deploys to GitHub Pages using GitHub Actions.

## Architecture

### Core Components
- **MkDocs**: Static site generator with Material theme
- **40docs Theme**: Custom workshop theme (`theme/` directory, cloned during build)
- **GitHub Actions**: Automated build and deployment pipeline
- **GitHub Pages**: Hosting platform for the generated documentation site

### Content Structure
```
docs/
├── index.md                    # Workshop landing page (with custom CSS)
└── Hands-on-Labs/
    ├── index.md               # Labs overview (FortiAppSec introduction)
    ├── 00-login.md            # Login instructions
    ├── 01-add-application.md  # Adding applications
    ├── 02-enable-features.md  # Enabling security features
    ├── 03-vulnerability-scan.md # Vulnerability scanning
    ├── 04-attack.md           # Attack simulation
    └── *.png                  # Screenshots and images
```

### Key Configuration Files
- `mkdocs.yml`: Main configuration with theme settings, plugins, and markdown extensions
- `requirements.txt`: Python dependencies for MkDocs and plugins
- `.github/workflows/deploy.yml`: CI/CD pipeline for GitHub Pages deployment

## Development Commands

### Local Development Setup
```bash
# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Clone the workshop theme (required for local preview)
git clone https://github.com/40docs/workshop_theme_template.git theme

# Start development server
mkdocs serve
```

### Build and Deploy
```bash
# Build static site locally
mkdocs build --verbose

# Deploy (automatic on push to main branch)
git push origin main
```

### Content Validation
```bash
# Check for broken links (if mkdocs-linkcheck plugin added)
mkdocs build --strict

# Validate markdown syntax
markdownlint docs/**/*.md
```

## Workshop Content Architecture

### Content Flow
1. **Login Process** (`00-login.md`): Authentication through Fortinet support portal
2. **Application Setup** (`01-add-application.md`): Adding applications to FortiAppSec
3. **Feature Configuration** (`02-enable-features.md`): Enabling security features
4. **Security Testing** (`03-vulnerability-scan.md`): Running vulnerability scans
5. **Attack Simulation** (`04-attack.md`): Testing security responses

### Image Management
- All workshop images stored in `docs/Hands-on-Labs/` alongside markdown files
- Images are referenced relatively (e.g., `![Login](login.png)`)
- glightbox plugin enables click-to-zoom functionality

### Theme Integration
- Workshop uses Material Design with dark theme (`scheme: slate`)
- Custom 40docs workshop theme provides branding and layout
- Theme is automatically cloned during GitHub Actions build process
- Local development requires manual theme cloning

## Deployment Architecture

### GitHub Actions Workflow
1. **Trigger**: Push to main branch, PR, or manual dispatch
2. **Build Process**:
   - Setup Python environment
   - Install dependencies from `requirements.txt`
   - Clone 40docs workshop theme
   - Build MkDocs site with verbose output
   - Upload Pages artifact
3. **Deploy Process**:
   - Deploy to GitHub Pages (main branch only)
   - Site available at configured URL

### Site Configuration
- **Site URL**: `https://40docs.github.io/workshop_fortiappsec/`
- **Theme**: Material with 40docs workshop customizations
- **Features**: Search, code highlighting, tabbed content, Mermaid diagrams
- **Plugins**: glightbox (image zoom), search

## Content Guidelines

### Markdown Features
- **Admonitions**: Use `!!! note`, `!!! warning`, `!!! tip` for callouts
- **Code Blocks**: Syntax highlighting with language specification
- **Tabbed Content**: Use `=== "Tab Name"` syntax
- **Mermaid Diagrams**: Support for flowcharts and diagrams
- **Image Lightbox**: Automatic zoom functionality on images

### File Naming Convention
- Use numbered prefixes for sequential labs: `00-`, `01-`, `02-`, etc.
- Descriptive names after prefix: `01-add-application.md`
- Images follow descriptive naming: `new-application-1.png`

### Repository-Specific Notes
- This is specifically a **FortiAppSec Cloud workshop** repository
- Content focuses on hands-on security application testing and configuration
- Images are workflow screenshots showing the FortiAppSec interface
- All labs build upon each other in sequence (login → setup → testing → attack simulation)