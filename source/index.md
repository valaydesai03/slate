---
title: OTAS Base API V1.0

language_tabs:
  - C#
  

toc_footers:

includes:

search: true
---

# Introduction

Welcome to the OTAS Base API. The OTAS Base API is organized around REST. Our API is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which can be understood by off-the-shelf HTTP clients, and we support cross-origin resource sharing to allow you to interact securely with our API from a client-side web application (though you should remember that you should never expose your secret API key in any public website's client-side code). JSON will be returned in all responses from the API, including errors (though if you're using API bindings, we will convert the response to the appropriate language-specific object).

You can use our API to access OTAS Base API endpoints, which can get information on identifiers, stocks, daily and intraday flags in our database.

# Authentication
> Make sure to replace `meowmeowmeow` with your API key.

OTAS uses API key to allow access to the API.

OTAS expects for the API key to be included in all API requests to the server in a header that looks like the following:

`?apikey=meowmeowmeow`

<aside class="notice">
You must replace `meowmeowmeow` with your personal API key.
</aside>

# Versioning
When we make backwards-incompatible changes to the API, we release new dated versions. The current version is 1.0.

# Metadata
Details of metadata

#Identifier Methods

##Get ISIN 
`GET /api/data/v1/isin/:isin/`
>Example Request 

```
/api/data/v1/isin/:isin/?apikey=meowmeowmeow
```

>Example Response Headers 

```
{
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "server": "Microsoft-IIS/7.5",
    "date": "Sat, 02 Aug 2014 06:05:14 GMT",
    "content-length": "65"
}
```

>Example Response Body (Valid ISIN)

```
{
    "isin": "isincode",
    "otasSecurityId": "otassecurityid",
    "type": "isin"
}
```

>Example Response Body (Invalid ISIN)

```
{
    "message": "OTAS SecurityId not found for ISIN\"invalid ISIN code\""
}
```

> Make sure to replace `meowmeowmeow` with your API key and :isin is valid code of ISIN.


Gets the ISIN object according to the supplied ISIN code.

###Returns: ISIN Object

Property | Type | Description
---------| ------- | -----------
isin | string | The ISIN code.
otasSecurityId | string | The OTAS security identifier
type | string | 

###Parameter(s):

Parameter | Type | Location | Description
---------| ------- | ------- | ------------
isin | string | query | The ISIN code.

###Verification Responses:

Response Code | Description
--------------| ------------
200           | Valid ISIN
400           | Invalid ISIN
	

#Stock Methods

## Get Stock
`GET /api/data/v1/stock/:otasSecurityId/`
>Example Request 

```
/api/data/v1/stock/:otasSecurityId/?apikey=meowmeowmeow
```

>Example Response Headers 

```
{
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "server": "Microsoft-IIS/7.5",
    "date": "Sat, 02 Aug 2014 06:33:26 GMT",
    "content-length": "1221"
}
```

>Example Response Body (Valid otasSecurityId)

```
{
    "otasSecurityId": "OT.VOD.S",
    "name": "Vodafone Group",
    "description": "Vodafone Group Plc (Vodafone), is a mobile communications company. Vodafone Red offers consumers and businesses a package with mobile data allowances, unlimited calls and texts, plus cloud and back-up services to secure personal data. Vodafone Cloud allows customers to store their personal digital content, such as contacts, photos and videos in the Vodafone network and to access it on the move from any connected device. Vodafone OneNet integrates landlines and mobiles providing a communication solution. Vodafone Secure Device Manager gives customer a way to manage many of their smart devices. In February 2014, Verizon Communications Inc completed the acquisition of Vodafone Group Plc's 45% indirect interest in Verizon Wireless. In April 2014, Vodafone Group Plc acquired100 %of its Indian subsidiary, Vodafone India Limited (VIL).",
    "country": "UNITED KINGDOM",
    "sector": "Telecommunication Services",
    "industry": "Telecommunication Services",
    "subIndustry": "Wireless Telecommunication Services",
    "currency": "GBp",
    "dividendCurrency": "GBp       ",
    "marketCapLocal": 52054520000,
    "marketCapUSD": 87654590000,
    "marketCapEuro": 65276220000,
    "type": "stock"
}
```

>Example Response Body (Invalid otasSecurityId)

```
{
    "message": "Error: An OTAS security symbol is of the form OT.<Issuer>.<Instrument>, where Instrument is 'S', 'E', or 'F' for stock, exchange traded fund, or foreign fund."
}
```

> Make sure to replace `meowmeowmeow` with your API key and :isin is valid code of ISIN.


Gets the stock object according to the supplied otas symbol. Use this method to get static data associated with a certain stock such as sector, country, currency etc. If you need to retrieve the data but have a different identifier, use the other methods earlier in this document to get the corresponding OTAS symbol. 

###Returns: Stock Object

Property | Type | Description
---------| ------- | -----------
otasSecurityId | string | The OTAS security identifier
name | string | The name of the company that issued the stock
description | string | Description of the company's business
country | string | The company's country per Thomson Reuters, typically where the company is headquartered
sector | string | The company's industrial sector (GICS Level 2)
industry | string | The company's specific industry (GICS Level 3)
subIndustry | string | The company's sub-industry (GICS Level 4)
currency | string | The currency with which most shares are traded, typically where the company is headquartered; the principal currency
dividendCurrency | string | The currency with which dividends are paid
marketCapLocal | float | The company's market capitalization in millions of units of the principal currency as of the last trading day
marketCapUSD | float | The company's market capitalization in millions of US dollars as of the last trading day
marketCapEuro | float | The company's market capitalization in millions of Euros as of the last trading day
type | string | 

