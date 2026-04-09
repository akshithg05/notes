Routing is a core part of front end design. Every complex application has many pages and hence we need to handle routing properly to route these pages.

It is a core part of our app, when we create a URL and path (e.g amazon.com/products/electronics/samsung/phones) , It is not easy to change these routes later on that easily. 
It becomes hard to change it later on if we did not design routes properly.

1. Search engines crawl websites, if we change routes, it directly impacts search engine optimization (SEO). Search engine track our pages because of routes.

2. Routing is important for user experience as well. Changing route from /x/z to /x/y/z will affect users as many will still visit the older route. This is because people tend to bookmark old routes.  In such cases we need to redirect routes. But this just a fallback, not a good design.

Therefore routing and route design is important.

3. Query params also play an important part of routes which need to be taken care of.

4. Earlier there were MPA (multiple page apps). Eg /about, /team, /contantus , all were different pages , different bundle of html css and js. With React angular , next we develop SPA.

5. Here one page is loaded and everything happens inside that page itself. only routes change which load different components within the same page which looks like multiple pages. Here routing becomes tougher and complicated. There is more logic involved.

Routing libraries or some router applications need to be used to achieve this. eg - react-router-dom in react. NextJS has its own router.

Dynamically components are replaced, but the full page is not reloaded. Only one html css js bundle on initial load. Only body section changes, header etc remains static.

Google crawls routes, if we change routes, SEO will get affected.

Best practice - 
1. Keep it as simple as possible, just simple , understandable, perceivable pages.

### Explain routing properly in interviews.


## 2. Protected routes - important in interview

Eg. /billing, /profile are protected routes

#### 3. How do you handle protected routes ? - important interview question.

#### 4. Nested routes

---REFER coding example of SHIMMER UI, we will be using the same React app--- 


### For protected routes check code in GH FSD

Bad way of having authenticated routes - 

``` js
<Route
	path="/about"
	element={isUserAuthenticated ? <AboutUs /> : <Login />}
></Route>
```

This is because the url will be the same but the component which is loaded will be different. This is not the right way to do things as it will confuse users.


##### Dont put auth logic where we have defined our routes, it will mess things up and does not scale well.

For protected routes create a wrapper and pass the route inside and then use outlet.


Outlet is used to outlet the children components 
The `<Outlet />` component in **React Router** is a placeholder used in a parent route element to define where its corresponding child route elements should be rendered.