# occ-install-extensions
(examples coming soon)

## Remote ExtensionID Generation:
This below example script generates an extension ID in the [Oracle Commerce Cloud](https://cloud.oracle.com/en_US/commerce-cloud "Oracle Commerce Cloud") Admin in preparation for zip file-upload.

The admin and the ccdebug use [/applicationsId](https://ccadmin-test-zbba.oracleoutsourcing.com/api/index.html?startCatalog=ccadmin#/Applications/createApplicationID "createApplicationId") API endpoint, but this returns 403 Forbidden Errors when trying to access outside of the OCCS domain


The following uses [POST /extensions/id](https://ccadmin-test-zbba.oracleoutsourcing.com/api/index.html?startCatalog=ccadmin#/ "create extension") and also works.

### Example 
(See code for working example)
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
Use [the API](https://docs.oracle.com/en/cloud/saas/commerce-cloud/cxocc/ "Oracle Commerce Cloud REST API") to upload and install your extension(zip) to OCC

### Steps
1. Start the [file upload](https://docs.oracle.com/en/cloud/saas/commerce-cloud/cxocc/op-ccadmin-v1-files-put.html "Start File Upload").  This will tell OCCS that you want to send it a file and it will return you a token you can use in the next step.   
If you are submitting via multipart/form you will need to use the [doFileUploadMultipart](https://docs.oracle.com/en/cloud/saas/commerce-cloud/cxocc/op-ccadmin-v1-files-post.html) to generate the token

2. Begin a [segmentFileUpload](https://docs.oracle.com/en/cloud/saas/commerce-cloud/cxocc/op-ccadmin-v1-files-id-post.html "File Segment Upload") using the token you received in the previous step.
In your request client add the following query parameters:
```
?changeContext=designStudio
```

3.  Create the [extension](https://docs.oracle.com/en/cloud/saas/commerce-cloud/cxocc/op-ccadmin-v1-extensions-post.html "create extension").


