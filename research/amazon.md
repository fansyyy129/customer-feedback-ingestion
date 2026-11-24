# Amazon — Data Source Feasibility Assessment

**Source:** Amazon Customer Reviews  
**Status:** Preliminary assessment completed; automated ingestion not validated

## 1. Accessibility

**Manual testing:** Amazon review content was inaccessible while logged out, and login was required to access full reviews.

After logging in, I was able to access full-length customer reviews and load additional reviews.

This does not establish permission for automated data collection.

## 2. Pagination

**Manual testing:** Approximately 10 reviews were displayed at a time. I could click "Show 10 more reviews" to load additional reviews.

This suggests that the website supports incremental review loading through its interface. However, the underlying mechanism and its suitability for automated retrieval have not been verified.

## 3. Available Fields

**Observed after authentication:**

- **Individual reviews:** Full review text, star ratings, review titles, dates, product variations, verified purchase labels, and helpful votes.
- **Review navigation:** Search, sorting options, and filters for star ratings, product variations, reviewer types, and content formats.
- **Aggregated feedback:** Overall ratings, star-rating distributions, and AI-generated summaries of positive and negative themes.
- **Multimedia content:** Customer-uploaded photos and videos.

## 4. Repeatability

**Manual testing:** I was able to access multiple reviews and load additional reviews after logging in.

**Not yet verified:** Automated retrieval has not been tested. Therefore, the consistency and repeatability of programmatic data collection remain unknown.

## 5. Sufficient Useful Text

Amazon reviews contain potentially useful customer-generated text for sentiment analysis, including product feedback, positive and negative experiences, and recurring complaints.

Manual testing confirmed that multiple full-length reviews could be viewed after authentication.

However, the amount of text that can be consistently retrieved through an authorized automated method has not been established.

## 6. Official API and Usage Restrictions

**Official documentation:** https://developer-docs.amazon/sp-api/

Amazon provides a Customer Feedback API through its Selling Partner API (SP-API).

Access requires appropriate developer/application permissions and seller or vendor authorization.

The API provides structured review-topic insights, customer snippets, and aggregated trends.

Documented data includes:

- ASIN identifiers
- Positive and negative topics
- Mention metrics
- Rating impact
- Review snippets

The API supports programmatic requests, has published rate limits, and refreshes its underlying data weekly.

Public visibility of reviews does not establish permission for automated scraping or commercial reuse.

## 7. Login / CAPTCHA / Verification

**Manual testing:**

- **Login:** Required to access full reviews in the tested scenario.
- **CAPTCHA:** Not encountered.
- **Additional verification:** Not encountered.

Other access controls may appear under different conditions but were not observed during this test.

## 8. Preliminary Conclusion

Amazon provides analytically useful customer feedback, and full-length reviews can be accessed manually after authentication.

However, automated accessibility, retrieval consistency, and permission for recurring collection remain unverified.

**Current assessment:** Amazon is analytically relevant and may serve as a reference or supplementary source, but it has not yet been validated as a practical, repeatable ingestion source.

Further implementation is deferred while alternative data sources are evaluated.
