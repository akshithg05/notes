
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


![[namastedev.com_learn_namaste-frontend-system-design_hld-e-commerce-app-amazon-flipkart (1).png]]

As a junior dev until API gateway and services, it is good to have knowledge. As a super senior level and full stack developer we need to have more knowledge about backend services, DB how it has been architecture , etc.

## 3. Data model

Very important 

![[namastedev.com_learn_namaste-frontend-system-design_hld-e-commerce-app-amazon-flipkart (1) 1.png]]
## 4. API

Have a discussion if you want to use REST or GraphQl if you know GQL.

![[namastedev.com_learn_namaste-frontend-system-design_hld-e-commerce-app-amazon-flipkart (2).png]]


## Primary non- functional requirements for applications like ecommerce

### 1. Optimization 

1. Lazy loading and code splitting.

![[namastedev.com_learn_namaste-frontend-system-design_hld-e-commerce-app-amazon-flipkart (2) 2.png]]

Adaptive loading hooks.

### 2. Search Engine Optimization (SEO)

## What is SEO?

SEO (Search Engine Optimization) is the process of improving how well a website:
- Gets discovered by search engines
- Gets indexed
- Ranks in search results

Goal:
Increase visibility, traffic, and discoverability.

For e-commerce websites, SEO directly impacts:
- Product discovery
- Organic traffic
- Revenue

---

# How Search Engines Work (Simple Flow)

1. Crawler visits website
2. Reads HTML content
3. Indexes important pages
4. Ranks pages based on quality signals

Important:
Search engines primarily understand HTML content, structure, metadata, and performance.

---

# 1. Title & Meta Tags

Meta information helps search engines and social platforms understand the page.

Important tags:
- title
- meta description
- Open Graph tags
- Twitter cards
- viewport

Examples:
- Product title in Google search
- Product description preview
- Image preview on WhatsApp/Twitter/LinkedIn

Good metadata improves:
- Click-through rate (CTR)
- Discoverability
- Social sharing previews

Example:

<title>iPhone 15 Pro - Buy Online</title>

<meta
  name="description"
  content="Buy iPhone 15 Pro with best offers and fast delivery."
/>

---

# 2. sitemap.xml

A sitemap is a structured list of important URLs in the application.

Purpose:
- Helps search engines discover pages
- Improves crawling efficiency
- Useful for large e-commerce sites

Common pages:
- Product pages
- Categories
- Landing pages

Example:
sitemap.xml contains:
- /products/iphone-15
- /products/macbook-air
- /category/mobiles

---

# 3. robots.txt

robots.txt tells crawlers:
- What they can crawl
- What they should avoid

Used to block sensitive or unnecessary pages.

Example pages to avoid indexing:
- Payment pages
- Admin pages
- Internal dashboards
- Cart/checkout pages

Example:

User-agent: *
Disallow: /checkout
Disallow: /admin

---

# 4. Canonical Tags

Canonical tags prevent duplicate content issues.

Sometimes multiple URLs point to the same content.

Example:
- /product/iphone
- /product/iphone?ref=home

Canonical tag tells search engines:
"This is the original page."

Example:

<link
  rel="canonical"
  href="https://example.com/product/iphone"
/>

Important for:
- Product variants
- Filters
- Tracking query params

---

# 5. Semantic HTML Improves SEO

Search engines understand semantic HTML better.

Use:
- header
- nav
- main
- article
- section
- h1 to h6

Avoid:
- Div-only layouts for everything

Semantic HTML improves:
- Accessibility
- SEO
- Crawlability

---

# 6. Page Speed Impacts SEO

Faster websites rank better.

Search engines consider:
- Core Web Vitals
- Load speed
- Performance metrics

Important metrics:
- LCP
- CLS
- FCP
- INP/FID

Slow websites:
- Rank lower
- Increase bounce rate

Optimizations:
- Image optimization
- Code splitting
- Lazy loading
- CDN caching
- Compression

Rule:
Better performance → Better SEO.

---

# 7. SSR vs CSR vs SSG for SEO

## CSR (Client-Side Rendering)
Problem:
Initial HTML mostly contains JavaScript.

Crawler may not fully render JS content.

SEO is weaker if content depends heavily on client rendering.

---

## SSR (Server-Side Rendering)
Server sends fully rendered HTML.

Benefits:
- Better crawlability
- Better indexing
- Better SEO

Very useful for:
- Product pages
- Dynamic content
- E-commerce websites

---

## SSG (Static Site Generation)
Pages are pre-generated at build time.

Benefits:
- Extremely fast
- Excellent SEO
- CDN-friendly

Best for:
- Frequently visited pages
- Marketing pages
- Popular product pages

---

## Hybrid Optimization for CSR Apps

For CSR applications:
- Use prerendering for crawlers
- Serve rendered HTML to bots
- Improve indexing without fully moving to SSR

This is often used as an SEO optimization strategy.

---

# 8. Shareable & Readable URLs

URLs should:
- Be human-readable
- Be shareable
- Reflect app state

Good:
/phones/iphone-15?color=black

