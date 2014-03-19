GET /reports/payments/{id}
=======

Returns reporting data pertaining to payments

### Common API Components

[See Common API Components](../../../../blob/master/Common.md)

### Example Request

```bash
curl https://api.chathamfinancial.com/reports/payments/exampleReport?transactionfromdate=2013-10-31&transactiontodate=2013-11-30&offset=0
    -X GET
	-H "Authorization: Bearer XXX"
```

This request will return all payments for transactions active from and including 2013-10-31 and to and including 2013-11-30 using the `exampleReport` payment report template.

### Example Response

```json
{
    "Paging": {
        "Limit": 500,
        "Offset": 0,
        "TotalRecords": 3
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

### Request Path Parameters

| Parameter | Type     |  Required  | Description                       |
| --------- | -------- | :--------: | --------------------------------- |
| `{id}`    | `string` | Yes        | The payment report template name |

### Request Query String Parameters

| Parameter             | Type   |  Required  | Description                                 |
| --------------------- | ------ | :--------: | ------------------------------------------- |
| `fromdate`            | `date` | No         | A date in the [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601#Calendar_dates) format `YYYY-MM-DD`. |
| `todate`              | `date` | No         | A date in the [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601#Calendar_dates) format `YYYY-MM-DD`. |
| `transactionfromdate` | `date` | Yes        | A date in the [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601#Calendar_dates) format `YYYY-MM-DD`. |
| `transactiontodate`   | `date` | Yes        | A date in the [ISO-8601](http://en.wikipedia.org/wiki/ISO_8601#Calendar_dates) format `YYYY-MM-DD`. |

### Response Codes

|  Status Code  | Description
| :-----------: | -----------
| 200           | The payment data is returned.
| 400           | Parameter validation failed. Check the response body for details. 
| | Examples: 
| | - A date is not in the specified date format.
| | - A from date occurs after a to date.
| | - A required parameter is missing.
| | - The length of time between `transactionfromdate` and `transactiontodate` is greater than five years.
| 401           | Missing, invalid, expired or revoked access token.
| 404           | Invalid payment report template name.
| 500           | Transaction data gathering failed. Try again or contact support if you continue to receive this response.

### Notes

- Set `transactionfromdate` and `transactiontodate` to the same value to get payments for transactions that were active on a specific day.
- Set `fromdate` and `todate` to the same value to only get payments for a specific day.
- If `fromdate` and `todate` are not provided, all payments for active transactions (as filtered by `transactionfromdate` and `transactiontodate`) are returned.
