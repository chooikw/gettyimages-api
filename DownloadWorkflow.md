# Downloading Image by Asset Id found in Search Results

## Sections
1. [cURL based example](#workflow-steps)
1. [Postman collections](#postman-collections)

## Workflow Steps
1. [Get an access token from Getty Images OAuth endpoint](#get-access-token)
1. [Use access token to search for images with largest download returned](#search-for-images-w-largest-downloads-field-specified)
1. [Download an image from the results](#download-the-image-using-its-asset-id-and-product-type)

### Get Access Token
In order to get download links from search you will need to use a [Resource Owner Request](OAuth-Workflow#resource-owner-flow) as used in the example below

Alternatively, a token retrieved via a [Client Credentials Request](OAuth-Workflow#client-credentials-flow) with a Sandboxed Api-Key, will also allow for downloading of a static image for testing purposes. NOTE: This static test image is not the actual asset image.

####Request
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'grant_type=password&client_id=exampleApiKey&client_secret=exampleSecret&username=someUsername&password=WithSomePassword' https://api.gettyimages.com/oauth2/token

#### Response

    {
      "access_token": "123456",
      "token_type": "Bearer",
      "expires_in": "1800"
    }

### Search For Images with Largest Downloads field specified
####Request
    curl -X GET -H "Authorization: Bearer 123456" -H "Api-Key: exampleApiKey"  https://api.gettyimages.com/v3/search/images?phrase=Kitties&fields=largest_downloads

####Response

    {
      "result_count": 3662,
      "images": [{
        "id": "83454804",
        "largest_downloads": [{
          "product_type": "easyaccess",
          "uri": "https://api.gettyimages.com/v3/downloads/images/83454804"
          }]
      },{
        "id": "103131833",
        "largest_downloads": [{
          "product_type": "editorialsubscription",
          "uri": "https://api.gettyimages.com/v3/downloads/images/103131833"
          }]
        }]
      }
    }

### Download the image using its asset id and product type
The largest_downloads array for each image in the response above gives a URI to be used to download the image, as well as the product  for which you are authorized to download.  To download the image file, create a POST request to the URI and indicate the product_type as a query string parameter as in the example below.  The default response to that request is to return the URI where you can download the actual image.  If you also set an auto_download parameter to “true”, this will execute a 302 redirect which automatically downloads the image file.

####Request
    curl -X POST -H "Api-Key: exampleApiKey" -H "Authorization: Bearer 123456" -d '' https://api.gettyimages.com/v3/downloads/images/83454804?auto_download=false&product_type=easyaccess

####Response
    {
      "uri": "https://delivery.gettyimages.com/xa/83454804.jpg?....."
    }

### Postman Collections
If you prefer to use [Postman](https://www.getpostman.com/), we have created collections that can be reused to execute the workflow outlined above.

1. [OAuth Collection](https://raw.githubusercontent.com/gettyimages/gettyimages-api-postman/master/OAuthCollection.json)
1. [Search Collection](https://raw.githubusercontent.com/gettyimages/gettyimages-api-postman/master/SearchCollection.json)
1. [Download Collection](https://raw.githubusercontent.com/gettyimages/gettyimages-api-postman/master/DownloadCollections.json)