
1. First step is to build a basic search bar with basic functionality where on each input we make an API call and results are fetched and displayed.

This method can be optimized to reduce API calls. Making API call on every request leads to wastage of resources. We can use debouncing, where we wait for a certain period and then make the API call to fetch results.

If there are many people are using our application this will become a problem.

## 2. Debouncing 

Only make the API call after a certain interval between keystrokes. Do not make the api call immediately, otherwise assume that we are continuing to tyoe.

Further enhancement which can be asked by the interviewer is caching implementation. We can cache the search results for that particular key value pair and show that instead of making API call.
## 3. Caching 

We can cache using localStorage, sessionStorage, Redux state library, or use local state variable.


