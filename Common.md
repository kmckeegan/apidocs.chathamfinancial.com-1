# ![Compass Logo](https://raw.github.com/Chatham/apidocs.chathamfinancial.com/master/ChathamCompass-150x150.png) Common API Components
=======================

## Required Components
The following components are required to be on every request made to the API.

### Authorization
-----

#### **[OAuth 2.0](http://tools.ietf.org/html/rfc6749) Access Token**

Each request is required to have an access token in the `Authorization` header of the request. The access token is provided by Chatham.

The format is:

```text
Authorization: Bearer <AccessToken>
```

Replace `<Access Token>` with the Chatham provided access token. See [RFC 6750](http://tools.ietf.org/html/rfc6750) for more information.

*Example:*

```text
Authorization: Bearer 6879dcb0789ef62a0789d509ff624a98c9809b66
```
#### **Related Status Codes**

|  Status Code  | Description                                    |
| :-----------: | ---------------------------------------------- |
| `401`         | You are not authorized to access the resource. |

-----
## Optional Components
The following components are optional and not required to be on each request. Each component may not be valid on every request, see notes for that component.

### Content Type
-----
You can specify the content type of the response by setting the `Accept` header in the request. All requests support setting the `Accept` header.

*Example:*

```text
Accept: application/json
```

Supported Content Types:
* `application/json`

The default content type is `application/json` if the `Accept` header is missing from the request. See [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) for more information.

#### **Related Status Codes**

|  Status Code  | Description                        |
| :-----------: | ---------------------------------- |
| `415`         | The content type is not supported. |

-----

### Compression

-----
All requests support compressed responses. Include `Accept-Encoding` header with a supported compression in your request to get a compressed response.

*Example:*

```text
Accept-Encoding: gzip,deflate
```

Supported Compression:

* `gzip`
* `deflate`

See [RFC 2616 Section 14.3](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.3) for more information.

-----

### Pagination
----
Responses that are collections are paged.

| Query String Parameter    | Default | Min Value | Max Value         | Description                                       |
| ------------------------- | ------- | --------- | ----------------- | ------------------------------------------------- |
| offset                    | `0`     | `0`       | `total items - 1` | Index of the first record to return (zero based). |
| limit                     | `100`   | `1`       | `500`             | Specifies the maximum number of items to return.  | 

* If the `previous` link is not present in the `Link` header, you are at the beginning of the collection.
* If the `next` link is not present in the `Link` header, you are at the end of the collection.

#### **Typical Paged Response**

**[Link Header](http://tools.ietf.org/html/rfc5988)**

```text
Link: <?limit=2&offset=2>;
      rel="previous",
      <?limit=2&offset=4>;
      rel="self",
      <?limit=2&offset=6>;
      rel="next",
      <?limit=2&offset=0>;
      rel="first",
      <?limit=2&offset=8>;
      rel="last"
```

**Message Body**

```json
{
    "Paging": {
        "Limit": 2,
        "Offset": 4,
        "TotalItems": 10
    },
    "Items": [
        { ...item1... },
        { ...item2... }
	]	
}
```

----

### Serialization Options
----

Per request serilization options are available. Options are set in the `X-Chatham-Serializer-Options` header. Multiple values are separated by a `,`.

| Option Name         | Description | Supported Content Types |
| ------------------- | ----------- | ----------------------- |
| `IncludeNullValues` | To save on processing and reduce response size, `null` values are not serialized by default. Use this option to include `null` values in the response. | `application/json` |


*Example:*

```text
X-Chatham-Serializer-Options: IncludeNullValues
```

**Note:** *Header name and values are case insensitive.*

----
