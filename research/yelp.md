# Yelp — Data Source Feasibility Assessment

## 1. Official API, Data Products, and Usage Restrictions

Yelp provides several different data access products. 

### 1.1 Yelp Places API (Formerly Yelp Fusion API)

**Official Documentation:**

- https://docs.developer.yelp.com/docs/places-intro
- https://docs.developer.yelp.com/docs/places-faq
- https://docs.developer.yelp.com/reference/v3_business_reviews
- https://docs.developer.yelp.com/docs/plans

Yelp Places API provides structured business information through REST endpoints.

Its main capabilities include:

- Business Search: Find businesses by keyword, location, category, or other filters.
- Business Details: Retrieve business names, addresses, ratings, review counts, and other attributes.
- Reviews: Retrieve a limited number of review excerpts.
- Review Highlights: Retrieve summarized review highlights under eligible plans.

**Review access limitations:**

The standard Places API does not provide full-length review text.

According to Yelp's documentation, review excerpts are approximately 160 characters long.

Available review excerpts depend on the plan. 

The Places Reviews API does not provide unrestricted pagination through all customer reviews. Users cannot select arbitrary reviews or retrieve the full review history through this endpoint.

**Assessment:** Useful for business metadata, overall ratings, and limited review previews. However, it is not sufficient for a recurring ingestion pipeline requiring substantial amounts of full-length customer feedback.

### 1.2 Yelp Insights / Partner APIs

**Official Documentation:**

- https://docs.developer.yelp.com/docs/yelp-insights
- https://docs.developer.yelp.com/docs/private-reviews-api

Yelp Insights provides expanded data access for authorized partners under a commercial agreement.

Its capabilities include:

- Private Reviews API: Access full-length customer reviews, review IDs, ratings, dates, and related information.
- Business Details: Retrieve detailed business information.
- Food & Drink Insights: Retrieve information about food and drink mentions.
- Engagement Metrics: Access consumer engagement indicators.
- Reporting API: Retrieve daily or monthly business activity metrics.
- Business Insights and Risk Signals: Access additional business analytics.

**Full-text review access:**

The Private Reviews API supports retrieval of full-length reviews.

Yelp's technical documentation describes access to the most recent 200 reviews, although actual availability and limits depend on the partner agreement.

Example endpoint:

`GET https://api.yelp.com/v3/private/businesses/{business_id}/reviews`

**Scheduled data delivery:**

Yelp Insights also supports:

- REST API requests for on-demand retrieval
- Daily or monthly JSON data feeds delivered through Amazon S3
- Review-related webhooks for supported partner integrations

Yelp recommends regular refreshes to maintain current review data. Subsequent feeds may reflect newly added, updated, or removed content.

**Access requirements:**

- A Yelp partnership agreement
- Appropriate API permissions
- Partner-specific account configuration
- Compliance with contractual data usage restrictions

**Assessment:** This is the most relevant Yelp product for a recurring full-text customer feedback ingestion workflow.

### 1.3 Yelp Open Dataset

**Official Sources:**

- https://www.yelp.com/dataset
- https://s3-media0.fl.yelpcdn.com/assets/srv0/engineering_pages/f64cb2d3efcc/assets/vendor/Dataset_User_Agreement.pdf

Yelp also provides a downloadable dataset containing historical business and customer review information.

The dataset includes structured files for different types of information, such as:

- Business information
- Review text and ratings
- User information
- Tips
- Check-ins
- Photos and photo metadata

Typical review fields include:

- `review_id`
- `business_id`
- `user_id`
- `stars`
- `date`
- `text`
- `useful`
- `funny`
- `cool`

**Advantages:**

- Contains substantial amounts of review text.
- Does not require website pagination or individual API requests for each review.
- Can support offline analysis and testing of data-processing methods.

**Limitations:**

The dataset is historical rather than a continuously updated live review feed.

The applicable Yelp Dataset User Agreement restricts usage to academic purposes. It does not automatically authorize commercial use or redistribution.

**Assessment:** Potentially useful for separately authorized academic research or educational experimentation. It should not be used as the production data source for commercial ingestion workflow without appropriate permission.

### 1.4 Other Yelp APIs

Yelp also provides additional APIs and integration tools, including:

