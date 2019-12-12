# RightsLine API Transition from V2 to V3 

Change is hard... But we think you'll really love what we've done!  

We have released a new version of the RightsLine public API, aptly titled V3.
V3 was designed to increase security and flexibility of the API compared to the previous version, V2.  

Differences between V2 and V3 include:

{maybe a table of some sort...?  or just summarize changes. }

If you are currently using V2 of RightsLine's public API and would like to transition to V3, please follow the steps listed below:

#### Steps to transition from RightsLine API V2 to V3
1. Modify requests to use [Amazon AWS Authentication](#amazon-aws-authentication).
2. [Convert date fields](#convert-date-fields) to ISO format.
3. [Convert List-of-Value (LOV) fields](#convert-list-of-value-lov-fields)  to JSON objects, or an array of JSON objects.
4. [Convert search responses](#convert-search-responses) to new format.

## Amazon AWS Authentication

With the introduction of V3 of our public API, we have transitioned to using Amazon AWS Authentication to sign all requests.  The credentials that you will need to pass with your requests will look a bit different.

#### Generating Access Keys

Start by generating your API Access Keys:

1. **Contact your RightsLine representative** for your organization's *V3 API Key*.
2. **Login to your user account** from https://admin.rightsline.com.
3. Open your **Profile** from the drop-down menu, and in the *API Access* module, click **Generate Access Keys**.

![Test](../images/auth.png)

> **Note:** You will use these keys to request temporary access keys to authenticate to the API.  These keys are private.  Please store them securely.

#### Requesting Temporary Credentials

Use the `API Key`, `Access Key`, and `Secret Access Key` to request your temporary API credentials.  The request will look like:

``` json 
POST /v3/auth/temporary-credentials
Accept: application/json
Content-Type: application/json
x-api-key: [API_KEY]
Body:
{
 "accessKey":"[ACCESS_KEY]",
 "secretKey":"[SECRET_ACCESS_KEY]"
}
```
A successful response:
``` json 
HTTP/1.1 200 OK
Body:
{
"accessKey": "***********",
"secretKey": "***************************",
"sessionToken": "FQoDYXd//////====ONCXz6OZC6FIxoWO1CGxVkwnY6WT07ZdLgGkr5ZkRCnGpa5uiF5KKbgMMWyQjKIazeyarBvXleDQmJznO4tBKq3U709cY20lVkdzHwAJQ5HXWHVop6w6cRy8uyOFPZ9fPD79PJ0L9KUkSo9uIG8DUK7PRvs4eAtIQQFdW+j2eHx6sUlF====34098qojfaof",
"expiration": "2018-01-01T00:00:01+00:00"
}
```

The credentials that you receive in the response will be used for all subsequent requests to the RightsLine API.  These credentials have an expiration of 1 hour after they are requested.  Once these credentials expire, you will need request another set of credentials.

#### Making a Request

Requests to the API will now include the following headers:

- `X-Api-Key` - Your organization's V3 API Key
- `X-Amz-Security-Token` - The "sessionToken" from the response in the previous step.
- `X-Amz-Date` - The ISO-8601 formatted date and time of the request. ex. 20190124T015900Z
- `Authorization` - The AWS Signature Version 4 authorization token.  To generate the authorization token, see: https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html

A sample request to create a new catalog-item:

``` json
POST /v3/catalog-item
X-Api-Key: [API_KEY]
X-Amz-Security-Token: FQoDYXd//////====ONCXz6OZC6FIxoWO1CGxVkwnY6WT07ZdLgGkr5ZkRCnGpa5uiF5KKbgMMWyQjKIazeyarBvXleDQmJznO4tBKq3U709cY20lVkdzHwAJQ5HXWHVop6w6cRy8uyOFPZ9fPD79PJ0L9KUkSo9uIG8DUK7PRvs4eAtIQQFdW+j2eHx6sUlF====34098qojfaof
X-Amz-Date: 20190124T015900Z
Authorization: AWS4-HMAC-SHA256 Credential=ASIAQGIY6FPQGYYQBEXU/20191212/us-east-1/execute-api/aws4_request, SignedHeaders=host;x-amz-date;x-amz-security-token;x-api-key, Signature=791afe433715f22df25973ece9c22f23cd53be71f20eda7abf6e745e0a163f17
Body:
{
    "title": "TEST SEASON 99",
    "template": {
        "templateId": 11,
        "templateName": "Season"
    },
    "status": {
        "statusId": 1,
        "statusName": "Active"
    }
}
```

[top](#rightsline-api-transition-from-v2-to-v3)

## Convert Date Fields

[top](#rightsline-api-transition-from-v2-to-v3)

## Convert List-of-Value (LOV) Fields

[top](#rightsline-api-transition-from-v2-to-v3)

## Convert Search Responses

[top](#rightsline-api-transition-from-v2-to-v3)
