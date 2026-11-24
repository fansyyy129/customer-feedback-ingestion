# Reddit — Data Source Feasibility Assessment

## 1. Official API and Usage Restrictions

### 1.1 Reddit Data API

**Official Documentation:**

- https://www.reddit.com/dev/api/
- https://support.reddithelp.com/hc/en-us/articles/16160319875092-Reddit-Data-API-Wiki
- https://support.reddithelp.com/hc/en-us/articles/14945211791892-Developer-Platform-Accessing-Reddit-Data
- https://redditinc.com/policies/data-api-terms

Reddit provides an official Data API for programmatic access to posts, comments, subreddits, and related information.

Its documented capabilities include:

- Retrieving subreddit post listings
- Retrieving post details and comment trees
- Searching for posts
- Accessing structured post and comment data
- Cursor-based pagination for listing endpoints

**Authentication and access requirements:**

- Reddit requires registered OAuth authentication for Data API clients.
- API access is subject to approval and applicable developer policies.
- Commercial use requires explicit permission from Reddit.

**Rate limits:**

Reddit's Data API documentation specifies a limit of 100 queries per minute per OAuth client ID for eligible free-access users, averaged over a 10-minute window.

Relevant response headers include:

- `X-Ratelimit-Used`
- `X-Ratelimit-Remaining`
- `X-Ratelimit-Reset`

These limits do not establish that this project qualifies for free access.

**Data usage restrictions:**

Reddit imposes restrictions on data collection, storage, redistribution, and certain AI-related uses.

Stored content must be handled in accordance with Reddit's deletion requirements, including removal of content deleted from Reddit.

**Assessment:** The Data API provides a documented technical mechanism for structured data retrieval, but its suitability for this commercial project depends on authorization.

### 1.2 Reddit Developer Platform

**Official Documentation:**

- https://developers.reddit.com/
- https://developers.reddit.com/docs/capabilities/server/reddit-api

Reddit also provides a Developer Platform for building applications and integrations within Reddit's ecosystem.

The platform provides developer tools and supported methods for interacting with Reddit data.

However, Developer Platform capabilities and permissions do not independently authorize unrestricted external collection of Reddit content for commercial analytics.

**Assessment:** Potentially useful for Reddit-integrated applications, but not a confirmed alternative to obtaining appropriate Data API permissions for this ingestion project.

### 1.3 Reddit for Researchers

**Official Documentation:**

- https://support.reddithelp.com/hc/en-us/articles/14945211791892-Developer-Platform-Accessing-Reddit-Data

Reddit provides a separate Reddit for Researchers program for eligible research use cases.

This program is distinct from standard developer access and has its own eligibility and approval requirements.

**Assessment:** Not an assumed access route for Sciencia AI's commercial ingestion project.

### 1.4 Automated Data Collection Restrictions

The ability to view Reddit content publicly does not establish permission to collect it automatically.

Automated collection must comply with Reddit's developer policies, access requirements, and applicable data-use terms.

For this assessment, no approved API access or commercial-use authorization is assumed to be available.

## 2. Accessibility

**Manual Testing:** I tested Reddit accessibility using a discussion in r/iphone while logged out.

I was able to access the post and read full-length comments without logging in.

The website also allowed me to view additional comments through its interface.

**Official API Documentation:** Reddit provides programmatic access to posts and comments through its Data API for approved clients using OAuth authentication.

**Not Verified:** Authorized automated accessibility for this project.

## 3. Pagination

**Manual Testing:** Reddit provided a button for loading additional comments.

I was able to load and view more comments without logging in.

This confirms that additional comments could be accessed through the website's manual interface.

**Official API Documentation:** Reddit's listing endpoints support cursor-based pagination using `after`, `before`, and `limit`.

Listing responses can contain an `after` cursor for requesting the next batch of records.

Post comment trees are accessed through comment-related endpoints and may require separate handling for additional replies.

**Not Verified:** Actual API pagination and repeated retrieval of multiple batches.

## 4. Available Fields

**Manual Testing:** The following information was observed on Reddit's website, not retrieved through an API.

**Post-level information:**

- Post title
- Post body
- Subreddit name

**Comment-level information:**

- Reviewer username
- Comment text
- Comment timestamp (relative time and exact date/time displayed on hover)
- Comment score and voting controls
- Nested replies and parent-child discussion structure
- Reply, Award, and Share options
- User profile images

The inspected discussion displayed multiple comments, including direct replies to other comments. This demonstrates that Reddit provides conversational context rather than only independent reviews.

**Official API Documentation:**

Potentially useful structured fields include:

- **Posts:** `id`, `title`, `selftext`, `subreddit`, `created_utc`, and `score`.
- **Comments:** `id`, `body`, `created_utc`, `score`, and `parent_id`.
- **Discussion structure:** Relationships between posts, comments, and nested replies.

These fields are identified from Reddit's documented data model. Their availability and completeness have not been verified through actual API responses for this project.

## 5. Repeatability

**Manual Testing:** I reopened the same Reddit post and was able to access previously viewed content again without logging in.

This indicates that manual access was repeatable under the tested conditions.

**Official API Documentation:** Reddit provides structured API endpoints that support programmatic requests.

However, content may change over time because of new comments, edits, deletions, or moderation.

## 6. Sufficient Useful Text

**Manual Testing:** Full-length user comments were accessible without authentication.

The inspected discussion contained user opinions and responses concerning an iPhone-related topic.

Some comments were short reactions, while others formed part of a discussion thread. This suggests that Reddit may provide useful qualitative feedback, although the relevance and depth of individual comments can vary.

**Official API Documentation:** Reddit provides post and comment text fields, including `selftext` and `body`.

**Not Verified:** The quantity and relevance of text available through an authorized automated method. A representative sample has not yet been systematically evaluated.

## 7. Login / CAPTCHA / Verification

**Manual Testing:**

- **Login:** Not required to view the tested post and comments.
- **CAPTCHA:** Not encountered.
- **Additional verification:** Not encountered.
- **Pagination:** Additional comments were accessible without authentication.
- **Repeated access:** Previously viewed content remained accessible when the post was reopened.

**Official API Documentation:** OAuth authentication is required for Reddit Data API access.

Reddit should therefore remain a candidate source rather than a validated recurring ingestion source.

Automated accessibility, repeatability, and the volume of retrievable text remain unverified.