- **Reporting API:** Provides business performance and engagement metrics rather than a general full-text review feed.
- **Reviews Webhooks:** Notify authorized partners of review events. Webhook payloads do not themselves provide full review text; authorized integrations can use review identifiers with an appropriate review data endpoint.
- **Respond to Reviews API:** Allows authorized business integrations to respond to reviews. Its primary purpose is review management rather than broad review collection.
- **Yelp GraphQL:** Provides access to certain Yelp Fusion data through a different query interface; it does not independently grant unrestricted full-review access.

These tools may support an ingestion or analytics workflow but do not remove the need for appropriate permissions.

### 1.5 Automated Scraping Restrictions

**Official Documentation:**

- https://www.yelp-support.com/article/Can-I-copy-or-scrape-data-from-the-Yelp-site
- https://terms.yelp.com/tos/en_us/20260101_en_us/

Yelp prohibits unauthorized automated scraping of its website, including automated extraction of reviews, business pages, photos, and user information.

Therefore, the ability to read reviews manually without logging in does not authorize automated website scraping.

Any recurring ingestion workflow should rely on an explicitly permitted API, data feed, or other authorized access arrangement.

## 2. Accessibility

**Manual Testing:** I tested Yelp review accessibility using the restaurant The Wolf while logged out.

I was able to access full-length customer reviews without logging in. Individual reviews were visible directly on the website, and additional review pages could be accessed without authentication.

Unlike Amazon, Yelp did not require login to view full reviews or navigate between review pages during my test.

However, manual accessibility does not establish permission or feasibility for automated data collection.

## 3. Pagination

**Manual Testing:** Yelp provided page-based navigation for customer reviews.

I was able to navigate to additional review pages and read full-length reviews on subsequent pages without logging in.

This confirms that manual pagination worked during the test.

**Official API Documentation:**

- The Yelp Places Reviews API returns a limited selection of review excerpts rather than an unrestricted paginated collection of all reviews.
- Yelp Insights provides additional review retrieval capabilities for authorized partners, but the amount of data available depends on the partnership agreement.

## 4. Available Fields

**Manual Testing:** The following information was observed on Yelp's website, not retrieved through an API

**Business-level information (e.g. The Wolf):**

- Business name: The Wolf
- Overall rating: 4.2 stars
- Total displayed reviews: 569
- Business categories

**Individual review information:**

- Reviewer display name
- Reviewer location
- Reviewer Elite status
- Reviewer category-specific review count
- Star rating
- Review date
- Full review text
- Customer-uploaded photos
- Review feedback options: Helpful, Thanks, Love this, and Oh no

**Official API Documentation:**

The standard Yelp Places API provides business information such as business ID, name, location, overall rating, review count, and other attributes depending on the API plan.

The Places Reviews API provides limited review excerpts and associated review information.

The Yelp Insights Private Reviews API documents additional fields, including:

- `id`: Unique review identifier
- `rating`: Review star rating
- `text`: Full review text
- `time_created`: Review creation time
- `url`: Review URL
- `user.name`: Reviewer display name
- `user.image_url`: Reviewer profile image URL
- `public_response`: Business owner's response, when available

## 5. Repeatability

**Manual Testing:** I reopened the same Yelp business page and was able to access previously viewed reviews again without logging in.

This indicates that manual review access was repeatable under the tested conditions.

**Official Documentation:** Yelp Insights supports programmatic access to review data and scheduled data delivery for authorized partners.

Yelp documents API retrieval and daily/monthly JSON feeds. It also recommends regular refreshes to keep data current and account for review removals.

## 6. Sufficient Useful Text

**Manual Testing:** Full-length customer reviews were accessible without authentication. It contains potentially useful text for sentiment analysis.

**Official Documentation:**

- Yelp Places API provides limited review excerpts, which may be insufficient for comprehensive text analysis.
- Yelp Insights Private Reviews API supports full-text reviews for authorized partners.
- Yelp Open Dataset contains historical review text suitable for certain academic research purposes.

## 7. Login / CAPTCHA / Verification

**Manual Testing:**

- **Login:** Not required to view full-length reviews.
- **CAPTCHA:** Not encountered.
- **Additional verification:** Not encountered.
- **Pagination:** Additional review pages were accessible without authentication.
- **Repeated access:** Previously viewed reviews remained accessible when the business page was reopened.

**Official API Documentation:**

- Yelp Places API requires an API key.
- Yelp Insights requires additional partner permissions and account configuration.
- Some partner operations use OAuth or other partner-specific authentication methods.
