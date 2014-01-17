GET /report/{id}
=======

Returns the contents of the report file or the status of the report if it is not ready.

#### Example Request

```bash
curl https://api.chathamfinancial.com/report/12345 
	-H "Authorization: Bearer XXX" 
	-H "Accept: application/json"
```

#### Example Response

The status code of the response indicates the status of the request.

|  Status Code  | Description
| :-----------: | -----------
| 200           | Report is ready.
| 202           | Report is still generating.
| 400           | Parameter validation failed. Check the response body for details.
| 401           | Missing, invalid, expired or revoked access token.
| 404           | Report is invalid. Check the value of the `id` parameter.
| 500           | Report generation failed. Try again or contact support if you continue to receive this response.
