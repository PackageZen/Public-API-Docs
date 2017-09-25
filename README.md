# Package Zen Public API Docs
Public API Documentation for People and Group Data Uploads to Package Zen

## How to Upload Organization Data to Package Zen:

Depending on whether you are testing or in production, you should use the correct ROOT_URL: 
- Development: https://staging.packagezen.com
- Production: https://api.packagezen.com

### What Protocol should I use when uploading my file?
In order to allow for different file types, the API endpoint uses the multipart Content Type (```Content-Type: multipart/form-data;```). Please make sure to follow this protocol when you are uploading your file.

### Which headers should I pass in?
In order to identify which organization to associate your upload with, we require the X-Org-Token header.  In addition, in order for us to know which API version you are pointing to, you will need to pass the Accept header.
1) ````X-Org-Token```` (This will be provided to you by the Package Zen team)
2) ````Accept application/vnd.packagezen.v1```` 

### Which parameters should I pass in?
All you need to pass to use is the file that you are uploading, withe the mentioned name:
1) ````uploaded_file```` (This is where your data file will reside. Please make sure that it is valid JSON within the file.)

### Submission Guidelines
Depending on which data you are uploading, you should use one of these endpoint respectively.

##### Uploading Groups Data

````POST /api/organizations/upload_groups````

##### Uploading People Data 

````POST /api/organizations/upload_people````

#### Success-Response
Upon successful upload, we issue a status code of 200 with a JSON payload of: 

```` {message: 'Saved successfully'}````

#### Error-Response
If any errors occur, then we will reply with a 400-499 error code depending on the error reason, with a JSON Payload of:

```` {error: "Your JSON could not be parsed."} ````

#### Curl Example
curl \
-H 'Accept: application/vnd.packagezen.v1' \
-H 'X-Org-Token: you_organization_token' \
-F uploaded_file=@single_usps.json \
--verbose http://staging.packagezen.com/api/organizations/upload_people
