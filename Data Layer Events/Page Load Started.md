# Page Load Started

This event is set as soon as the information contained within is available to the site/application. Set all values as applicable. When creating page names for your site, follow the considerations below:

**pageType naming convention:**
* Homepage = homepage
* Product Details Pages = product details
* Category Pages = product category
* Product Listing Pages = product listing
* Account Pages = account
* Promotions = promotions
* Locations = locations
* Knowledge Hub Content = knowledge hub
* Login Page = login
* Cart/Checkout Process = cart
* Anything else = other

---

## Javascript Code

```javascript
appEventData || [];
appEventData.push({
  "event": "Page Load Started",
  "page": {
    "pageCategory": "<pageCategory>",
    "pageType": "<pageType>",
    "siteLanguage": "<siteLanguage>",
    "pageName": "<pageName>",
    "siteName": "<siteName>",
    "searchPhrase": "<searchPhrase>",
    "codeBase": "<codeBase>"
  }
});
```

---

## Variable Definitions

| field | type | description | examples |
| :--- | :--- | :--- | :--- |
| **pageCategory** | string | General category or Site Section of the page. Top level of page hierarchy. | Home, About Us, Shop, Account, Blog, Investors |
| **pageType** | string | Describes what purpose the page serves. Often aligns with the CMS template. | Home, product detail, product listing, search results, account, cart, etc. |
| **siteLanguage** | string | Language in which the site is presented ISO 639-1 code. | en-us, en-gb, ch-cn, fr-ca, fr-fr, da |
| **pageName** | string | Describes the page and its content specifically. | product - XYZ123, Mens - Tops - Sweaters, Order Confirmation |
| **siteName** | string | Common language used within the business to refer to the website. This can be specific to Country Sites. | Prospecting-EU, Prospecting-US, Member Portal, Shop-CA, Shop-US, Shop-EU |
| **searchPhrase** | string | Set with an applicable search phrase if a user lands on any page that is NOT also setting Listing Viewed. | Power Tools |
| **codeBase** | string | Indicates if the site is a ‘react’ codebase or some other codebase. | React, angular, vue, svelte, etc |
