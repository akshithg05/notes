![[namastedev.com_learn_namaste-frontend-system-design_fixing.png]]
## What Does Fixing Bugs Involve?
Fixing bugs is not just about writing a quick fix.  
It involves a structured process to:
- Identify the most critical issues
- Debug effectively
- Mitigate impact quickly
- Prevent similar issues in the future

---

## 1. Prioritization
We cannot fix everything at once. Bugs are prioritized based on severity and impact.

Common priority levels:
- P0 – Critical  
  - App down
  - Core flows broken
  - Revenue-impacting issues
- P1 – High  
  - Major feature broken
  - Large user impact
- P2 – Medium  
  - Partial feature issues
  - Workarounds exist
- P3 – Low  
  - Minor UI bugs
  - Cosmetic issues

Prioritization helps teams focus on what matters most.

---

## 2. Debugging
Good debugging skills are what make a strong developer.

### Source Maps
- Code shipped to browsers is minified and compressed
- Source maps map minified code back to original source code
- Helps identify:
  - Exact file
  - Line number
  - Root cause of the issue

Without source maps, debugging production issues is extremely difficult.

---

### Session Replay
Session replay tools show exactly what the user experienced.

Examples:
- Microsoft Clarity
- LogRocket

Benefits:
- Reproduce user actions
- See UI behavior
- Identify where the app broke
- Debug issues that cannot be reproduced locally

---

## 3. Mitigation
Mitigation focuses on **reducing user impact immediately**.

### Rollback
- Revert to a previous stable build
- Fastest way to stop bleeding
- Used for critical production issues

### Hotfix
- Small targeted fix
- Avoids full redeploy
- Fixes only the affected functionality

### Selective Deploy (SSD)
- Deploy fixes to specific features or services
- Limits blast radius
- Reduces risk

---

## 4. Prevention
Prevention ensures the same issue does not happen again.

### Testing
- Unit test cases
- Integration tests
- End-to-end tests

### Code Quality
- Linting
- Type checking (TypeScript)

### Process Improvements
- PR review process
- Peer reviews
- Automated CI checks

### Safety Mechanisms
- Rate limiting
- Security scans
- Performance scans

Prevention reduces long-term defect rates and improves system reliability.

---

## Key Takeaway
Bug fixing is a cycle of prioritization, debugging, mitigation, and prevention that ensures system stability and developer efficiency.

---

## One-Line Interview Summary
Fixing bugs involves prioritizing issues, debugging with tools like source maps and session replay, mitigating impact quickly, and preventing future defects through testing and process improvements.
