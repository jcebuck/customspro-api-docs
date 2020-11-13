# CustomsPro API Documentation

<img alt="Header image" src="https://www.channelports.co.uk/wp-content/uploads/2020/06/GettyImages-612499184.png" height="400" align="right">

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

Once you have passed the authentication step. You can now create shipments using your account.  
POST to `/api/v1/gettoken`. Be sure to pass the authorization token as a header.  
The base request should look like:

```bash
curl --location --request POST 'https://roroclearances.co.uk/api/v1/createshipment' \
--header 'Authorization: Bearer <YOUR_TOKEN>' \
--header 'Content-Type: application/json' \
--data-raw '{...}'
```

JSON examples are shown below. For XML requests, the root node should be called `ShipmentContract`, other node names can be found in Swagger. The examples are based on the example invoices you should have received from us in another email with the link to this documentation.

### Into the UK

Example payload is shown below.

```json

{
  "IsIntoUK": true,
  "IsNCTSShipment": false,
  "CustomerReference": "string",
  "VehicleNumber": "string",
  "TrailerNumber": "string",
  "ExpectedDate": "2021-11-10T10:28:34.793Z",
  "PortCode": "string",
  "RouteUKPortCode": "string",
  "RouteNonUKPortCode": "string",
  "Consignments": [
    {
      "UKTrader": {
        "Name": "string",
        "CountryCode": "GB",
        "CountryName": "UNITED KINGDOM",
        "PostCode": "string",
        "AddressLine1": "string",
        "AddressLine2": "string",
        "Town": "string",
        "EORI": "string",
        "DefermentNumber": "string",
        "IsDirectRepresentation": true
      },
      "Partner": {
        "Name": "string",
        "CountryCode": "GB",
        "CountryName": "UNITED KINGDOM",
        "PostCode": "string",
        "AddressLine1": "string",
        "AddressLine2": "string",
        "Town": "string",
        "EORI": "string",
        "DefermentNumber": "string",
        "IsDirectRepresentation": true
      },
      "Declarant": {
        "Name": "string",
        "CountryCode": "GB",
        "CountryName": "UNITED KINGDOM",
        "PostCode": "string",
        "AddressLine1": "string",
        "AddressLine2": "string",
        "Town": "string",
        "EORI": "string",
        "DefermentNumber": "string",
        "IsDirectRepresentation": true
      },
      "TotalPackages": 0,
      "TotalGrossWeight": 0,
      "TotalNetWeight": 0,
      "InvoiceNumber": "string",
      "InvoiceCurrency": "GBP",
      "TotalValue": 0,
      "FreightCurrency": "GBP",
      "FreightAmount": 0,
      "Box63NonEUPercent": 0,
      "InsuranceCurrency": "GBP",
      "InsuranceAmount": 0,
      "LRN": "string",
      "CommodityContracts": [
        {
          "Product": {
            "ProductCode": "string",
            "Name": "string",
            "CommodityImportCode": "string",
            "CommodityExportCode": "string"
          },
          "GrossWeight": 0,
          "NetWeight": 0,
          "SecondQuantity": 0,
          "ThirdQuantity": 0,
          "Value": 0,
          "NumberOfPackages": 0,
          "CountryCodeOfDestination": "string",
          "HasPreference": false,
          "PreferenceType": "string",
          "PreferenceCertificateNumber": "string",
          "LicenceIdentifier": "string",
          "LicenceNumber": "string"
        }
      ]
    }
  ]
}
```

### Out of the UK

