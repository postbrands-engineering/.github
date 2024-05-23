# Postbrands API Clientside 

Postbrands is a brazilian fintech specializing in national and crossborder instant payments.

Our technological solution for instant payments is focused on conversion and makes bureaucracy easier for companies headquartered abroad with customers in Brazil.

We are a Brazilian online payment technology company. We work to simplify financial transactions over the internet, effectively making life easier for our customers and their buyers.

We have the fastest API integration on the market and we accredit the operation of our customers in the main Brazilian banks, taking care of all the bureaucracy so that they have more time to focus on the business.

## Authentication -> 

    You can get the token directly from the administration dashboard. 
    
-> [Click here to go to dashboard](https://banking.postbrands.com.br/dashboard/development)
## Generate invoice

### Request

`POST https://transaction.postbrands.com.br/v1/pix/invoice/generate`

`SHELL`

    curl --request POST \
     --url https://transaction.postbrands.com.br/v1/pix/invoice/generate \
     --header 'accept: application/json' \
     --header 'authorization: Bearer tokenAuth ' \
     --header 'content-type: application/json' \
     --data ' {"payer_name": "Julio Campos",
      "document": "06054778170",
      "expiration": 18600,
      "additionalInformation": "Pix gerado para pagar invoice",
      "alertClient": "Pague antes do vencimento",
      "amount": "15.30" }'
      

`PHP`

    <?php

    $curl = curl_init();

    $payload = json_encode(
        array(
            "payer_name" => "Julio Campos",
            "document" => "06054778170",
            "expiration" => 18600,
            "additionalInformation" => "Pix gerado para pagar invoice",
            "alertClient" => "Pague antes do vencimento",
            "amount" => "15.30"
        )
    );

    curl_setopt_array($curl, [
        CURLOPT_URL => "https://transaction.postbrands.com.br/v1/pix/invoice/generate",
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_ENCODING => "",
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => "POST",
        CURLOPT_POSTFIELDS => $payload,
        CURLOPT_HTTPHEADER => [
            "Accept: application/json",
            "authorization: Bearer YOURAUTHTOKEN",
            "Content-Type: application/json"
        ],
    ]);

    $response = curl_exec($curl);

    ?>
    
`NodeJS`

    const axios = require('axios');
    const invoiceParams = JSON.stringify({
        "payer_name": "Julio Campos",
        "document": "06054778170",
        "expiration": 18600,
        "additionalInformation": "Pix gerado para pagar invoice",
        "alertClient": "Pague antes do vencimento",
        "amount": "15.30"
    });

    axios.post('https://transaction.postbrands.com.br/v1/pix/invoice/generate', invoiceParams, {
        headers: {
            'Authorization': `Bearer YOURAUTHTOKEN`
        }
    })
        .then((res) => {
            console.log(res.data)
        })
        .catch((error) => {
            console.error(error)
        })

- {tokenAuth} -> Get on integration dashboard.
- {payer_name} -> The name and surname of the player where the pix will be generated and the code shown.
- {document} -> The customer's CPF code, is is CNPJ change the element cpf to cnpj.
- {expiration} -> The expiration is calculated in seconds, it depends on the demand, it can last up to 1 month.
- {additionalInformation} -> The 'value' is what will appear to the player at the time of deposit and the 'key' will apapear on the bottom line to identify it. I recommend not using player and using random acronyms to know which game that guy is from.
- {alertClient} -> The 'alertClient' is the value linked to the key as additional information for billing.
- {amount} -> It should only be double numbers, that is, if you put 25 only the server will reject it. It must be 25.00 in double number.      
      

