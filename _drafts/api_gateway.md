---
title: API Gateway
layout: post
tags: development
---

# Problem Statement

Yesterday we sketched a search results page we want to test.  It's the most basic version possible: CSS2, limited formatting and no JavaScript.  It will be the fallback user interface.  It will also help us exercise a public API that can be used to query records.


Right now, we don't want to mess with the production environment until we've got an alternative candidate, so we'll need to find a another way.  The original site doesn't have an API, but it responds to AJAX search requests with a HTML fragment that contains pages of records and a JavaScript fragment that contains metadata about the query.  

## Endpoints

Unfortunately, there is a different endpoint for each collection, and we want unified results in the new version.

```
- *EPPI:* /eppi/results
- *IED:* /ied/results
- *VMR:* /vmr/results
```

## Request Params

Each endpoint behaves identically, with the exception of a subset of different accepted request params.  These relate to the different characteristics of each collection.

### Common Params

There are some common params accepted by all:

```
#### Fulltext Query

- *q*: Search query text in natural language.
- qclean:

#### Sorting & Pagination

- *page*: Page or cursor position within the result set.  Default: 1.
- *per_page:*: Number of search resukts returned per page/request. Default: 10.
- *sort*: Field on which results are ordered.
- *sort_dir*: The direction in which results are ordered, asc or desc.  Default: asc
```

### EPPI Params

Maybe the search field wouln't need to be specified with appropriate weighting?

nb.  Facet IDs are reused from the EPPI collection.

```
- *fields*: One of fulltext, title, exact_title, code, paper_no.
- *from*: Range start. Year.
- *to*: Range end. Year.

#### Facets (Document Type)

- *cat[25]* Bill
- *cat[26]* Account
- *cat[31]* Command Paper
- *cat[32]* Report
```

### IED Params

At the time of writing, the date input element couldn't be used.  It would have been better to reformat the date at the client before making the request, but maybe this was simpler for progressive fallback?

The calendar functionality doesn't work or has been removed (no errors).

The facet IDs aren't sequential.  Maybe there are missing or unused facets?  nb.  Facet IDs are reused from the EPPI collection.

```
- *start[d]*: Start date.
- *start[m]*: Start month.
- *start[y]*: Start year.
- *end[d]*: End date.
- *end[m]*: End month.
- *end[y]*: End year.

#### Facets (Document Type)

- *cat[20]*: Shipping Advertisements
- *cat[22]*: Official Documents
- *cat[24]*: Emigrant Letters
- *cat[25]*: Family Papers
- *cat[26]*: Diaries and Journals
- *cat[27]*: Other Letters
- *cat[29]*: Newspaper Extracts
- *cat[30]*: Periodical Extracts
- *cat[31]*: Hansard
- *cat[32]*: Folklore, Song, Music
- *cat[33]*: Births, Deaths, Marriages
- *cat[34]*: Wills
- *cat[35]*: Shipping News
- *cat[40]*: Statistics
```

### VMR Params

```
- *vmr_gender_id*: Gender, one of ,,,, 
- *vmr_age_group*: Age Group, one of ,,,,
- *vmr_denomination_id*: Denomination, one of ,,,,,.
- *vmr_emigration_id*: Decade of emigration.
- *vmr_return_id*: Decade of return, if any.

#### Places

The following fields are indexed placenames.

- *birthplace_id*:
- *childhood_residence_id*:
- *residence_id*:
- *vmr_destination_id*:
```

# API Gateway

- API Versioning
- Access protocols: Token-based, HMAC Signed, Basic Auth, Keyless
- Analytics logging
- Blacklist/Whitelist/Ignored endpoint access
- IP Whitelisting
- Key Expiry
- Webhooks

### Rate Limiting

### Quotas

# Params Mapping

# Go

## HttpUtil Reverse Proxy

# Deployment

# Links

1. [Pattern: API Gateway / Backend for Front-End](http://microservices.io/patterns/apigateway.html)
1. [Optimizing the Netflix API](https://medium.com/netflix-techblog/optimizing-the-netflix-api-5c9ac715cf19)
1. [HttpUtil ReverseProxy](https://golang.org/pkg/net/http/httputil/#ReverseProxy)
1. [Reverse Proxy in Go](https://blog.charmes.net/post/reverse-proxy-go/)
1. [Tyk API Gateway](https://tyk.io/)







