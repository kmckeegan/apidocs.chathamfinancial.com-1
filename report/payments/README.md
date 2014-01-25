GET /reports/payments/{id}
=======

Returns reporting data pertaining to payments

### Common API Components

[See Common API Components](../../../../blob/master/Common.md)

### Example Request

```bash
curl https://api.chathamfinancial.com/reports/payments/exampleReport?fromdate=2013-10-31&todate=2013-11-30&offset=0
    -X GET
	-H "Authorization: Bearer XXX"
```

### Example Response

```json
{
    "Paging": {
        "Limit": 500,
        "Offset": 0,
        "TotalRecords": 2
    },
    "Items": [{
            "Id": "23433234",
            "TransactionId": "CFSponsor20130930",
            "PaymentAmount": 10000000,
            "PaymentDate": "2013-10-31"
		},
        {
            "Id": "23433235",
            "TransactionId": "CFSponsor20130930",
            "PaymentAmount": 10000000,
            "PaymentDate": "2013-11-30"
    	},
        ,
        {
            "Id": "1343435",
            "TransactionId": "CFSponsor20120831",
            "PaymentAmount": 10000000,
            "PaymentDate": "2013-10-31"
        },
        
	]	
}
```

### Request Query String Parameters

| Parameter     | Type      |  Required  | Description                      |
| ------------- | --------- | :--------: | -------------------------------- |
| fromdate      | `datetime`  | Yes        | A date in the format YYYY-MM-DD. |
| todate        | `datetime`  | Yes        | A date in the format YYYY-MM-DD. |


### Response Codes

|  Status Code  | Description
| :-----------: | -----------
| 200           | The transaction data is returned.
| 400           | Parameter validation failed. Check the response body for details. 
| | Examples: 
| | - Invalid Column name  
| | - From Date is not in the specified Date format
| | - To Date is not in the specified Date format
| 401           | Missing, invalid, expired or revoked access token.
| 500           | Transaction data gathering failed. Try again or contact support if you continue to receive this response.




