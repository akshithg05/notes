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
4. If we want access to footer of an application use pagination.

#### Infinite scroll pros/ when to use-

1. Real-time / dynamic data.
2. If we want the data to be addictive and keep user on the app for a long time. Friction in pagination is more if we want to move from one page to another.
3. Mobile friendly compared to pagination.

Cons of infinite scroll -

1. Bad for SEO. Difficult for search engines to crawl if there are infinite data in page. Only one part of page can be crawled by search engines.
2.  Searching capability is difficult because how to search in a page when data itself does not exist.

#### Always decide infinite scroll vs pagination, which one is actually required.

![[namastedev.com_learn_namaste-frontend-system-design_pagination.png]]

Google search recently shifted from infinite scroll to pagination

## Types of pagination

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
3. 
