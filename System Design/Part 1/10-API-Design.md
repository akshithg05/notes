Now, let's delve into the process of designing APIs, also known as the surface area or API contract. We will use the Twitter REST API as an example, which will help us understand the considerations, restrictions, versioning, and the various functions that an API can encompass.

APIs typically provide general CRUD (Create, Read, Update, Delete) functions. In the case of Twitter, these functions may include `createTweet()`, `getTweets()`, `editTweet()` and `deleteTweet()`.

These operations are performed on entities, which can be thought of as nouns or resources (e.g. tweets, users, etc). The operations themselves, such as create, delete, etc., are equivalent to different HTTP/REST methods, namely `GET`, `POST`, `PUT`, and `DELETE`. As developers, we need not be concerned with the internal implementation of the API, but rather focus on the method signature and the return value.

By defining the API contract, we establish a clear interface for developers to interact with the API, ensuring consistent behavior and seamless integration into their applications.

## Why bother designing good APIs?

When designing good APIs, it is crucial to consider their public-facing nature. These APIs can be relied upon by hundreds, if not thousands, of applications, which heavily depend on their function calls. This restriction limits API developers from making excessive changes to avoid potential crashes in the apps that rely on the Twitter API.

### Creating a Tweet

Let's consider the example of the `createTweet(userId, content)` method, which is used to create a tweet. Suppose we want to introduce a reply feature. Modifying the original method signature to include a `parentId` parameter, like `createTweet(userId, content, parentId)`, would potentially disrupt a large number of applications. To address this, a better approach would be to make the `parentId` parameter optional.

By making the `parentId` parameter optional, we acknowledge that not every tweet is a reply and may not have a parent tweet. This design choice also ensures **backward compatibility**, which means that newer additions or changes to the software application should still be compatible with older versions of the same application. Therefore, applications utilizing the `createTweet(userId, content)` method would not be required to make any changes to their existing code.

Considering **backward compatibility** helps maintain a smooth transition and avoids breaking existing functionality for applications that rely on the original method.

A tweet object might look like the following and creating the tweet might have the following URL:

`https://api.twitter.com/v1.0/tweet`

```json
userId: string, // The creator of the tweet, passed by the client
tweetId: string, // Uniquely identifies each tweet, created server side
content: string, // Passed in by the client
createdAt: date, // The timestamp, handled server side
likes: int, // handled by the server side
```

### Retrieving Tweets

Retrieving a single tweet can be accomplished using an endpoint like `https://api.twitter.com/v1.0/tweet/:userId`, which fetches all the tweets for a specific creator. However, when it comes to retrieving a list of tweets, a different approach is needed. This situation often arises in Higher Education institutions' websites, where a segment on the homepage displays their Twitter activity. Using the same endpoint for retrieving a single tweet is not suitable in this case.

To address this, let's recall the concept of pagination discussed in the previous chapter. To fetch only 10 tweets, we can structure our URL as follows: `https://api.twitter.com/v1.0/users/:id/tweets?limit=10&offset=0`. Here, the `limit` parameter indicates the number of tweets to be fetched per page, while the `offset` parameter determines the starting point. It's important to recall that GET requests are idempotent, meaning that regardless of how many times we call this URL, it should consistently return the same data without side effects. (Though, in twitter's case the homefeed data itself may change over time.)

By incorporating `limit` and `offset` parameters in the URL, we can implement pagination effectively, enabling the retrieval of a specific number of tweets at a time while maintaining consistency in the returned data.

> We could technically design a server to write data to a database in handling of a get request, but it is against HTTP best practices. GET requests are supposed to be read-only.

### API Versions

When significant changes are made to an API, such as adding new parameters, methods, or completely changing how things work, companies typically update the API version. They announce that the previous version is deprecated and developers are encouraged to update their API calls accordingly.

By versioning the API, it becomes easier to distinguish between different iterations and helps developers adapt their code to accommodate any changes or improvements. Deprecating the older version prompts developers to transition to the latest version, which often offers better functionality, improved performance, and bug fixes.

The deprecation announcement serves as a notification for developers to update their code and align it with the latest API specifications. This ensures compatibility and a smooth transition while embracing the advancements and updates in the API design.

> Sometimes, to address the security vulnerabilities, API providers may release new versions as well. For this, they may deprecate old API keys and issue and generate new ones for the client. API keys are like a secret token, which is included in the API requests to verify the identity and permissions of the requesting application or client.

---

## Twitter's REST API

This section demonstrates how the REST API looks like on the Developer Platform of Twitter.

1. First, let's look at how a tweet is created.

![create-tweet-1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/e4314932-936f-47d8-d091-f8890fb78200/sharpen=1)

> Above we see the API call (POST) to create a tweet on behalf of the authenticated user.

![create-tweet-2](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/6d79e1b7-d52d-4157-fe99-14826546db00/sharpen=1)

> The payload that would be sent in the POST request. Notice how these are all optional.

![create-tweet-3](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/c49c2729-95d8-46c4-b520-f820af4d6200/sharpen=1)

> The result of a successful response. The response fields in the Twitter API contain information returned by the API server after making a request.

2. Another example is a `GET` request for fetching a given user's tweets.

![fetch-tweet-1](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/5149e595-6bd7-4d8a-805a-7050fcaa3c00/sharpen=1)

> Above we see the end-point URL format we discussed before hand. Given an ID, we can fetch the tweet. Our pagination concept from earlier also comes into play here. The `2` in the URL represents the version of the API.

![fetch-tweet-2](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/99e11fff-d673-46ca-8833-29ecae1f0c00/sharpen=1)

> Notice how the parameter `id` is required.

![fetch-tweet-3](https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/907707b9-4015-4ad7-a332-54eba70bd600/sharpen=1)

> Passing in `max_results` parameter allows us to control how many results we fetch on each request. This is also optional and has a value set by default.

---

# Closing Notes

I encourage you to look at other APIs of your favorite social media apps to get more familiar.

Here are a few good ones:

- [Reddit](https://www.reddit.com/dev/api/)
- [Instagram](https://developers.facebook.com/docs/instagram-api/)
- [Facebook](https://developers.facebook.com/docs/)
- [Stripe](https://stripe.com/docs/api) (extremely good docs)

In conclusion, good API design should:

- Not have conflicting end-points
- Be backwards compatible
- Provide pagination