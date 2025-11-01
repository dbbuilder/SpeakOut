# Security Policy

## Supported Versions

We release patches for security vulnerabilities in the following versions:

| Version | Supported          |
| ------- | ------------------ |
| 1.x.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

**Please do NOT report security vulnerabilities through public GitHub issues.**

### How to Report

If you discover a security vulnerability, please follow these steps:

1. **Email**: Send details to security@[your-domain].com
   - DO NOT open a public issue
   - DO NOT discuss publicly until fixed

2. **Include**:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)
   - Your contact information

3. **Response Time**:
   - Initial response: Within 48 hours
   - Status update: Within 1 week
   - Resolution timeline: Depends on severity

### What to Expect

1. **Acknowledgment**: We'll confirm receipt within 48 hours
2. **Assessment**: We'll assess the severity and impact
3. **Communication**: We'll keep you updated on progress
4. **Fix**: We'll develop and test a patch
5. **Disclosure**: We'll coordinate disclosure timing with you
6. **Credit**: We'll credit you (if desired) in release notes

## Security Best Practices

### For Users

- **Keep Updated**: Always use the latest version
- **Secure Credentials**: Use strong passwords
- **HTTPS Only**: Never use HTTP in production
- **Review Permissions**: Only grant necessary camera/storage permissions
- **Protect Data**: Don't share sensitive screenshots or logs

### For Developers

- **Dependencies**: Keep all dependencies updated
- **Secrets**: Never commit secrets to Git
- **Code Review**: All PRs must be reviewed
- **Input Validation**: Validate all user input
- **SQL Injection**: Use parameterized queries
- **XSS Prevention**: Sanitize all output
- **Authentication**: Use JWT with secure tokens
- **Rate Limiting**: Implement on all endpoints

## Security Features

### Data Protection

- **Encryption in Transit**: HTTPS/TLS 1.3 required
- **Encryption at Rest**: Azure Storage encryption enabled
- **Temporary Storage**: Images auto-deleted after 24 hours
- **No Face Data**: Facial recognition opt-in only
- **User Control**: Export and delete all data anytime

### Authentication & Authorization

- **JWT Tokens**: Short-lived access tokens (30 min)
- **Refresh Tokens**: Secure refresh mechanism
- **Password Hashing**: bcrypt with salt
- **Rate Limiting**: 100 requests/min per user
- **Session Management**: Secure session handling

### Azure Security

- **Key Vault**: All secrets stored in Azure Key Vault
- **Managed Identity**: No hardcoded credentials
- **Network Security**: Firewall rules configured
- **Monitoring**: Application Insights enabled
- **Compliance**: COPPA and GDPR compliant

### Code Security

- **Dependency Scanning**: Dependabot enabled
- **SAST**: Static analysis in CI/CD
- **Secrets Scanning**: GitHub secrets scanning
- **Code Review**: Mandatory for all changes

## Known Security Considerations

### Image Upload

- **File Type Validation**: Only JPEG, PNG allowed
- **Size Limits**: Max 10MB per image
- **Virus Scanning**: Recommended for production
- **Temporary Storage**: 24-hour auto-deletion

### Computer Vision API

- **Rate Limits**: Azure CV API rate limited
- **Data Retention**: Images processed, not stored by Azure
- **Privacy**: No Microsoft data retention

### User Data

- **Minimal Collection**: Only essential data collected
- **Purpose Limitation**: Data used only for app functionality
- **User Rights**: Export, delete, and access controls
- **COPPA Compliance**: Suitable for users under 13

## Vulnerability Disclosure Policy

We follow **responsible disclosure**:

1. **Private Reporting**: Vulnerabilities reported privately
2. **Investigation**: We investigate and develop fixes
3. **Coordination**: We coordinate disclosure timing
4. **Public Disclosure**: After fix is deployed
5. **Credit**: Reporter credited (if desired)

### Disclosure Timeline

- **Critical**: Fix within 7 days, public disclosure after 14 days
- **High**: Fix within 30 days, public disclosure after 45 days
- **Medium**: Fix within 60 days, public disclosure after 90 days
- **Low**: Fix in next regular release

## Security Updates

Security updates are released as:

- **Patch releases**: 1.0.x for critical/high severity
- **Minor releases**: 1.x.0 for medium severity
- **Major releases**: x.0.0 for breaking security changes

Check [CHANGELOG.md](CHANGELOG.md) for security update notes.

## Security Hall of Fame

We recognize security researchers who responsibly disclose vulnerabilities:

<!-- List will be added as researchers report issues -->

Thank you for helping keep SpeakOut and our users safe!

## Additional Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Azure Security Best Practices](https://docs.microsoft.com/en-us/azure/security/)
- [WCAG Security Considerations](https://www.w3.org/WAI/WCAG21/Understanding/)
- [COPPA Compliance](https://www.ftc.gov/legal-library/browse/rules/childrens-online-privacy-protection-rule-coppa)

## Contact

- **Security Email**: security@[your-domain].com
- **PGP Key**: [Link to PGP public key]
- **Response Time**: 48 hours

---

**Last Updated**: 2025-10-31
