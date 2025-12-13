
![[Pasted image 20251213082045.png]]

Modern applications depend heavily on third-party libraries.  
While these libraries are useful, **they should not be trusted blindly**, especially because each library may depend on many other libraries (transitive dependencies).

Below are the five key practices discussed.

---
## 1. Regular Dependency Audits

There is **no shortcut** to dependency auditing.

- Regularly check for vulnerabilities using:
  - `npm audit`
  - `yarn audit`
- During `npm install`, warnings may appear for **old or vulnerable packages**.
- NPM also classifies vulnerabilities by **severity** (low, moderate, high, critical).

### Important Notes
- Do **not** blindly run `npm audit fix`.
- Automatic fixes may:
  - Break functionality
  - Introduce logic issues
- Always review the **audit report** and update dependencies **manually when needed**.

Only fix what is in your control.

---
## 2. Enforcing Dependency Audits

As developers, running audits manually all the time is not practical.  
Auditing should be enforced automatically.

### a. Enable Audit by Default
```bash
npm config set audit true
```
This ensures vulnerabilities are flagged during install/update.

---

### b. Use Dependabot
- Dependabot runs **scheduled scans** (weekly/monthly).
- Automatically raises PRs for:
  - Vulnerable dependencies
  - Outdated packages
- Can be integrated with:
  - GitHub Actions
  - CI pipelines

---

### c. Custom GitHub Actions
- Create your own workflow to run audits:
  - On code push
  - On PR creation
  - Before merge
- Helps enforce security checks consistently.

---
## 3. Dependency & Code Monitoring

Tools like **CodeQL** go beyond dependency scanning.

They:
- Scan **external dependencies**
- Analyze **your own source code**
- Detect:
  - Security vulnerabilities
  - Unsafe coding patterns
  - Compliance issues

This ensures both **dependencies and application code** are secure.

---
## 4. Dependency Locking

Using `package-lock.json` is critical.

- Locks **exact versions** of:
  - Direct dependencies
  - Transitive (nested) dependencies
- Ensures:
  - Same versions across dev, CI, and production
  - No unexpected behavior due to version mismatch
  - Better reproducibility and stability

Without lock files, subtle version differences can introduce bugs or vulnerabilities.

---
## 5. Security & Penetration Testing Tools

In addition to audits, security testing tools help identify deeper issues.

Examples:
- Application vulnerability scanners
- Secret scanners
- **Burp Suite**

These tools help:
- Detect runtime vulnerabilities
- Identify exposed secrets
- Simulate real-world attack scenarios

---
## Summary

Dependency security requires a layered approach:

1. Regular audits (`npm audit`)
2. Enforced scanning (Dependabot, CI)
3. Code + dependency analysis (CodeQL)
4. Locked dependency versions
5. Penetration and vulnerability testing

Third-party code is powerful — but must always be treated as **untrusted by default**.