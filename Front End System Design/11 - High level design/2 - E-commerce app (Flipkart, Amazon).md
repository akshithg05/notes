
FSD for applications like Myntra, Amazon, Flipkart, etc.

Not the same problem statement we will get every time. We have to keep asking the interviewer and get requirements and design the system. We have to drive the interview.

2 ways the problem statement can be put -

1. **Configurable UI** - The layout we see for amazon changes per user. Not only items, but even the layout shown is different for different users. Homepages are not static. It is a config driver UI for these homepages. So this can be the problem statement and what is the high level design for this.
2. **Browse and Purchase** - Inside a particular category (eg: Mobiles). We have search capabilities, many filters (brand, price, etc). Details page, cart, payment gateway, confirmation page, authentication.

## 1.  Browse and Purchase

As always first thing is requirements - Functional and non functional requirements.

#### 1.1 Functional 
Whatever you can see from a user perspective. What you can see

When we are doing the system design round, first think of the whole user flow of what a user will do while ordering some item or booking and list the steps as functional requirements.

As a dev, you need to be able to think from the customer perspective. Expectation is to know user requirement as a senior dev.

#### 1.2 Non - functional
These are not absolutely necessary, but to have these will be good and it will enhance the User experience.

1. Device Support - support for multiple devices
2. Auth - checkout page, payment page we need to login , etc
3. i18n - Internationalization - based on region change language and support languages. Language should not be a barrier for using your product and website
4. SEO - Helps to increase page index of website.
5. Optimization 
6. Security - Payments are involved, address and PII. All these info shouldnt be leaked.
7. Accessibility
8. Deployment strategies.
9. Offline support.

![[namastedev.com_learn_namaste-frontend-system-design_hld-e-commerce-app-amazon-flipkart.png]]


## 2. Architecture


