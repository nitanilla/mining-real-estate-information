# Knowledge-Graph
WordPress plugin to add Knowledge Graph meta data in LD-JSON format to &lt;head />

https://developers.google.com/structured-data/customize/overview

uses: [Admin Page Class] (https://github.com/bainternet/Admin-Page-Class)

# Bug Report
- Noticed that "TollFree" staying on in a ContactPoint (opened an issue).

#Aim 
have form to create as hand coded this example:
```
<script type="application/ld+json">
{"@context": "http://schema.org",
    "@type": "RealEstateAgent",
     "name": "Real Estate Intelligence Agency",
    "logo": "http://www.realestate-huntsville.com/wp-content/uploads/2012/12/real-estate-intelligence-agency-logo.png",
"description": " A real estate brokerage specializing in back-to-basics residential and commercial real estate sales and marketing services.",
    "address": {
     "streetAddress": "107 Clinton Ave W",
   "addressLocality": "Huntsville",
     "addressRegion": "AL",
        "postalCode": "35801",
    "addressCountry": "USA"
    },
    "telephone": "+1-256-457-0804",
      "contactPoint" : [
      { "@type" : "ContactPoint",
      "telephone": "+1-256-682-0383",
      "contactType" : "Sales and Marketing",
      "areaServed" : "US",
       "availableLanguage" : ["English", "Finnish"]
       }
       ],
      "url": "http://www.RealEstate-Huntsville.com",
  "sameAs" : ["https://www.facebook.com/RealEstateIntelligenceAgencyInc",
              "http://twitter.com/REIA007",
              "https://plus.google.com/115551206707821669279",
              "https://www.youtube.com/channel/UCJ_pqfxGw6hhSMuJxIPQHZg",
              "https://www.linkedin.com/company/real-estate-intelligence-agency"
              ]
}
</script>	
```
# ToDo
- [x] Company name
- [x] Logo
- [x] URL
- [x] Description
- [x] Social Links et al. (sameAs)
- [x] Contact info
- [x] contactPoint(s)/ContactPoint
- [ ] Lint/Validate
- [ ] Search, try and be compatiable with [Google Analytics by Yoast] (https://github.com/Yoast/wordpress-seo)
- [ ] Modify admin-page-class to validate repeater block
- [ ] Modify admin-page-class so that can delete repeater fields
