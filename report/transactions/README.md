GET /report/transactions/{id}
=======

Returns reporting data pertaining to transactions

### Common API Components

[See Common API Components](../../../../blob/master/Common.md)

### Example Request

```bash
curl https://api.chathamfinancial.com/report/transactions/examplereport?fromdate=2013-07-01&todate=2013-09-30&offset=0
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
            "Id": "CFSponsor20110930",
            "EffectiveDate": "2011-09-30",
            "Notional": 30000000,
    	    "NotionalCurrency": "USD"	
		},
        {
	    	"Id": "CFSponsor201311031",
    		"EffectiveDate": "2011-11-31",
    		"Notional": 250000000,
    		"NotionalCurrency": "EUR"	
		}
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



