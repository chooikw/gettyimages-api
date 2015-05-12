# From 0 to Search Results in 5 minutes

## Workflow
1. [Sign Up](https://developer.gettyimages.com/member/register) for an Api-Key and Secret
1. Make a request against the search endpoint with your query phrase

For the example below our Api-Key will be j878g39yx378pa77djthzzpn.

##Search for images by Phrase
You can search through our images with your Api-Key.

###Quick Things to Know
* An Api-Key can be retrieved from [Developer Registration Portal](https://developer.gettyimages.com/member/register)
* Protect your information: Do not post credentials against the endpoints without using SSL!

Curl Command:

`curl -X GET -H "Api-Key: j878g39yx378pa77djthzzpn" https://api.gettyimages.com/v3/search/images?phrase=kitties`  

JSFiddle Example: [http://jsfiddle.net/cmacpherson/6g9qtbtc](http://jsfiddle.net/cmacpherson/6g9qtbtc)

Example Response:

    {
      "result_count":100,
      "images":[
        {
          "id": "83454804",
          "asset_family": "creative",
          "caption": null,
          "collection_code": "DV",
          "collection_id": 13,
          "collection_name": "Digital Vision",
          "display_sizes": [
            {
              "is_watermarked": false,
              "name": "thumb",
              "uri": "http://cache1.asset-cache.net/xt/83454804.jpg?v=1&g=fs1|0|DV|54|804&s=1&b=MkUw"
            }
          ],
          "license_model": "royaltyfree",
          "max_dimensions": {
            "height": 3682,
            "width": 4800
          },
          "title": "Portrait of group of kittens"
        }
      ]
    }

Request Details:

| Request Part | Value |
|---|---|
| Method | GET |
|Path| /v3/search/images|
| HOST| api.gettyimages.com|

| Query Param | Value |
|---|---|
| phrase | kitties|

| Header| Value |
| --- | --- |
| Api-Key | j878g39yx378pa77djthzzpn |
