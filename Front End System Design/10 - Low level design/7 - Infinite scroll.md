Keep scrolling and things keep loading onto the web page

1. Find out that the user has reached the end of the page

window.innerHeight - height of the viewing content
document.body.scrollHeight - total height of the webpage
window.scrollY - how much on Y axis we have scrolled.

```js
window.scrollY + window.innerHeight = document.body.scrollHeight
``` 
if we have reached the end of the webpage

