# HowToMgr Project Documentation for Claude

## Project Overview

HowToMgr is a comprehensive collection of installation and configuration guides for free and open-source software (FOSS) infrastructure services. The project provides standardized, high-quality documentation for system administrators and developers across multiple operating systems.

### Core Mission
- Document FOSS alternatives to proprietary software
- Provide production-ready installation guides
- Maintain consistent, testable documentation
- Support multiple operating systems and architectures

## Project Structure

```
/root/Projects/github/howtomgr/
├── .claude/                    # Claude AI documentation and context
│   ├── CLAUDE.md              # This file - project documentation
│   └── README.md              # Claude-specific project notes
├── .github/                   # GitHub workflows and templates
├── howtomgr.github.io/        # Frontend website repository (submodule)
├── SPEC.md                    # SPEC 2.0 documentation standard
├── TEMPLATE.md                # Basic guide template
├── [tool-name]/               # Individual tool repositories (574 total)
│   ├── README.md              # SPEC 2.0 compliant installation guide
│   ├── META.json              # Metadata for frontend integration
│   ├── LICENSE.md             # MIT license for the guide
│   └── .git/                  # Individual git repository
└── run-all-batches.sh         # Batch processing script
```

## SPEC 2.0 Standard

All guides MUST follow SPEC 2.0 format with exactly 16 sections:

1. **Title and Introduction** - Brief description with FOSS alternatives
2. **Prerequisites** - Hardware, software, network requirements
3. **Installation** - Multi-OS installation procedures
4. **Configuration** - Initial setup and basic configuration
5. **Service Management** - systemd, OpenRC, launchd, Windows services
6. **Troubleshooting** - Common issues and solutions
7. **Security Considerations** - Firewall, SSL/TLS, authentication
8. **Performance Tuning** - Optimization and scaling
9. **Backup and Restore** - Data protection procedures
10. **System Requirements** - Detailed hardware specifications
11. **Support** - Official resources and community links
12. **Contributing** - How to contribute to the project
13. **License** - Software licensing information
14. **Acknowledgments** - Credits and recognition
15. **Version History** - Release notes and changelog
16. **Appendices** - Additional resources, examples, references

### Required Operating System Coverage

Each guide must include installation instructions for:
- **RHEL-based**: RHEL 8/9, CentOS Stream, Rocky Linux, AlmaLinux, Fedora
- **Debian-based**: Debian 11/12, Ubuntu 20.04/22.04/24.04 LTS
- **Arch-based**: Arch Linux, Manjaro, EndeavourOS
- **Alpine Linux**: 3.18+ (for containerization)
- **SUSE-based**: openSUSE Leap/Tumbleweed, SLES (where applicable)
- **Secondary**: macOS, FreeBSD, Windows (where supported)

## Repository Standards

### META.json Structure
Each repository contains a META.json file with standardized metadata:

```json
{
  "category": "primary-category",
  "subcategory": "specific-subcategory", 
  "name": "repository-name",
  "title": "Human Readable Title",
  "description": "Detailed description mentioning FOSS alternatives",
  "dependencies": ["package1", "package2"],
  "default_ports": [80, 443],
  "supported_os": ["rhel", "debian", "arch", "alpine"],
  "difficulty_level": "beginner|intermediate|advanced",
  "estimated_setup_time": "30-60 minutes",
  "installation_methods": ["package-manager", "source"],
  "license": "Software License",
  "spec_version": "2.0",
  "maintenance_status": "active|deprecated",
  "created_date": "2025-09-16T00:00:00.000000",
  "last_updated": "2025-09-16T00:00:00.000000",
  "features": ["multi-os-support", "security-hardening"],
  "tags": ["keyword1", "keyword2"],
  "repository_url": "https://github.com/howtomgr/tool-name",
  "documentation_url": "https://howtomgr.github.io/category/tool-name",
  "website_url": "https://howtomgr.github.io/category/tool-name",
  "guide_path": "/category/tool-name",
  "version": "1.0.0"
}
```

### Categories and Subcategories

