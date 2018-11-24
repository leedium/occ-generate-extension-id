# occ-generate-extensions
(examples coming soon)

## Remote ExtensionID Generation:
This below example script generates an extension ID in the [Oracle Commerce Cloud](https://cloud.oracle.com/en_US/commerce-cloud "Oracle Commerce Cloud") Admin in preparation for zip file-upload.

The admin and the ccdebug use [/applicationsId](https://ccadmin-test-zbba.oracleoutsourcing.com/api/index.html?startCatalog=ccadmin#/Applications/createApplicationID "createApplicationId") API endpoint, but this returns 403 Forbidden Errors when trying to access outside of the OCCS domain


The following uses [POST /extensions/id](https://ccadmin-test-zbba.oracleoutsourcing.com/api/index.html?startCatalog=ccadmin#/ "create extension") and also works.

This Node example uses [axios](https://www.npmjs.com/package/axios) HTTP client.
```

axios(
{
  "method": "POST",
  "data": {
    "name": "{NAME_OF_YOUR_EXTENSION}",
    "type": "extension"
  },
  "url": "https://{YOUR_ADMIN_SERVER}/ccadmin/v1/extensions/id",
  "responseType": "json",
  "headers": {
    "Authorization": "Bearer {AUTHENTICATION_TOKEN}",
    "X-CCAsset-Language": "en",
    "X-CCProfileType": "applicationAccess"
    "Accept": "application/json, text/javascript, */*; q=0.01",

  }
})
  .then(res)
  .catch(err)

```

## Remote Extension uploads to OCCS Admin
(example coming soon)


## Remote Extension deactivate (needed before uninstall / removal ) 
In order to remove an extension you must first deactivate it.  
Using the Api use the following endpoint with the following payload.
```
 method: POST
 url: /ccadminui/v1/extensions/{extensionId}
 body (json): {"op":"deactivate"}
```
