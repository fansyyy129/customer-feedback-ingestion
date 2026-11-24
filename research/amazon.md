Amazon

Accessibility: Tested Amazon review access while logged out. The review content was inaccessible, and login was required to access whole reviews. This does not establish permission for automated data collection. After logging in, I was able to access full-length customer reviews and load additional reviews.

Pagination: 
In my manual test, approximately 10 reviews were displayed at a time. I could click "Show 10 more reviews" to load additional reviews. 
This suggests that the website supports incremental review loading through its interface. However, this mechanism might affect automated retrieval.
 
Available Fields (After authentication)
•	Individual reviews: Full review text, star ratings, review titles, dates, product variations, verified purchase labels, and helpful votes.
•	Review navigation: A search function, sorting options, and filters for star ratings, product variations, reviewer types, and content formats.
•	Aggregated feedback: Overall ratings, star-rating distributions, and AI-generated summaries of common positive and negative themes.
•	Multimedia content: Customer-uploaded photos and videos associated with reviews.

Repeatability: During manual testing, I was able to access multiple customer reviews and load additional reviews after logging in. However, automated retrieval has also not been tested.

Sufficient Useful Text: Amazon reviews contain potentially useful customer-generated text for sentiment analysis, including product feedback, positive and negative experiences, and recurring complaints. The ability to load additional reviews suggests that multiple reviews can be accessed through the website.

Official API: https://developer-docs.amazon/sp-api/
Amazon offers Customer Feedback API through its Selling Partner API (SP-API). Access requires appropriate developer/application permissions and seller or vendor authorization. Public visibility of reviews does not establish permission for automated scraping or commercial reuse.
The API provides structured review-topic insights, customer snippets, and aggregated trends. Documented data includes ASIN identifiers, positive and negative topics, mention metrics, rating impact, and review snippets. The API supports programmatic requests, has published rate limits, and refreshes its underlying data weekly.

Login/ CAPTCHA/ verification: A login requirement was observed. No CAPTCHA or additional verification challenge was encountered during my manual test (might have one in other attempts next time).


<img width="468" height="621" alt="image" src="https://github.com/user-attachments/assets/a546a9fd-684d-468c-9882-33254f854bce" />