#### Primary Categories:
- **web-servers**: nginx, apache, caddy
- **databases**: postgresql, mysql, mongodb, redis
- **monitoring**: prometheus, grafana, nagios, zabbix
- **virtualization**: libvirt, qemu, lxc, docker
- **networking**: openvpn, wireguard, haproxy, traefik
- **security**: fail2ban, certbot, vault, keycloak
- **communication**: matrix, xmpp, email-servers
- **development-tools**: git, jenkins, gitlab, vscode-server
- **file-storage**: nextcloud, samba, nfs, minio
- **media**: plex, jellyfin, kodi, subsonic
- **automation**: ansible, terraform, puppet, saltstack
- **mail**: postfix, dovecot, roundcube, rainloop
- **cms**: wordpress, drupal, ghost, strapi
- **operating-systems**: debian, ubuntu, arch, alpine
- **surveillance**: shinobi, zoneminder, bluecherry
- **home-automation**: home-assistant, openhab, domoticz
- **backup**: restic, borgbackup, bacula, amanda

## Common Commands and Patterns

### Repository Management

```bash
# Navigate to project root
cd /root/Projects/github/howtomgr

# List all repositories
ls -1 | grep -v "\." | wc -l  # Count repos (should be 574)

# Find non-compliant repositories  
find . -maxdepth 2 -name "README.md" -exec grep -L "## Table of Contents" {} \;

# Check SPEC 2.0 compliance
grep -r "## 16\. Appendices" */README.md | wc -l

# Update a specific repository
cd /root/Projects/github/howtomgr/[tool-name]
# Edit README.md and META.json as needed
```

### Batch Operations

```bash
# Process repositories in batches
./run-all-batches.sh

# Process specific batch ranges
./run-batches-21-40.sh

# Check for missing META.json files
for dir in */; do
  if [ ! -f "$dir/META.json" ]; then
    echo "Missing META.json: $dir"
  fi
done
```

### Quality Assurance

```bash
# Verify all guides have required sections
for guide in */README.md; do
  if ! grep -q "## 1\. Prerequisites" "$guide"; then
    echo "Missing Prerequisites: $guide"
  fi
done

# Check for proper Table of Contents
grep -L "## Table of Contents" */README.md

# Validate JSON syntax
for json in */META.json; do
  if ! jq . "$json" >/dev/null 2>&1; then
    echo "Invalid JSON: $json"
  fi
done
```

## Content Standards

### Writing Guidelines
- **Target Audience**: Intermediate Linux administrators
- **Tone**: Professional, concise, instructional
- **Code Blocks**: Always include comments explaining purpose
- **Security**: Emphasize security-first configurations
- **Testing**: All commands must be tested and functional

### Security Requirements
Every guide MUST include:
- Non-root user creation and usage
- Proper file permissions (principle of least privilege)
- Firewall configuration for all major systems
- SSL/TLS setup with modern cipher suites
- Authentication configuration (no default passwords)
- SELinux/AppArmor contexts where applicable

### Code Standards
```bash
# Example format - always include explanatory comments
# Update package lists
sudo apt update

# Install required packages
sudo apt install -y package-name

# Expected result: package is now installed and ready to configure
```

## Frontend Integration

The howtomgr.github.io frontend automatically:
- Fetches repository list via GitHub API
- Renders README.md files with syntax highlighting
- Uses META.json for categorization and search
- Provides responsive design (90% width ≥720px, 98% <720px)
- Supports Dracula dark theme and light theme
- Generates automatic table of contents
- Includes copy buttons for code blocks

## Project History and Status

### Current Status (September 2025)
- **574 repositories** total
- **100% SPEC 2.0 compliance** achieved
- **All major categories** represented
- **Multi-OS support** for all guides
- **Production-ready** configurations

### Major Milestones
- **2024**: Initial project creation and basic guides
- **Early 2025**: SPEC 2.0 development and standardization
- **September 2025**: Complete SPEC 2.0 migration and Claude integration
- **Current**: Maintenance and expansion phase

