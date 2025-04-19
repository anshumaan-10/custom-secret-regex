```markdown
# 🔐 Search for All Leaked Keys & Secrets Using One Regex

This repository offers a **comprehensive and extensible collection of regular expressions** to detect leaked secrets, credentials, tokens, and sensitive data in codebases or text files.

Use it for:
- Static secret scanning
- Security automation
- CI/CD pipeline integration
- Secure coding practices

---

## 📦 Features

- 100+ ready-to-use regex patterns
- Detects secrets across major cloud and SaaS providers
- Supports API keys, OAuth tokens, JWTs, credentials, private keys, and more
- Designed for use in SAST tools, CLI scans, and IDE integrations

---

## 🔍 Complete Regex Patterns Collection

### 🔑 API Keys & Tokens

| Provider         | Regex Pattern                                          | Description                    |
|------------------|--------------------------------------------------------|--------------------------------|
| Google API Key   | `AIza[0-9A-Za-z-_]{35}`                                | Google Cloud API Key           |
| Google reCAPTCHA | `6L[0-9A-Za-z-_]{38}|6[0-9a-zA-Z_-]{39}`               | reCAPTCHA site/secret keys     |
| Google OAuth     | `ya29\.[0-9A-Za-z\-_]+`                                | Google OAuth 2.0 token         |
| Firebase Key     | `AAA[A-Za-z0-9_-]{7}:[A-Za-z0-9_-]{140}`               | Firebase Cloud Messaging key   |
| AWS Access Key   | `A[SK]IA[0-9A-Z]{16}`                                  | AWS Access Key ID              |
| AWS Secret Key   | `(?i)aws(.{0,20})?(secret|private)?(.{0,20})?['\"][0-9a-zA-Z\/+=]{40}['\"]` | AWS Secret Access Key |
| AWS MWS Token    | `amzn\.mws\.[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}` | Amazon Marketplace token |
| Stripe Key       | `sk_live_[0-9a-zA-Z]{24}`                              | Stripe live secret key         |
| Stripe Pub Key   | `pk_live_[0-9a-zA-Z]{24}`                              | Stripe public key              |
| GitHub Token     | `ghp_[A-Za-z0-9_]{36}`                                 | GitHub personal access token   |
| GitLab Token     | `glpat-[0-9a-zA-Z\-_]{20,}`                            | GitLab personal access token   |
| Slack Token      | `xox[baprs]-([0-9a-zA-Z]{10,48})?`                     | Slack bot, user, and app tokens|
| Twilio API Key   | `SK[0-9a-fA-F]{32}`                                    | Twilio secret key              |
| Twilio SID       | `AC[a-zA-Z0-9_\-]{32}`                                 | Twilio account SID             |
| Mailgun API      | `key-[0-9a-zA-Z]{32}`                                  | Mailgun API key                |
| Heroku API       | `heroku[a-z0-9]{32}`                                   | Heroku API key                 |
| DigitalOcean     | `do[0-9a-z]{32}`                                       | DigitalOcean token             |

---

### 🔐 Authorization Patterns

| Type        | Regex Pattern                                    | Description                     |
|-------------|--------------------------------------------------|---------------------------------|
| Basic Auth  | `basic\s+[a-zA-Z0-9=:_\+\/-]+`                    | HTTP Basic Auth header          |
| Bearer Token| `bearer\s+[a-zA-Z0-9_\-\.=:_\+\/]+`               | Bearer tokens (e.g. OAuth2)     |
| API Key     | `api[_-]?key['"]?\s*[:=]\s*['"]?[A-Za-z0-9_\-]{20,}` | Generic API keys               |

---

### 🔏 Security Tokens & Credentials

| Type            | Pattern                                                   | Description                      |
|------------------|-----------------------------------------------------------|----------------------------------|
| RSA Private Key  | `-----BEGIN RSA PRIVATE KEY-----`                         | PEM-encoded RSA private key      |
| EC Private Key   | `-----BEGIN EC PRIVATE KEY-----`                          | Elliptic Curve private key       |
| DSA Private Key  | `-----BEGIN DSA PRIVATE KEY-----`                         | DSA private key                  |
| PGP Private Key  | `-----BEGIN PGP PRIVATE KEY BLOCK-----`                   | PGP private key block            |
| SSH Private Key  | `-----BEGIN OPENSSH PRIVATE KEY-----`                     | SSH private key (OpenSSH format) |
| JWT              | `eyJ[A-Za-z0-9-_]+\.[A-Za-z0-9-_]+\.[A-Za-z0-9-_.+/=]*`   | JSON Web Token (JWT)             |
| Bearer JWT       | `Bearer [A-Za-z0-9-_]+\.[A-Za-z0-9-_]+\.[A-Za-z0-9-_]+`   | JWT in Authorization header      |

---

### 👤 Common Identifiers

| Type         | Regex Pattern                                                                 | Description           |
|--------------|--------------------------------------------------------------------------------|-----------------------|
| Email        | `[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,7}`                             | Email address         |
| URL          | `https?://(?:www\.)?[a-zA-Z0-9-]+\.[a-zA-Z]{2,}(?:/[\w\-._~:/?#\[\]@!$&'()*+,;=]*)?` | HTTP/HTTPS URLs     |
| IPv4         | `(?<![\d.])((25[0-5]|2[0-4]\d|[01]?\d\d?)\.){3}(25[0-5]|2[0-4]\d|[01]?\d\d?)(?![\d.])` | IP address         |
| UUID         | `[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{4}-[a-fA-F0-9]{12}` | UUID format           |

---

### 🧪 Secret & Password Assignments

| Regex Pattern | Description |
|---------------|-------------|
| `(?:password|passwd|pwd|token|secret)[\s:=]+['"]?([a-zA-Z0-9_\-/+=!@#$%^&*(){}[\]:;'"|<>?.~]{6,})['"]?` | Passwords or secrets in assignment |
| `(?:api[_-]?key|access[_-]?token|secret)[\s:=]+['"]?([a-zA-Z0-9_\-/+=]{20,})['"]?` | Keys/tokens in assignment line |

---

## 📚 Usage Examples

### ✅ JavaScript (Node.js)
```javascript
const patterns = [
    /AIza[0-9A-Za-z-_]{35}/, // Google API
    /sk_live_[0-9a-zA-Z]{24}/, // Stripe
    /-----BEGIN RSA PRIVATE KEY-----/, // RSA Key
    /ghp_[A-Za-z0-9_]{36}/ // GitHub Token
];

function scan(text) {
    return patterns.filter(regex => regex.test(text));
}
```

### ✅ Bash (grep + regex)
```bash
grep -rEi 'AIza[0-9A-Za-z-_]{35}|sk_live_[0-9a-zA-Z]{24}|ghp_[A-Za-z0-9_]{36}' .
```

---

## ⚠️ Known Limitations

- Regex-based detection can yield **false positives**.
- For advanced scanning, integrate with tools like:
  - [TruffleHog](https://github.com/trufflesecurity/trufflehog)
  - [Gitleaks](https://github.com/gitleaks/gitleaks)
  - [Detect Secrets (Yelp)](https://github.com/Yelp/detect-secrets)

---

## 🛠 Recommended Workflow

1. Run this regex collection in a CI step (`pre-push`, `pre-commit`, or nightly scan).
2. Alert developers on secrets via Slack/email.
3. Rotate detected secrets via secret manager.
4. Add validation to prevent pushing secrets using tools like [Husky](https://typicode.github.io/husky/#/) or GitHub Actions.

---

## 🧠 Contributions

Feel free to submit PRs to:
- Add new provider patterns
- Optimize regex performance
- Fix false positives or negatives

---

## 📜 License

MIT License © 2025 Anshumaan Singh

---

## 📬 Contact

**Anshumaan Singh**  
Application Security | DevSecOps  
[📧 anshumaansingh10jan@gmail.com](mailto:anshumaansingh10jan@gmail.com)  
[🔗 LinkedIn](https://linkedin.com/in/anshumaan-singh-6b51b5239)


