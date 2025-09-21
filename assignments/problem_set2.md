# Problem Set 2: Composing Concepts

## Concept Questions
1. **Contexts**. The NonceGeneration concept ensures that the short strings it generates will be unique and not result in conflicts. What are the contexts for, and what will a context end up being in the URL shortening app?
- Contexts are for differentiating users of the NonceGeneration. For example, if I have two domains `bit.ly` and `byte.ly`, the same nonce generated for both wouldn't conflict with each other since they exist in separate contexts. Contexts in the context of the URL shortening app are different domains we are using as the **base part of the URL**.
2. **Storing using strings**. Why must the NonceGeneration store sets of used strings?
- The problem with maintaining and incrementing a counter for the NonceGeneration is that it does not keep track of strings that have already been created. There is a chance that the same string would be generated twice, which we do not want to happen, since the spec require that every nonce generated in a context is unique.
3. **Words as nonces**. One option for nonce generation is to use common dictionary words (in the style of yellkey.com, for example) resulting in more easily remembered shortenings. What is one advantage and one disadvantage of this scheme, both from the perspective of the user? How would you modify the NonceGeneration concept to realize this idea?
- An advantage is that it is much easier to communicate to other people. Saying `yellkey.com/short` is much easier than `yellkey.com/Yu78vi`. A disadvantage is there are a limited amount of words to use vs. the combination of random alphanumeric characters. This can make nonces easily guessable, posing a security issue. I would add "a set of `Words`" to the `Context` in the concept and change `generate` to choose a word from `Words` not already in `used`, then mark that word as used.

## Synchronizations for URL Shortening
1. **Partial matching**. In the first sync (called generate), the Request.shortenUrl action in the when clause includes the shortUrlBase argument but not the targetUrl argument. In the second sync (called register) both appear. Why is this?
- This is because the `targetUrl` is not needed to generate a nonce. We established earlier that the `shortUrlBase` is our context, so we only need this much information to guarantee that we don't generate a duplicate nonce.
2. **Omitting names**. The convention that allows names to be omitted when argument or result names are the same as their variable names is convenient and allows for a more succinct specification. Why isn’t this convention used in every case?
- There are sometimes where we have a variable we want to bind, but it has a different name than the result, so we must write it out. `expireResource(): (resource: shortUrl)` is an example of this. Additionally, when syncs connect actions across different concepts, we might have duplicate names, so dropping names could be confusing.
3. **Inclusion of request**. Why is the request action included in the first two syncs but not the third one?
- We established that the `expireResource` action is a system action, which is performed spontaneously when its precondition is true. Thus, it makes sense that the third sync has no request because it is called by the system, not the user.
4. **Fixed domain**. Suppose the application did not support alternative domain names, and always used a fixed one such as “bit.ly.” How would you change the synchronizations to implement this?
- We would no longer need to have different contexts, and thus no longer need `shortUrlBase`. We would change the `generate` sync by removing the `shortUrlBase` parameter to the `Request.shortenUrl`. We would change the `register` sync by removing the `shortUrlBase` parameter from `Request.shortenUrl` and set the `shortUrlBase` parameter in `UrlShortening.register` to be a hardcoded value (whatever our global context is). The `setExpiry` sync would not change.
5. **Adding a sync**. These synchronizations are not complete; in particular, they don’t do anything when a resource expires. Write a sync for this case, using appropriate actions from the ExpiringResource and URLShortening concepts.
- **sync** handleExpiry \
**when** ExpiringResource.expireResource () : (resource: shortUrl)\
**then** UrlShortening.delete(shortUrl)

## Extending the Design

