Tricky topic with many nuances, Many techniques are there to do pagination.
Pagination is not just a problem about front end, it includes backend concepts as well.

### 1. What is pagination ?

When we have large amounts of data and want to show it on our website, we cannot show it on a single page. We need pages in our application to show this information. We want to create smaller parts of the data to show on the website on each page.

### 3. How do we know that we want pagination ?

Only suggest pagination in an interview if it is really required.
Is there any alternative to pagination ?

### 3. A basic alternative to pagination can be infinite scroll.

We have to smartly decide if we want to alternate between having multiple pages or load more data as infinite scroll.

In an interview dont be fixed with one appraoch. Suggest alternative approach, choose one approach, and justify your approach. This is the best way to approach problems.


## 4. Pagination vs Infinite Scroll

#### Pagination pros and when to use-

1. The data is structured and hierarchical.
2. Access to footer of an application
3. Finite data and fixed number of pages
4. Easy to move back and forth.

#### Infinite scroll pros/ when to use-

1. Real-time / dynamic data.
2. If we want the data to be addictive and keep user on the app for a long time. Friction in pagination is more if we want to move from one page to another.
3. Mobile friendly compared to pagination.

Cons of infinite scroll -

1. Bad for SEO. Difficult for search engines to crawl if there are infinite data in page. Only one part of page can be crawled by search engines.
2.  Searching capability is difficult because how to search in a page when data itself does not exist.

#### Always decide infinite scroll vs pagination, which one is actually required.

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_pagination 1.png]]

Google search recently shifted from pagination to infinite scroll

## 5. Types of pagination

### 1. Front end pagination 

- Browser level
Fetch all data at once. Get all the data, then show a navigation to dynamically paginate. API call is only once though. As user moves back and forth in the page we fetch the data.

### 2. Server side pagination 

- API Level
Make API call get products. If user moves to another page, make API call and show it on the web page. Here we are fetching data per page (not all data at once).


### Pros and cons of each type 

#### 1. Front end pagination

Pros -
1. Changing page does not require API call, page change is very fast, no extra time is required. Faster page navigation.
2. Less API calls (only one).
3. Easy to implement (no backend logic required).
4. Map, filter, reduce on all data at a time.
5. Full data control

Drawbacks / Cons -
1. High initial load time. First API call will take a lot of time if dataset is huge.
2. It is browser heavy, can make the application/ page very slow. Not fruitful for large amounts of data.

[[2026-04-09]]

#### 2. Backend pagination (Server side pagination)

Pros -
1. Works well on large data.
2. Initial load time is very fast. (only 10-50 entries if needed)

Cons - 
1. Many API calls, every page change requires an API call.
2. Sorting, searching APIs must be written, everything must be done on backend. (Trickier than frontend pagination).
3. Backend dependency.

![[Front End System Design/images/namastedev.com_learn_namaste-frontend-system-design_pagination 1.png]]

Mainly choose on data. More data - backend , less data- front end pagination.

## 6. Server side pagination implementation (offset pagination)

We need to send some things to the API -
1. Offset - How many items to skip
2. Limit - How many results to fetch and display
3. Page - page generally = offset ((page-1) x limit)

For example , If in the API we sent page 2 and limit 10
then we would be skipping 10 records and showing the next 10.

All this depends on the API design pattern on the backend.

## 7. Another pagination - cursor pagination 

Many people say we need to use this cursor pagination only.
It was introduced by facebook, and they say we need toa

### Problems with Offset pagination

![[namastedev.com_learn_namaste-frontend-system-design_pagination 1 1.png]]
## What is Offset Pagination

Offset pagination is a commonly used pagination technique where we fetch data using:
- `offset` → starting index
- `limit` → number of items to fetch

Example:
- Page 1 → offset = 0, limit = 4
- Page 2 → offset = 4, limit = 4
- Page 3 → offset = 8, limit = 4
---
## Example Scenario

Consider a list of users registering on a platform.
Initial data:

- Page 1 → x, y, z, d
- Page 2 → j, k, l, m
- Page 3 → t, y, u, i

User navigates:
- Page 1 → Page 2 → Page 3

---
## Problem with Offset Pagination

### 1. Data is Dynamic (Real-Time Updates)

While the user is navigating between pages:
- New users may get added
- Existing users may get deleted

This causes **data shifting across pages**

---
### 2. Duplicate Data Issue

Scenario:
- User moves from Page 2 → Page 3
- Meanwhile, new users (e.g., a, s) are added at the top (Page 1)

Effect:
- All existing data shifts forward
- Some items that were on Page 2 may now appear again on Page 3

Result:
- User sees **duplicate entries across pages**

---
### 3. Missing / Skipped Data Issue

If some data is deleted:
- Items shift backward
- Some entries may get skipped entirely

Result:
- User **misses certain data**
- Inconsistent pagination experience
---
## Key Insight

Offset pagination assumes that:
- The dataset is **static**

But in real-world applications:
- Data is **frequently changing**    

This makes offset pagination unreliable for dynamic data.

---
## Conclusion

Offset pagination can lead to:
- Duplicate data
- Missing data
- Inconsistent user experience

Because of these issues, a better approach called **Cursor Pagination** was introduced (popularized by Facebook).