Bad:
/product?id=12345&x=abc

Search and filters should be represented in the URL when meaningful.

Benefits:
- Better sharing
- Better SEO
- Better user experience

---

# SEO Interview Cheat Sheet

1. Use proper title and meta tags
2. Add sitemap.xml
3. Configure robots.txt properly
4. Use canonical tags to avoid duplicate content
5. Use semantic HTML
6. Optimize page speed and Core Web Vitals
7. Prefer SSR/SSG for SEO-heavy pages
8. Keep URLs readable and shareable

---

# Key Takeaway

SEO in e-commerce depends on discoverability, semantic structure, metadata, performance, and rendering strategy (SSR/SSG) to improve search ranking and user reach.

---

# One-Line Interview Summary

SEO improves discoverability and ranking by optimizing metadata, semantic HTML, page speed, crawlability, and rendering strategies like SSR and SSG.


## 3. Internationalization

## What is Internationalization (i18n)?

Internationalization (i18n) is the process of designing applications so they can support:
- Multiple languages
- Different regions
- Different cultures

Goal:
Make the application adaptable for global users without major code changes.

Example:
- English
- Arabic
- Japanese
- French

---

# i18n vs l10n

## Internationalization (i18n)
Preparing the application for multiple languages and regions.

## Localization (l10n)
Actually translating and adapting content for a specific region.

Example:
- Currency formatting
- Date formatting
- Language translation

---

# 1. HTML Language Attribute

Set the language using the `lang` attribute.

Example:

``` hmtl
<html lang="en">
```
Benefits:
- Helps browsers and screen readers
- Enables browser translation features
- Improves SEO
- Improves accessibility

The lang attribute should match the user’s region/language.

---

# 2. hreflang Alternate Links

Used to tell search engines about alternate language versions of a page.

Example:

``` html
<link
  rel="alternate"
  hreflang="en"
  href="https://example.com/en"
/>

<link
  rel="alternate"
  hreflang="fr"
  href="https://example.com/fr"
/>
```

Benefits:
- Better SEO for multilingual sites
- Prevents duplicate indexing issues
- Helps users reach correct regional pages

---

# 3. x-default Fallback

Used when no matching language is found.

Example:

<link
  rel="alternate"
  hreflang="x-default"
  href="https://example.com"
/>

Acts as the default fallback page.

---

# 4. RTL (Right-to-Left) Language Support

Languages like:
- Arabic
- Urdu
- Hebrew

use Right-to-Left (RTL) layout.

Important:
These are NOT left-to-right languages.

---

## CSS Support for RTL

Example:

``` html
<html dir="rtl">
```
Useful CSS logical properties:
- margin-inline-start
- padding-inline-end
- inset-inline-start

Avoid hardcoded:
- margin-left
- padding-right

Logical properties automatically adapt to RTL/LTR layouts.

---

# 5. Language Switching Libraries

Frontend libraries help manage translations dynamically.

Popular libraries:
- i18next
- react-i18next
- next-intl
- formatjs

Features:
- Dynamic translation loading
- Namespace support
- Pluralization
- Variable interpolation

Example:

t("welcome_message")

---

# 6. Currency & Date Formatting

Different countries use different:
- Currency symbols
- Number formats
- Date formats
- Time zones

Examples:
- $1,000.00 (US)
- 1.000,00 € (Europe)

Use Intl APIs:

``` js
new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD"
})

new Intl.DateTimeFormat("en-IN")
```

Important:
Never hardcode date or currency formats.

---

# 7. Form Validation & Localization

Validation messages should also be translated.

Example:
- "Email is required"
- "Password too short"

Validation rules may vary by region:
- Postal codes
- Phone numbers
- Address formats

---

# 8. API Localization

Backend APIs can support localization using headers.

Example:

Accept-Language: en-US

Backend can return:
- Translated responses
- Region-specific data
- Localized formatting

Use UTF-8 encoding to support multilingual text properly.

---

# 9. Cultural Considerations

Symbols, colors, images, and gestures can mean different things across cultures.

Examples:
- Colors may carry different emotional meanings
- Hand gestures may be offensive in some countries
- Icons may not be universally understood

Design carefully for global audiences.

---

# SEO & Internationalization

For multilingual SEO:
- Use lang attribute
- Use hreflang tags
- Use translated URLs
- Avoid automatic redirection without user choice

---

# i18n Interview Cheat Sheet

1. Set correct HTML lang attribute
2. Use hreflang alternate links
3. Add x-default fallback
4. Support RTL languages
5. Use logical CSS properties
6. Use i18n libraries for translations
7. Format dates/currency using Intl APIs
8. Localize form validation
9. Use Accept-Language headers
10. Respect cultural differences in UI design

---

# Key Takeaway

Internationalization prepares applications for global audiences by supporting multiple languages, regional formats, RTL layouts, localization, and culturally aware UI design.

---

# One-Line Interview Summary

Internationalization (i18n) enables applications to support multiple languages, regions, and cultural conventions through localization, formatting, RTL support, and language-aware rendering.