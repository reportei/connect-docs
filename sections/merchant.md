Campfires
=========

Endpoints:

- [Show current merchant settings](#merchant-settings)

Show current merchant settings
-------------

* `GET /merchants/settings` will return a list of all active Integrations available for the current merchant, as well as other settings, such as rate limit.

###### Example JSON Response
<!-- START GET /merchants/settings -->
```json
{
    "merchant": {
        "uuid": "c1e6c85a-6441-4107-ab36-b8bf581b40e0",
        "name": "Reportei",
        "app_url": "https://reportei.com",
        "redirect_url": "https://reportei.com",
        "created_at": "2024-09-24 17:07:26",
        "updated_at": "2024-09-24 17:07:26",
        "rate_limit_per_minute": "999",
        "rate_limit_per_second": "999",
        "total_customers": 2,
        "available_integrations": [
            {
                "name": "Instagram Business",
                "slug": "instagram_business"
            },
            {
                "name": "Facebook",
                "slug": "facebook"
            },
            {
                "name": "Meta Ads",
                "slug": "facebook_ads"
            },
            {
                "name": "Google Analytics",
                "slug": "google_analytics"
            },
            {
                "name": "Google Analytics 4",
                "slug": "google_analytics_4"
            },
            {
                "name": "Google Ads",
                "slug": "google_adwords"
            },
            {
                "name": "Twitter",
                "slug": "twitter"
            },
            {
                "name": "Twitter Ads",
                "slug": "twitter_ads"
            },
            {
                "name": "YouTube",
                "slug": "youtube"
            },
            {
                "name": "LinkedIn",
                "slug": "linkedin"
            },
            {
                "name": "LinkedIn Ads",
                "slug": "linkedin_ads"
            },
            {
                "name": "RD Station Marketing",
                "slug": "rdstation"
            },
            {
                "name": "Google Search Console",
                "slug": "search_console"
            },
            {
                "name": "Google My Business",
                "slug": "google_my_business"
            },
            {
                "name": "Mailchimp",
                "slug": "mailchimp"
            },
            {
                "name": "Hotmart",
                "slug": "hotmart"
            },
            {
                "name": "TikTok",
                "slug": "tiktok"
            },
            {
                "name": "TikTok Ads",
                "slug": "tiktok_ads"
            },
            {
                "name": "Pinterest",
                "slug": "pinterest"
            },
            {
                "name": "Pinterest Ads",
                "slug": "pinterest_ads"
            },
            {
                "name": "Pipedrive",
                "slug": "pipedrive"
            },
            {
                "name": "Active Campaign",
                "slug": "active_campaign"
            },
            {
                "name": "Phonetrack",
                "slug": "phonetrack"
            },
            {
                "name": "RD Station CRM",
                "slug": "rd_crm"
            },
            {
                "name": "HubSpot Marketing",
                "slug": "hubspot_marketing"
            },
            {
                "name": "HubSpot CRM",
                "slug": "hubspot_crm"
            },
            {
                "name": "Egoi",
                "slug": "egoi"
            },
            {
                "name": "Shopify",
                "slug": "shopify"
            },
            {
                "name": "Google Sheets",
                "slug": "google_sheets"
            },
            {
                "name": "WooCommerce",
                "slug": "woo_commerce"
            },
            {
                "name": "NuvemShop",
                "slug": "nuvem_shop"
            }
        ]
    }
}
```
<!-- END GET /chats.json -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://integrations.reportei.com/merchants/settings
```
