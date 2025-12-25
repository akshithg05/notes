- Creating code and application is easy, but maintaining it is difficult. Hence we need test cases.
- Testing plays an important role when adding new features
- Front end system testing from a perspective of a developer.

What is covered
![[Pasted image 20251224120537.png]]


- Test driven development  - Takes a lot of time almost 2x time, but 100% code coverage.

### Senior Engineer knowledge

- Know how to write UTs (important for everyone).
- Integration testing.
- Ensuring playwright / cypress and test guidelines are important.
- Feature level, we have to write test cases and keep pipeline.
- Take a call - what is must have test case, what can be ignored and what is not required.

### Interview Qs

- What kind of tests you have written and what scenarios you have covered.

![[Pasted image 20251224122320.png]]

Think about corner cases.
Think about scale.
Think about 0 cases.

# Overview

- Very few % of front end devs write test cases. Many of them know how to write test cases but do not get the opportunity to write test cases.
- It is an important aspect as frontend is the face of the product.
- It is a very crucial part of front end devs as well.

- Many FAANGs and companies have no testers at all, so devs have to write test cases.

## Types of testing 

### 1. Unit Testing:
Unit testing involves testing individual components or functions in isolation to ensure they work correctly.
Tools: Popular unit testing tools for JavaScript include Jest, Mocha, and Jasmine.

### 2. Integration Testing:
Integration testing focuses on verifying that different components or modules work together as expected when integrated.
Tools: Testing libraries like Cypress, Selenium, and Puppeteer can be used for integration testing.

### 3. Functional Testing:
Functional testing evaluates the application's features and functionality from an end-user perspective.
Tools: Selenium, Cypress, and Playwright are commonly used for functional testing.

The above three tests are generally written by developers to some extent.

### 4. End-to-End (E2E) Testing:
E2E testing involves testing the entire application flow, from the user interface to the backend, to ensure all components work together seamlessly.
Tools: Cypress, Selenium, and Playwright are also commonly used for E2E testing.

If we have a dedicated testing team they will write e2e testing, usability testing and manual testing.
### 5. Regression Testing:
Regression testing ensures that new code changes do not introduce bugs or break existing functionality.
Tools: Automated testing tools can be used for regression testing, and CI/CD pipelines often include regression test suites.

### 6. Performance Testing:
Performance testing assesses the speed, responsiveness, and overall performance of the frontend application under different conditions.
Tools: Tools like Lighthouse, Google PageSpeed Insights, and WebPageTest can be used for performance testing.

If web page loading is slow, web search engines will de-rank our website and it will be shown lower in the ranking.

### 7. Accessibility Testing:
Accessibility testing ensures that the application is usable by people with disabilities and complies with accessibility standards.
Tools: Lighthouse, Axe, and Pa11y are popular tools for accessibility testing.

**For senior engineers, accessibility testing is very crucial and important. WCAG(Web Content Accessibility Guidelines) guidelines are a must in big companies and in interviews.**

### 8. Cross-Browser Testing:
Definition: Cross-browser testing checks the application's compatibility and functionality across different web browsers.
Tools: BrowserStack, CrossBrowserTesting, and Sauce Labs are examples of platforms that provide cross-browser testing capabilities.

### 9. Usability Testing:
Usability testing evaluates how easily users can interact with and navigate through the application.
Tools: Usability testing often involves manual testing and user feedback.
This is another name for manual testing

### 10. Security Testing:
Security testing identifies and addresses vulnerabilities in the application, protecting it from potential threats.
Tools: Tools like OWASP ZAP, Burp Suite, and Snyk can be used for security testing.

### 11. Localization and Internationalization Testing:
These types of testing ensure that the application works correctly in different languages and regions.
Tools: Manual testing is often involved in checking language translations and regional settings.
Effective testing strategies often involve a combination of automated and manual testing methods to thoroughly assess the frontend application's quality and reliability.


### 12. A/B Testing:
A/B testing, also known as split testing, is a method used to compare two versions of a webpage or application to determine which one performs better. It is a statistical experiment in which different variations of a page or feature are presented to users randomly, and their responses are analyzed to determine which variation is more effective.

### 13. TDD:
TDD stands for Test-Driven Development. It is a software development methodology in which tests are written before the actual code that needs to be implemented. TDD follows a cycle of steps: write a test, make the test pass, and then refactor the code.