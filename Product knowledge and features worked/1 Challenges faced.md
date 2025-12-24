## Scale issues of 10k Servers

## ⭐ **STAR Answer**

### **Situation**

While working on the frontend of HPE’s Compute Ops Management (COM) tool, one of our enterprise customers, Booking.com, onboarded **over 10,000 servers**. The application had not been scale-tested for such a large environment, which led to API failures and significant UI performance issues.
### **Task**

My responsibility was to **identify the root cause**, reproduce the issue reliably, and ensure the UI remained performant and usable at that scale without negatively impacting the customer experience.
### **Action**

- Used our internal **mock server platform** to simulate **10,000+ servers** with real API responses, allowing us to reproduce the issue in a controlled environment.
- Identified that large payloads and heavy synchronous rendering were causing API timeouts and UI lag.
- Implemented **pagination** and enforced a **maximum server count** to prevent extreme loads.
- Added **lazy loading** and **infinite scrolling** to reduce initial data fetch and DOM rendering.
- Introduced **user warnings and notifications** when server counts exceeded 10k to set expectations and guide usage.

### **Result**

These changes significantly **improved UI responsiveness**, reduced API failures, and stabilized the application even at large scale. The customer validated the improvements, and the platform became better prepared for future high-scale enterprise deployments.expected.”**


# 2. Talk about some security features of COM

- How we implemented some security CI pipelines, dependabot, secret scanner for leaking secrets, regular dependency auditing.

# 3. Talk about testing

- Initially test case coverage of COM UI was at 75% when we wrote test cases manually without using any kind of AI tools and it used to take addition 2-3 days effort per feature to write these. Once we started embracing AI tools, we could write tests within the development estimate as well as cover a higher % of code.
- We wrote unit and isolated test cases using jest for all components and aimed at 95% test coverage. We reached approximately 93% test coverage with the help of Co-pilot and other AI tools.