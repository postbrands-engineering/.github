# Softbird API Clientside 

Softbird is a brazilian fintech specializing in national and crossborder instant payments.

Our technological solution for instant payments is focused on conversion and makes bureaucracy easier for companies headquartered abroad with customers in Brazil.

We are a Brazilian online payment technology company. We work to simplify financial transactions over the internet, effectively making life easier for our customers and their buyers.

We have the fastest API integration on the market and we accredit the operation of our customers in the main Brazilian banks, taking care of all the bureaucracy so that they have more time to focus on the business.

## Authentication

    You can get the token directly from the administration dashboard. https://banking.softbird.com.br/dashboard/development

## Generate invoice

### Request

`POST https://clientside.softbird.com.br/invoice/generate`

    curl -i -H 'Accept: application/json' -d 

### Response

    HTTP/1.1 201 Created
    Date: Thu, 24 Feb 2011 12:36:31 GMT
    Status: 201 Created
    Connection: close
    Content-Type: application/json
    Location: /invoice/generate
    Content-Length: 35
