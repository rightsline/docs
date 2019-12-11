# RightsLine API Transition from V2 to V3 

Change is hard... But we think you'll really love what we've done!  

We have released a new version of the RightsLine public API, aptly titled V3.
V3 was designed to increase security and flexibility of the API compared to the previous version, V2.  

Differences between V2 and V3 include:

{maybe a table of some sort...?  or just summarize changes. }

If you are currently using V2 of RightsLine's public API and would like to transition to V3, please follow the steps listed below:

1. Modify requests to use [Amazon AWS Authentication](#1-amazon-aws-authentication).
2. [Convert date fields](#2-convert-date-fields) to ISO format.
3. [Convert List-of-Value (LOV) fields](#3-convert-list\-of\-value-\(lov\)-fields)  to JSON objects, or an array of JSON objects.


## 1. Amazon AWS Authentication

With the introduction of V3 of our public API, we have transitioned to using Amazon AWS Authentication to sign all requests.  The credentials that you will need to pass with your requests will look a bit different:

### Request Temporary Credentials
Instead of sending each request with a Public Key and a Private Key, requests will need to be sent with 3 things:  a **Company API Key**, a **RightsLine Access Key**, and a **RightsLine Secret Access Key**.
 
To obtain the RightsLine Access and Secret Access Keys, you will need to make a request to obtain them.  
The request to obtain RightsLine Access and Secret keys looks as follows:

Request:
``` json 
POST /v3/auth/temporary-credentials
Accept: application/json
Content-Type: application/json
x-api-key: {Company_API_Key}
Body:
{
 "accessKey":"*************",
 "secretKey":"**************************"
}
```
Response:
``` json 
HTTP/1.1 200 OK
Date: {}
Content-Type: {}
Content-Length: {}
Body:
{
"accessKey": "***********",
"secretKey": "***************************",
"sessionToken": "FQoDYXd//////====ONCXz6OZC6FIxoWO1CGxVkwnY6WT07ZdLgGkr5ZkRCnGpa5uiF5KKbgMMWyQjKIazeyarBvXleDQmJznO4tBKq3U709cY20lVkdzHwAJQ5HXWHVop6w6cRy8uyOFPZ9fPD79PJ0L9KUkSo9uIG8DUK7PRvs4eAtIQQFdW+j2eHx6sUlF====34098qojfaof",
"expiration": "2018-01-01T00:00:01+00:00"
}
```
Your Company API Key will be provided by RightsLine.  It is shared among your organization and is unique per environment (Staging, Integration, Prod Mirror, and Production).  

[top](#rightsline-api-transition-from-v2-to-v3)

## Data Format Changes

### Date Fields
All date fields are now in ISO format.  

### Money Fields
Money data is now in JSON format. 

    "characteristics": {
        "balance": {
            "locAmt": "37500.00",
            "locCur": 1,
            "locSym": "USD",
            "divAmt": "37500.00",
            "divCur": 1,
            "divSym": "USD"
        },
        "total": {
            "locAmt": "37500.00",
            "locCur": 1,
            "locSym": "USD",
            "divAmt": "37500.00",
            "divCur": 1,
            "divSym": "USD"
        },
        "allow_full_recoupment": {
            "id": 1,
            "value": "Yes"
        }
    }
[top](#rightsline-api-transition-from-v2-to-v3)

## 3. Convert List-of-Value (LOV) Fields