### Additional Concepts
**concept** User\
**purpose** maintain access of short URLs\
**principle** a user registers an account, assigns and unassigns shortUrls to it, can be authenticated for access to those shortUrls, and may delete their account along with its associations.\
**state**\
&nbsp;&nbsp; a set of `Users` with \
&nbsp;&nbsp;&nbsp;&nbsp; a username String\
&nbsp;&nbsp;&nbsp;&nbsp; a set of `ShortUrls`\
**actions**\
&nbsp;&nbsp;`register(username: String): (user: User)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** user with username to not already exist\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** creates a new user with the given username\
&nbsp;&nbsp;`assign(user: User, shortUrl: String)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** user to exist, shortUrl to exist\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** associates the `shortUrl` with the user\
&nbsp;&nbsp;`unassign(user: User, shortUrl: String)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** user to exist, shortUrl to exist\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** disassociates the `shortUrl` with the user\
&nbsp;&nbsp;`authenticate(user: User, shortUrl: String): (flag: Boolean)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** user to exist, shortUrl to exist\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** returns true if user can access `shortUrl` else false\
&nbsp;&nbsp;`delete(user: User)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** user to exist\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** deletes user

**concept** Analytics\
**purpose** keep track of number of time a mapping between URL and shortened URL is used\
**principle** for each shortUrl, the system initializes an analytics record, increments the count whenever the shortUrl is used, and reports the total count when requested.\
**state**\
&nbsp;&nbsp; a set of `Records` with\
&nbsp;&nbsp;&nbsp;&nbsp; a `shortUrl` String\
&nbsp;&nbsp;&nbsp;&nbsp; a `count` Number\
**actions**\
&nbsp;&nbsp;`initialize(shortUrl: String)`\
&nbsp;&nbsp;&nbsp;&nbsp;**requires** no record has shortUrl\
&nbsp;&nbsp;**effect** creates new record with shortUrl and count = 0\
&nbsp;&nbsp;`increment(shortUrl: String)`\
&nbsp;&nbsp;&nbsp;&nbsp; **requires** shortUrl to exist in `Records`\
&nbsp;&nbsp;&nbsp;&nbsp; **effect** adds 1 to count for shortUrl\
&nbsp;&nbsp;`reportAnalytics(shortUrl: String)`\
&nbsp;&nbsp;&nbsp;&nbsp; **requires** shortUrl to exist in `Records`\
&nbsp;&nbsp;&nbsp;&nbsp;**effect** returns current count for shortUrl

### Additional Syncs
1. When shortenings are created\
**sync** assignOwnership\
**when**\
&nbsp;&nbsp;Request.shortenUrl (user, targetUrl)\
&nbsp;&nbsp;UrlShortening.register (): (shortUrl)\
**then** UserAccounts.assign (user, shortUrl)

2. When shortenings are translated to targets\
**sync** recordAccess\
**when** UrlShortening.lookup (shortUrl)\
**then** Analytics.increment (shortUrl)

3. When a user wants to examine analytics\
**sync** examineAnalytics\
**when**\
&nbsp;&nbsp;Request.viewAnalytics (user, shortUrl)\
&nbsp;&nbsp;UserAccounts.authenticate (user, shortUrl): (flag)\
**then** if flag is true then Analytics.reportAnalytics (shortUrl)

### Additional Features
- **Allowing users to choose their own short URLs**: To implement this, we would need to add a new function to the UrlShortening concept that allows the user to create their own custom mapping `customRegister(shortUrl: String, targetUrl: String)`. We'd need to make a register custom sync, analogous to our register sync.
- **Using the "word as nonce" strategy to generate more memorable short URLs**: To implement this, we would follow the same steps as in 3. of [concept questions](#concept-questions). No sync modifications are necessary.
- **Including the target URL in analytics, so that lookups of different short URLs can be grouped together when they refer to the same target URL**: This feature is undesirable because as a user of UrlShortener, I only care about how often ***MY*** links are accessed, not other links that map to the same URL. This would potentially expose other mappings to the target URL as well if the user is able to see all shortened URLs that map to the target.
- **Generate short URLs that are not easily guessed**: To implement this, we only need to change the postcondition of `NonceGeneration.generate`. We would strengthen the postcondition to provide the level of complexity desired (e.g. length $n$ string with special characters). 
- **Supporting reporting of analytics to creators of short URLs who have not registered as user**: This feature is undesirable because it would require loosening the ownership rules in our `User` concept. In my implementation, we want only a certain set of users to be able to access analytics, so we should require users to register for them to see the analytics.