###Parameter(s):

Parameter | Type | Location | Description
---------| ------- | ------- | ------------
otasSecurityId | string | query | The OTAS security identifier

###Verification Responses:

Response Code | Description
--------------| ------------
200           | Valid otasSecurityId
400           | Invalid otasSecurityId

#List Management Methods

## Get List
`GET /api/data/v1/lists`
>Example Request 

```
/api/data/v1/lists?type=typeoflist&apikey=4D69167EF59EAC183AE1845A2D7EB
```

>Example Response Headers 

```
{
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "server": "Microsoft-IIS/7.5",
    "date": "Sat, 02 Aug 2014 08:05:44 GMT",
    "content-length": "8908"
}
```

>Example Response Body (Valid type of list)

```
[
    {
        "securityListId": 1,
        "securityListName": "AEX (Amsterdam)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 41,
        "securityListName": "ASX100 (Australia)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 51,
        "securityListName": "ASX200 (Australia)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 52,
        "securityListName": "ASX50 (Australia)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 37,
        "securityListName": "ATX 20 (Austria)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 35,
        "securityListName": "Bolsa IPC (Mexico)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 36,
        "securityListName": "Bovespa (Brazil)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 19,
        "securityListName": "BSE 200 (India)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 2,
        "securityListName": "CAC 40 (France)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 7,
        "securityListName": "DAX 30 (Germany)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 12,
        "securityListName": "DJ Industrials (US)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 48,
        "securityListName": "Europe ex UK",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 3,
        "securityListName": "FTSE 100 (UK)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 6,
        "securityListName": "FTSE 250 (UK)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 53,
        "securityListName": "FTSE 350 (UK)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 55,
        "securityListName": "FTSE Bursa Malaysia KLCI",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 4,
        "securityListName": "FTSE MIB (Italy)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 54,
        "securityListName": "FTSE Taiwan 50",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 22,
        "securityListName": "HSCCI Index (Hong Kong)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 21,
        "securityListName": "HSCEI Index (China)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 59,
        "securityListName": "HSCI Index (Hong Kong)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 20,
        "securityListName": "HSI Index (Hong Kong)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 60,
        "securityListName": "HSM 100 (Hong Kong)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 5,
        "securityListName": "IBEX 35 (Spain)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 45,
        "securityListName": "ISE30 (Turkey)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 57,
        "securityListName": "Jakarta LQ-45",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 56,
        "securityListName": "KOSPI 200",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 38,
        "securityListName": "Luxxx 11 (Luxembourg)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 11,
        "securityListName": "NASDAQ 100 (US)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 46,
        "securityListName": "Nikkei 225",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 14,
        "securityListName": "OBX (Norway)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 15,
        "securityListName": "OMX 25 (Finland)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 13,
        "securityListName": "OMX 30 (Sweden)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 39,
        "securityListName": "OSE (Norway)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 40,
        "securityListName": "PS120 (Portugal)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 42,
        "securityListName": "PSE (Philippines)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 44,
        "securityListName": "RTS (Russia)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 33,
        "securityListName": "Russell 1000 (US)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 50,
        "securityListName": "Russell 2000 (US)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 8,
        "securityListName": "S&P 500 (US)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 58,
        "securityListName": "SE Thai 50",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 18,
        "securityListName": "SENSEX (India)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 49,
        "securityListName": "SMI 20 (Switzerland)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 43,
        "securityListName": "STI (Singapore)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 9,
        "securityListName": "STOXX 50 (Europe)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 10,
        "securityListName": "STOXX 600 (Europe)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 47,
        "securityListName": "Topix 30",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    },
    {
        "securityListId": 34,
        "securityListName": "Toronto 60 (Canada)",
        "securityListType": "MarketIndex",
        "securityListIsPublic": true,
        "securityListOwnerName": "Shared",
        "type": "securityListIdentifier"
    }
]
```

>Example Response Body (Invalid type of list)

```
{
    "message": "List type 'hello' is not recognized or currently supported. "
}
```

> Make sure to replace `meowmeowmeow` with your API key and :isin is valid code of ISIN.


Returns the lists to which the logged-in user has access 

###Returns: Security List Identifier object array

Property | Type | Description
---------| ------- | -----------
securityListId | integer | The integer primary key of the subject security list
securityListName | string | The name of the subject security list
securityListType | string | The name of the subject security list: WatchList, Portfolio, OrderList, MarketIndex, RegionalIndex, or IndustryIndex
securityListIsPublic | boolean | Indicates whether the list will be shared (read-only) with other members of the user's user group
securityListOwnerName | string | The name of the user who owns the list, the only user who can edit the list
type | string | 

###Parameter(s):

Parameter | Type | Location | Description
---------| ------- | ------- | ------------
type | string | query | Optional filter to return only lists of type: 'watchlist', 'portfolio', 'orderlist', 'marketindex', 'regionalindex', or 'industryindex'. If omitted, all available lists are returned. If present, specify using the query string, e.g. '...lists?type=MarketIndex'.

###Verification Responses:

Response Code | Description
--------------| ------------
200           | Valid type of list
400           | Invalid type of list