### Response

    {
        "transactionId": 1464038550,
        "status": "ACTIVE",
        "client": {
            "name": "Julio Campos",
            "cpf": "06054778170"
        },
        "amount": {
            "charged": 15.3
        },
        "pix": {
            "paymentTo": "b9111f34-9def-469d-8b97-e012d69014cd",
            "type": "COB",
            "qrcode": "https://clientside.postbrands.com.br/v1/invoice/qrcode/1464038550",
            "copyandpaste": "00020101021226910014br.gov.bcb.pix2569api.developer.btgpactual.com/v1/p/v2/84737b5a68814ac38fe9464c38ed3cd75204899953039865802BR5925TUNNEL VENTURE CAPITAL GR6009Sao Paulo61080145200162070503***6304044B",
            "locationid": "31529069"
        },
        "additionalInformation": {
            "value": "Pix gerado para pagar invoice",
            "key": "Pague antes do vencimento"
        },
        "createAt": "2023-03-22T01:25:00.7300423+00:00",
        "lastUpdate": "2023-03-22T01:25:00.7300423+00:00",
        "transactionIdentification": "kk6g232xel65a0daee4dd13kk1464038550"
    }
   

### Webhook Response when PAID

    {
        "receiverTaxID": "48931870000100",
        "client": {
            "name": "TUNNEL VENTURE CAPITAL GROUP LTDA",
            "taxid": "48931870000100"
        },
        "status": "CONFIRMED",
        "amount": "15.3",
        "type": "INVOICE_DEPOSIT",
        "transactionId": "1464038550",
        "transactionIdentification": "kk6g232xel65a0daee4dd13kk1464038550"
    }
    
## Transfer to CPF/CNPJ account via API

### Request

`POST https://transaction.postbrands.com.br/v1/pix/transaction/transfer`

`SHELL`

    curl --request POST \
     --url https://transaction.postbrands.com.br/v1/pix/transaction/transfer \
     --header 'accept: application/json' \
     --header 'authorization: Bearer tokenAuth ' \
     --header 'content-type: application/json' \
     --data ' {"taxID": "06054778170", "amount": "1.00" }'
      

`PHP`

    <?php

    $curl = curl_init();

    $payload = json_encode(
        array(
            "taxID" => "06054778170",
            "amount" => "1.00"
        )
    );

    curl_setopt_array($curl, [
        CURLOPT_URL => "https://transaction.postbrands.com.br/v1/pix/transaction/transfer",
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_ENCODING => "",
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => "POST",
        CURLOPT_POSTFIELDS => $payload,
        CURLOPT_HTTPHEADER => [
            "Accept: application/json",
            "authorization: Bearer YOURAUTHTOKEN",
            "Content-Type: application/json"
        ],
    ]);

    $response = curl_exec($curl);

    ?>
    
`NodeJS`

    const axios = require('axios');
    const invoiceParams = JSON.stringify({
        "taxID": "06054778170",
        "amount": "1.00"
    });

    axios.post('https://transaction.postbrands.com.br/v1/pix/transaction/transfer', invoiceParams, {
        headers: {
            'Authorization': `Bearer YOURAUTHTOKEN`
        }
    })
        .then((res) => {
            console.log(res.data)
        })
        .catch((error) => {
            console.error(error)
        })

- {tokenAuth} -> Get on integration dashboard.
- {document} -> The Pix key can be a random key, with digits generated at the time of the transaction, or it can be your email, CPF or CNPJ and phone number
- {amount} -> Amount to transfer.     
      

### Response

      {
        "receiverTaxID": "47850280000190",
        "transactionId": 1492890669,
        "status": "SUCCESS",
        "slipAuth": "CONFIDENTIAL",
        "endToEndId": "CONFIDENTIAL",
        "amount": "1.00",
        "date": "2023-04-13 14:10:27",
        "clientCode": "CONFIDENTIAL",
        "extract": "CONFIDENTIAL",
        "debitParty": {
            "account": "000000",
            "branch": 30,
            "taxId": "47850280000190",
            "accountType": "CACC",
            "name": "POSTBRANDS INSTITUICAO DE PAGAMENTO LTDA"
        },
        "creditParty": {
            "key": "06054778170",
            "bank": "90400888",
            "account": "00000000000010388079",
            "branch": 2185,
            "taxId": "06054778170",
            "accountType": "CACC",
            "name": "ADLER LOPES DE MORAIS"
        }
        
.