```json
{
    "IsIntoUK": false,
    "IsNCTSShipment": false,
    "CustomerReference": "MYREFERENCE1",
    "VehicleNumber": "ABC123T",
    "TrailerNumber": "9898UY",
    "ExpectedDate": "2020-11-14T16:20:34.991Z",
    "PortCode": "DOVER",
    "RouteUKPortCode": "string",
    "RouteNonUKPortCode": "string",
    "AttachmentContracts": [
        {
        "Name": "string",
        "Attachment": "dGVzdA=="
        }
    ],
    "Consignments": [
        {
            "UKTrader": {
                "Name": "ENGINE COMPANY",
                "CountryCode": "GB",
                "CountryName": "United Kingdom",
                "PostCode": "CV99 9ZZ",
                "AddressLine1": "123 STREET LANE",
                "AddressLine2": "string",
                "Town": "COVENTRY",
                "EORI": "GB243512587000",
                "PaymentCode": "B",
                "DefermentNumber": "string",
                "IsDirectRepresentation": true
            },
            "Partner": {
                "Name": "GRANDE AERO SRL",
                "CountryCode": "IT",
                "CountryName": "Italy",
                "PostCode": "622550",
                "AddressLine1": "VIA MINIRELI",
                "AddressLine2": "string",
                "Town": "NAPOLI",
                "EORI": "string",
                "IsDirectRepresentation": true
            },
            "Declarant": {
                "Name": "CHANNELPORTS LTD",
                "CountryCode": "GB",
                "CountryName": "United Kingdom",
                "PostCode": "CT21 4BL",
                "AddressLine1": "FOLKESTONE SERVICES",
                "AddressLine2": "JUNCTION 11 M20",
                "Town": "HYTHE",
                "EORI": "GB683470514000",
                "IsDirectRepresentation": true
            },
            "TotalPackages": 1,
            "TotalGrossWeight": 150,
            "TotalNetWeight": 150,
            "InvoiceNumber": "EX5555222",
            "InvoiceCurrency": "USD",
            "TotalValue": 2200,
            "FreightCurrency": "USD",
            "FreightAmount": 0,
            "Box63NonEUPercent": 0,
            "InsuranceCurrency": "USD",
            "InsuranceAmount": 0,
            "LRN": "string",
            "CommodityContracts": [
                {
                    "Product": {
                        "ProductCode": "65200000",
                        "Name": "ENGINE STAND",
                        "CommodityImportCode": "string",
                        "CommodityExportCode": "73259990"
                    },
                    "GrossWeight": 150,
                    "NetWeight": 150,
                    "SecondQuantity": 0,
                    "ThirdQuantity": 0,
                    "Value": 2200,
                    "NumberOfPackages": 0,
                    "CountryCodeOfDestination": "IT",
                    "LicenceIdentifier": "string",
                    "LicenceNumber": "string"
                }
            ]
        }
    ]
}
```

## Required Fields

* Boolean values’ default to false when omitted. If required to be true you will need to specify them.
* CustomerReference is required and has a max length of 16 characters.
* VehicleNumber OR TrailerNumber must be present.
* ExpectedDate must be in the future, in the format yyyy-MM-ddTHH:mm:ss.
* There must be at least one Consignment in the request and each Consignment must have one or more CommodityContracts (up to 99).
* The sum of all Value fields of CommodityContracts must equal the TotalValue of the parent Consignment. This also applies to NumberOfPackages and TotalPackages.
UKTrader, Partner, and Declarant must be present in each Consignment. Their details are not saved separately, so if you make more than one request to the CreateShipment endpoint you will need to include these details again. I.e. they cannot be referenced by ID.
* EORI is required for UKTrader and Declarant. It should be 2 characters followed by 12 digits, e.g. GB987654312000.
* PaymentCode can be either ‘B’ or ‘C’ and is only required when there is also a DefermentNumber.
* FreightCurrency is only required when FreightAmount is present and greater than 0.
* InsuranceCurrency is only required when InsuranceAmount is present and greater than 0.
* CommodityImportCode should be 2 digits.
* CommodityExportCode should be 8 digits.
* PreferenceType and PreferenceCertificateNumber are only required when HasPreference is true.

## Common Errors

1. Attachment format  
The attachment must be a base64 encoded binary representation of the file that you pass with your request.

2. Currency Codes  
Currency codes must be in ISO 4217 format (https://www.iban.com/currency-codes).

3. Country Codes  
Country codes must be in ISO 3166 format (https://www.iban.com/country-codes).

4. EORI Number  
EORI numbers should be 2 characters followed by 12 digits, e.g. GB987654312000.


