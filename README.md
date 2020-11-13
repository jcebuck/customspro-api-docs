# CustomsPro API Documentation.

<img alt="Header image" src="https://www.channelports.co.uk/wp-content/uploads/2020/06/GettyImages-612499184.png" height="450" align="right">

## Overview

This guide is to help you get started integrating with our API. More information about the product can be found here - [What Is CustomsPro?](https://www.channelports.co.uk/what-is-customspro/).

The API supports both JSON and XML formats. Just be sure to specify the appropriate Content-Type with your requests.

Swagger documentation can be found here - https://roroclearances.co.uk/swagger/index.html. You will need to check there to find root node names if you plan to use XML.

Additional global values, used by the software, such as countries, ports, and routes can be found here - [CustomsPro Additional Information](https://docs.google.com/spreadsheets/d/1rnjnCt48oIuF_pSxEWslt95k3DMBU5Kf31FTnoaTPQo/edit?usp=sharing).

## Table of Contents

* [Authentication](#authentication)
* [Create Shipment](#create-shipment)
  * [Into the U.K.](#into-the-uk)
  * [Out of the UK](#out-of-the-uk)

## Authentication

Authentication to the API is done using a bearer token. (HTTP Header - `Authorization: Bearer <token>`).  
This can be retrieved by making a POST request to the API endpoint `/api/v1/gettoken` with your username and password.

```bash
curl --location --request POST 'https://roroclearances.co.uk/api/v1/gettoken' \
--header 'Content-Type: application/json' \
--data-raw '{
    "Username": "<YOUR_USERNAME>",
    "Password": "<YOUR_PASSWORD>"
}'
```

Or, alternatively, with an XML body instead and `application/xml` Content-Type:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<LoginContract>
<Username>????</Username>
<Password>???????</Password>
</LoginContract>
```

The response will contain your token:

```json
{
    "Token": "<YOUR_TOKEN>",
}
```

## Create Shipment

### Into the UK

### Out of the UK