### Recent Changes
- Migrated code_server content to vscode-server repository
- Updated final 7 repositories to SPEC 2.0 compliance
- Standardized all META.json files with proper categorization
- Implemented comprehensive quality assurance processes

## Working with Claude

### Common Tasks

1. **Adding New Software Guide**:
   - Research the software and identify FOSS nature
   - Create new repository directory
   - Generate SPEC 2.0 compliant README.md
   - Create accurate META.json with proper categorization
   - Test installation procedures on multiple OS

2. **Updating Existing Guide**:
   - Read current README.md and META.json
   - Identify what needs updating (versions, procedures, security)
   - Update content following SPEC 2.0 format
   - Verify all 16 sections are present and complete
   - Update META.json timestamps and version

3. **Quality Assurance**:
   - Check for SPEC 2.0 compliance across all repositories
   - Validate META.json syntax and completeness
   - Ensure consistent categorization
   - Verify security best practices are included

4. **Batch Operations**:
   - Process multiple repositories efficiently
   - Use provided batch scripts when available
   - Maintain consistency across similar tools
   - Update metadata systematically

### Best Practices for Claude

1. **Always read existing files first** before making changes
2. **Use absolute paths** when referencing files
3. **Follow SPEC 2.0 format exactly** - all 16 sections required
4. **Test commands** and verify they work as documented
5. **Update META.json** whenever README.md changes
6. **Maintain security focus** in all configurations
7. **Include FOSS alternatives** for proprietary software
8. **Use consistent formatting** and naming conventions

### Commands to Remember

```bash
# Test package installations
sudo apt update && sudo apt install -y package-name  # Debian/Ubuntu
sudo dnf install -y package-name                     # RHEL/Fedora
sudo pacman -S package-name                          # Arch
apk add --no-cache package-name                      # Alpine

# Service management
sudo systemctl enable --now service-name            # systemd
sudo rc-update add service-name default             # OpenRC
```

### File Paths to Remember

- **Project Root**: `/root/Projects/github/howtomgr/`
- **SPEC Document**: `/root/Projects/github/howtomgr/SPEC.md`
- **Template**: `/root/Projects/github/howtomgr/TEMPLATE.md`
- **Individual Guides**: `/root/Projects/github/howtomgr/[tool-name]/README.md`
- **Metadata**: `/root/Projects/github/howtomgr/[tool-name]/META.json`

## Excluded Content

### Never Include
- Docker/Kubernetes as primary installation method
- Proprietary software without FOSS alternatives mentioned
- Software requiring paid licenses or subscriptions
- Deprecated or unmaintained projects (>2 years no updates)
- Beta/alpha software (unless no stable release exists)
- Personal opinions or subjective preferences
- Hardcoded passwords or sensitive information

### Exceptions
- Docker may be mentioned as alternative installation method
- WSL2 acceptable for Windows installations
- Source compilation when no packages available
- Enterprise software if widely used (with FOSS alternatives listed)

## Maintenance Schedule

### Regular Tasks
- **Monthly**: Check for broken links and outdated versions
- **Quarterly**: Review software updates and security patches
- **Bi-annually**: Full guide review and testing
- **As needed**: Security updates within 48 hours

### Quality Checks
- SPEC 2.0 compliance verification
- META.json validation and consistency
- Link checking and URL validation
- Security review of configurations
- Testing on supported operating systems

## Contact and Resources

### Project Resources
- **GitHub**: https://github.com/howtomgr
- **Website**: https://howtomgr.github.io
- **Specification**: SPEC.md in project root

### Key Principles
1. **FOSS First**: Always prioritize free and open-source software
2. **Production Ready**: All guides must be suitable for production use
3. **Security Focused**: Security is never optional
4. **Multi-Platform**: Support all major operating systems
5. **Community Driven**: Encourage contributions and feedback
6. **Quality Assured**: Every guide must be tested and verified
7. **Consistently Formatted**: Follow SPEC 2.0 without deviation

---

This documentation should be updated whenever significant changes are made to the project structure, standards, or processes. Always ensure Claude has access to the most current version of this file when working on HowToMgr tasks.

Last Updated: September 16, 2025
Version: 1.0.0