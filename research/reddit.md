# Reddit — Data Source Feasibility Assessment

## 1. Accessibility

**Official Documentation:** Reddit provides a Data API that allows approved developers to access posts and comments programmatically.

API access requires authorization and OAuth authentication. Commercial use requires explicit permission from Reddit.

**Manual Testing:** Not performed.

**Automated Testing:** Not performed because approved API access and commercial-use authorization are not currently available for this project.

Therefore, the accessibility of Reddit data for an automated ingestion workflow remains unverified.

## 2. Pagination

**Official Documentation:** Reddit's listing endpoints support cursor-based pagination using parameters such as `after`, `before`, and `limit`.

The `after` parameter allows clients to request additional records beyond the current batch.

This suggests that Reddit provides a documented mechanism for retrieving multiple batches of data through its API.

However, pagination has not been tested in practice.

## 3. Available Fields

**Official Documentation:** Reddit's API provides structured data containing information about posts and comments.

Potentially useful fields include:

- **Posts:** Post ID (`id`), title (`title`), post text (`selftext`), subreddit (`subreddit`), creation time (`created_utc`), and score (`score`).
- **Comments:** Comment ID (`id`), comment text (`body`), creation time (`created_utc`), score (`score`), and parent ID (`parent_id`).
- **Discussion structure:** Relationships between posts, comments, and replies.

These fields are identified from the API's documented data structure. Their availability and completeness have not been verified through actual API responses.

## 4. Repeatability

**Official Documentation:** Reddit provides structured API endpoints that support programmatic requests and pagination.

However, no automated retrieval test has been performed.

It has not been verified whether the same posts and comments can be consistently retrieved across multiple requests or at different times.

Therefore, repeatability remains unverified.

## 5. Sufficient Useful Text

Reddit discussions may contain useful customer-generated text for sentiment analysis, including product experiences, complaints, suggestions, comparisons, and recurring issues.

Post content and comment threads may provide more detailed customer feedback than numerical ratings alone.

However, no actual text samples have been retrieved or evaluated in this assessment.

Therefore, the quantity and relevance of text available through an authorized automated method remain unverified.

## 6. Official API and Usage Restrictions

**Official Documentation:**

- https://www.reddit.com/dev/api/
- https://support.reddithelp.com/hc/en-us/articles/16160319875092-Reddit-Data-API-Wiki
- https://support.reddithelp.com/hc/en-us/articles/14945211791892-Developer-Platform-Accessing-Reddit-Data
- https://redditinc.com/policies/data-api-terms

Reddit provides an official Data API for programmatic access to posts, comments, and other Reddit content.

Access requires approved API credentials and OAuth authentication.

Commercial use requires explicit permission from Reddit. API access is also subject to rate limits and restrictions on data collection, storage, redistribution, and certain AI-related uses.

For this assessment, no approved API access or commercial-use authorization is assumed to be available.

Therefore, the official API has not been tested.

## 7. Login / CAPTCHA / Verification

**Official Documentation:** OAuth authentication is required for Reddit Data API access.

**Manual Testing:** Not performed.

**Automated Testing:** Not performed.

No conclusion can be drawn about CAPTCHA challenges or additional verification requirements during actual retrieval.

## 8. Preliminary Conclusion

Reddit is a potentially useful source of customer-generated feedback, including product discussions, complaints, suggestions, and user experiences.

Compared with Amazon's manually accessible review interface, Reddit provides a documented API with structured data and cursor-based pagination.

However, the availability of an official API does not establish that the project has permission to use it.

**Current assessment:** Reddit is technically promising as a potential customer feedback source, but practical accessibility, repeatability, and authorized automated ingestion have not yet been validated.

Further testing would require appropriate API access and commercial-use authorization. Until then, Reddit should remain a candidate source rather than a validated ingestion source.
