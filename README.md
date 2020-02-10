
# Dashboard
https://gazetm.com

Gazet Team provides authentication information for publisher dashboard once partnership has approved.
Our partners are able to check assigned offers and brief report ( revenue, conversions ).


# API Document

This document represent usage of Gazet NCPI - Publisher API.
Make sure that you have granted to access service.
Every endpoint should have client id and secret code on Http Header. 
If not, please contact Gazet team to get those codes.

## Try out
[https://api.gazetm.com/swagger-ui.html#/Offers/listZippedUsingGET](https://api.gazetm.com/swagger-ui.html#/Offers/listZippedUsingGET)

We provide try out web page for previewing.

## Offer List

This endpoint returns every offers which are assigned for you.

### Request
- url : [https://api.gazetm.com/v2/offer/list](https://api.gazetm.com/v2/offer/list)
- method : GET
- header : 

   key            |type                          | mandatory | description 
	----------------|-----------------------| -------------|-----------------------------
	 client_id 			| string           | Yes | must issued by gazet team 
	 client_secret	| string           | Yes | must issued by gazet team 
- parameters : None

### Response

Response body formed like below JSON string.

 field | type | nullable | description 
------|-------|----------|-------------
 offerId | string | False | offer unique identification 
 offerName | string | False | Short title of offer  
 description | string | True | Detail description about offer 
 platform | string | False | Target Platform `Android / iOS / Etc` 
 region | string | False | Target Region (eg - KR, US, JP ) 
 previewUrl | string | False | Final landing url of campaign 
 clickUrl | string | False | Offer specific click URL <br> https://clk.gazetlink.com/TestOf?pd={sub_pub_id}&g={gaid}&i={idfa}&tx={transaction_id} <br> {sub_pub_id} - sub publisher id <br> {gaid} - Google Advertising ID (Device Id if not available) <br> {idfa} - Identifier for Advertisers <br> {transaction_id} - your click id 
 creative | JSON array | False | JSON item field <br> url - creative downloadable url <br> creativeType - `image,video,etc` <br> resolution - `width`x`height` 
 payout | number | False | payout amount of approved conversion 
 currency | string | False | payout currency (eg - USD, KRW ) 
 costType | string | False | payout action `CPI / CPA / CPM`
 capping | JSON | True | Capping per specific period <br> `daily / weekely / monthly` <br> usually daily capping assigned <br><br> null or 0 means unlimited 
 kpi | JSON | False | hard - hard kpi of campaign <br> soft - soft kpi of campaign 
 traffic | JSON | True | include - prefer source <br> exclude - source to avoid 
 startTimestamp | number | True | start timestamp of campaign 
 endTimestamp | number | True | start timestamp of campaign 
 startDate | string | True | start date time 
 endDate | string | True | end date time 

#### example
```
[
  {
    "offerId": "TestOf",
    "offerName": "Gazet_Offer_AOS_KR",
    "description": null,
    "platform": "Android",
    "region": "KR",
    "previewUrl": "https://play.google.com/store/apps/details?id=com.gazetfactory.ncpiapp",
    "clickUrl": "https://clk.gazetlink.com/TestOf?pd={sub_pub_id}&g={gaid}&i={idfa}&tx={transaction_id}",
    "creativeType": null,
    "creative": [
      {
        "url": "https://cdn.gazetfactory.com/RhCeCU/0f4ffaf7-8a34-408f-bdb0-db30f2871701",
        "creativeType": image,
        "resolution": "1024x768"
      },
      {
        "url": "https://cdn.gazetfactory.com/RhCeCU/d6f1a2c2-a3e8-42b7-82f1-c3d355defb11",
        "creativeType": image,
        "resolution": "1040x585"
      }
    ],
    "payout": 0.66,
    "currency": "USD",
    "costType": "CPI",
    "capping": {
      "daily": 50
    },
    "kpi": {
      "hard": "1. D0 Veiw rate 300% below  (least 1 daily installs/sub-pub)\n2. Fraud traffic\n- If there is no download time stamp value\n- Country : other than KR\n- Language : other than 한국어 (means Korean)\n- CTIT < 10 sec\n- Carrier : other than KT, LG U+, SKTelecom\n- Abnormal Traffic can be proven - Customer User ID, App/OS/SDK version(mismatch), weird Device Download Time (checked in P360)",
      "soft": "-Veiw rate over 500%, ITCT(Install to Call) over 5 minutes\n-Campaign will be optimized based on P360"
    },
    "traffic": {
      "include": "",
      "exclude": "No Free-Recharge apps traffic / No SMS, Email / No Adult traffic / No Bot Traffic (No repeated IP) / No incent / No SNS, Facebook traffic / No Google / No 4shared / No Appwall traffic / No Traffic from ilbe.com or womad.life  / No re-brokering/ No brand bi"
    },
    "startTimestamp": null,
    "endTimestamp": null,
    "startDate": null,
    "endDate": null
  }
]
```
