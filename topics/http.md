---
title: HTTP - Symfony Certification Preparation List
---
[Back to index](../readme.md#table-of-contents)

# HTTP

## Client / Server interaction
- [HTTP Protocol - wikibooks.org](https://en.wikibooks.org/wiki/Communication_Networks/HTTP_Protocol)
- [Header Field Definitions - w3.org](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)
- [Hypertext Transfer Protocol - wikipedia.org](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)

## Status codes
- [Know Your HTTP Status Codes Well - github.com](https://github.com/for-GET/know-your-http-well/blob/master/status-codes.md) :

### 1xx

code | reason | description | spec
---: | :----- | :---------- | :---
`1xx` | **Informational** | "indicates an interim response for communicating connection status or request progress prior to completing the requested action and sending a final response." ~ [sure](http://www.urbandictionary.com/define.php?term=sure) | [RFC7231#6.2](https://tools.ietf.org/html/rfc7231#section-6.2),<br> [RFC2616#10.1](https://tools.ietf.org/html/rfc2616#section-10.1)
`100` | Continue | "indicates that the initial part of a request has been received and has not yet been rejected by the server." | [RFC7231#6.2.1](https://tools.ietf.org/html/rfc7231#section-6.2.1),<br> [RFC2616#10.1.1](https://tools.ietf.org/html/rfc2616#section-10.1.1)
`101` | Switching Protocols | "indicates that the server understands and is willing to comply with the client's request, via the Upgrade header field, for a change in the application protocol being used on this connection." | [RFC7231#6.2.2](https://tools.ietf.org/html/rfc7231#section-6.2.2),<br>[RFC2616#10.1.2](https://tools.ietf.org/html/rfc2616#section-10.1.2)

### 2xx

code | reason | description | spec
---: | :----- | :---------- | :---
`2xx` | **Successful** | "indicates that the client's request was successfully received, understood, and accepted." ~ [cool](https://twitter.com/DanaDanger/status/183316183494311936) | [RFC7231#6.3](https://tools.ietf.org/html/rfc7231#section-6.3),<br> [RFC2616#10.2](https://tools.ietf.org/html/rfc2616#section-10.2)
`200` | OK | "indicates that the request has succeeded." | [RFC7231#6.3.1](https://tools.ietf.org/html/rfc7231#section-6.3.1),<br>[RFC2616#10.2.1](https://tools.ietf.org/html/rfc2616#section-10.2.1)
`201` | Created | "indicates that the request has been fulfilled and has resulted in one or more new resources being created." | [RFC7231#6.3.2](https://tools.ietf.org/html/rfc7231#section-6.3.2),<br>[RFC2616#10.2.2](https://tools.ietf.org/html/rfc2616#section-10.2.2)
`202` | Accepted | "indicates that the request has been accepted for processing, but the processing has not been completed." | [RFC7231#6.3.3](https://tools.ietf.org/html/rfc7231#section-6.3.3),<br>[RFC2616#10.2.3](https://tools.ietf.org/html/rfc2616#section-10.2.3)
`203` | Non-Authoritative Information | "indicates that the request was successful but the enclosed payload has been modified from that of the origin server's 200 (OK) response by a transforming proxy." | [RFC7231#6.3.4](https://tools.ietf.org/html/rfc7231#section-6.3.4),<br>[RFC2616#10.2.4](https://tools.ietf.org/html/rfc2616#section-10.2.4)
`204` | No Content | "indicates that the server has successfully fulfilled the request and that there is no additional content to send in the response payload body." | [RFC7231#6.3.5](https://tools.ietf.org/html/rfc7231#section-6.3.5),<br>[RFC2616#10.2.5](https://tools.ietf.org/html/rfc2616#section-10.2.5)
`205` | Reset Content | "indicates that the server has fulfilled the request and desires that the user agent reset the "document view", which caused the request to be sent, to its original state as received from the origin server." | [RFC7231#6.3.6](https://tools.ietf.org/html/rfc7231#section-6.3.6),<br>[RFC2616#10.2.6](https://tools.ietf.org/html/rfc2616#section-10.2.6)
`206` | Partial Content | "indicates that the server is successfully fulfilling a range request for the target resource by transferring one or more parts of the selected representation that correspond to the satisfiable ranges found in the requests's Range header field." | [RFC7233#4.1](https://tools.ietf.org/html/rfc7233#section-4.1),<br>[RFC2616#10.2.7](https://tools.ietf.org/html/rfc2616#section-10.2.7)

### 3xx

code | reason | description | spec
---: | :----- | :---------- | :---
`3xx` | **Redirection** | "indicates that further action needs to be taken by the user agent in order to fulfill the request." ~ [ask that dude over there](https://twitter.com/DanaDanger/status/183316183494311936) | [RFC7231#6.4](https://tools.ietf.org/html/rfc7231#section-6.4),<br> [RFC2616#10.3](https://tools.ietf.org/html/rfc2616#section-10.3)
`300` | Multiple Choices | "indicates that the target resource has more than one representation, each with its own more specific identifier, and information about the alternatives is being provided so that the user (or user agent) can select a preferred representation by redirecting its request to one or more of those identifiers." | [RFC7231#6.4.1](https://tools.ietf.org/html/rfc7231#section-6.4.1),<br>[RFC2616#10.3.1](https://tools.ietf.org/html/rfc2616#section-10.3.1)
`301` | Moved Permanently | "indicates that the target resource has been assigned a new permanent URI and any future references to this resource ought to use one of the enclosed URIs." | [RFC7231#6.4.2](https://tools.ietf.org/html/rfc7231#section-6.4.2),<br>[RFC2616#10.3.2](https://tools.ietf.org/html/rfc2616#section-10.3.2)
`302` | Found | "indicates that the target resource resides temporarily under a different URI." | [RFC7231#6.4.3](https://tools.ietf.org/html/rfc7231#section-6.4.3),<br>[RFC2616#10.3.3](https://tools.ietf.org/html/rfc2616#section-10.3.3)
`303` | See Other | "indicates that the server is redirecting the user agent to a different resource, as indicated by a URI in the Location header field, that is intended to provide an indirect response to the original request." | [RFC7231#6.4.4](https://tools.ietf.org/html/rfc7231#section-6.4.4),<br>[RFC2616#10.3.4](https://tools.ietf.org/html/rfc2616#section-10.3.4)
`304` | Not Modified | "indicates that a conditional GET request has been received and would have resulted in a 200 (OK) response if it were not for the fact that the condition has evaluated to false." | [RFC7232#4.1](https://tools.ietf.org/html/rfc7232#section-4.1),<br>[RFC2616#10.3.5](https://tools.ietf.org/html/rfc2616#section-10.3.5)
`305` | Use Proxy | *deprecated* | [RFC7231#6.4.5](https://tools.ietf.org/html/rfc7231#section-6.4.5),<br>[RFC2616#10.3.6](https://tools.ietf.org/html/rfc2616#section-10.3.6)
`306` | | *unused* | [RFC7231#6.4.6](https://tools.ietf.org/html/rfc7231#section-6.4.6),<br>[RFC2616#10.3.7](https://tools.ietf.org/html/rfc2616#section-10.3.7)
`307` | Temporary Redirect | "indicates that the target resource resides temporarily under a different URI and the user agent MUST NOT change the request method if it performs an automatic redirection to that URI." | [RFC7231#6.4.7](https://tools.ietf.org/html/rfc7231#section-6.4.7),<br>[RFC2616#10.3.8](https://tools.ietf.org/html/rfc2616#section-10.3.8)

### 4xx

code | reason | description | spec
---: | :----- | :---------- | :---
`4xx` | **Client Error** | "indicates that the client seems to have erred." ~ [*you* fucked up](https://twitter.com/DanaDanger/status/183316183494311936) | [RFC7231#6.5](https://tools.ietf.org/html/rfc7231#section-6.5),<br> [RFC2616#10.4](https://tools.ietf.org/html/rfc2616#section-10.4)
`400` | Bad Request | "indicates that the server cannot or will not process the request because the received syntax is invalid, nonsensical, or exceeds some limitation on what the server is willing to process." | [RFC7231#6.5.1](https://tools.ietf.org/html/rfc7231#section-6.5.1),<br>[RFC2616#10.4.1](https://tools.ietf.org/html/rfc2616#section-10.4.1)
`401` | Unauthorized | "indicates that the request has not been applied because it lacks valid authentication credentials for the target resource." | [RFC7235#6.3.1](https://tools.ietf.org/html/rfc7235#section-3.1),<br>[RFC2616#10.4.2](https://tools.ietf.org/html/rfc2616#section-10.4.2)
`402` | Payment Required | *reserved* | [RFC7231#6.5.2](https://tools.ietf.org/html/rfc7231#section-6.5.2),<br>[RFC2616#10.4.3](https://tools.ietf.org/html/rfc2616#section-10.4.3)
`403` | Forbidden | "indicates that the server understood the request but refuses to authorize it." | [RFC7231#6.5.3](https://tools.ietf.org/html/rfc7231#section-6.5.3),<br>[RFC2616#10.4.4](https://tools.ietf.org/html/rfc2616#section-10.4.4)
`404` | Not Found | "indicates that the origin server did not find a current representation for the target resource or is not willing to disclose that one exists." | [RFC7231#6.5.4](https://tools.ietf.org/html/rfc7231#section-6.5.4),<br>[RFC2616#10.4.5](https://tools.ietf.org/html/rfc2616#section-10.4.5)
`405` | Method Not Allowed | "indicates that the method specified in the request-line is known by the origin server but not supported by the target resource." | [RFC7231#6.5.5](https://tools.ietf.org/html/rfc7231#section-6.5.5),<br>[RFC2616#10.4.6](https://tools.ietf.org/html/rfc2616#section-10.4.6)
`406` | Not Acceptable | "indicates that the target resource does not have a current representation that would be acceptable to the user agent, according to the proactive negotiation header fields received in the request, and the server is unwilling to supply a default representation." | [RFC7231#6.5.6](https://tools.ietf.org/html/rfc7231#section-6.5.6),<br>[RFC2616#10.4.7](https://tools.ietf.org/html/rfc2616#section-10.4.7)
`407` | Proxy Authentication Required | "is similar to 401 (Unauthorized), but indicates that the client needs to authenticate itself in order to use a proxy." | [RFC7235#3.2](https://tools.ietf.org/html/rfc7235#section-3.2),<br>[RFC2616#10.4.8](https://tools.ietf.org/html/rfc2616#section-10.4.8)
`408` | Request Timeout | "indicates that the server did not receive a complete request message within the time that it was prepared to wait." | [RFC7231#6.5.7](https://tools.ietf.org/html/rfc7231#section-6.5.7),<br>[RFC2616#10.4.9](https://tools.ietf.org/html/rfc2616#section-10.4.9)
`409` | Conflict | "indicates that the request could not be completed due to a conflict with the current state of the resource." | [RFC7231#6.5.8](https://tools.ietf.org/html/rfc7231#section-6.5.8),<br>[RFC2616#10.4.10](https://tools.ietf.org/html/rfc2616#section-10.4.10)
`410` | Gone | "indicates that access to the target resource is no longer available at the origin server and that this condition is likely to be permanent." | [RFC7231#6.5.9](https://tools.ietf.org/html/rfc7231#section-6.5.9),<br>[RFC2616#10.4.11](https://tools.ietf.org/html/rfc2616#section-10.4.11)
`411` | Length Required | "indicates that the server refuses to accept the request without a defined Content-Length." | [RFC7231#6.5.10](https://tools.ietf.org/html/rfc7231#section-6.5.10),<br>[RFC2616#10.4.12](https://tools.ietf.org/html/rfc2616#section-10.4.12)
`412` | Precondition Failed | "indicates that one or more preconditions given in the request header fields evaluated to false when tested on the server." | [RFC7232#4.2](https://tools.ietf.org/html/rfc7232#section-4.2),<br>[RFC2616#10.4.13](https://tools.ietf.org/html/rfc2616#section-10.4.13)
`413` | Payload Too Large | "indicates that the server is refusing to process a request because the request payload is larger than the server is willing or able to process." | [RFC7231#6.5.11](https://tools.ietf.org/html/rfc7231#section-6.5.11),<br>[RFC2616#10.4.14](https://tools.ietf.org/html/rfc2616#section-10.4.14)
`414` | URI Too Long | "indicates that the server is refusing to service the request because the request-target is longer than the server is willing to interpret." | [RFC7231#6.5.12](https://tools.ietf.org/html/rfc7231#section-6.5.12),<br>[RFC2616#10.4.15](https://tools.ietf.org/html/rfc2616#section-10.4.15)
`415` | Unsupported Media Type | "indicates that the origin server is refusing to service the request because the payload is in a format not supported by the target resource for this method." | [RFC7231#6.5.13](https://tools.ietf.org/html/rfc7231#section-6.5.13),<br>[RFC2616#10.4.16](https://tools.ietf.org/html/rfc2616#section-10.4.16)
`416` | Range Not Satisfiable | "indicates that none of the ranges in the request's Range header field overlap the current extent of the selected resource or that the set of ranges requested has been rejected due to invalid ranges or an excessive request of small or overlapping ranges." | [RFC7233#4.4](https://tools.ietf.org/html/rfc7233#section-4.4),<br>[RFC2616#10.4.17](https://tools.ietf.org/html/rfc2616#section-10.4.17)
`417` | Expectation Failed | "indicates that the expectation given in the request's Expect header field could not be met by at least one of the inbound servers." | [RFC7231#6.5.14](https://tools.ietf.org/html/rfc7231#section-6.5.14),<br>[RFC2616#10.4.18](https://tools.ietf.org/html/rfc2616#section-10.4.18)
`418` | I'm a teapot | "Any attempt to brew coffee with a teapot should result in the error code 418 I'm a teapot." | [RFC2324#2.3.2](https://tools.ietf.org/html/rfc2324#section-2.3.2)
`426` | Upgrade Required | "indicates that the server refuses to perform the request using the current protocol but might be willing to do so after the client upgrades to a different protocol." | [RFC7231#6.5.15](https://tools.ietf.org/html/rfc7231#section-6.5.15)

### 5xx

code | reason | description | spec
---: | :----- | :---------- | :---
`5xx` | **Server Error** | "indicates that the server is aware that it has erred or is incapable of performing the requested method." ~ [*we* fucked up](https://twitter.com/DanaDanger/status/183316183494311936) | [RFC7231#6.6](https://tools.ietf.org/html/rfc7231#section-6.6),<br> [RFC2616#10.5](https://tools.ietf.org/html/rfc2616#section-10.5)
`500` | Internal Server Error | "indicates that the server encountered an unexpected condition that prevented it from fulfilling the request." | [RFC7231#6.6.1](https://tools.ietf.org/html/rfc7231#section-6.6.1),<br>[RFC2616#10.5.2](https://tools.ietf.org/html/rfc2616#section-10.5.1)
`501` | Not Implemented | "indicates that the server does not support the functionality required to fulfill the request." | [RFC7231#6.6.2](https://tools.ietf.org/html/rfc7231#section-6.6.2),<br>[RFC2616#10.5.3](https://tools.ietf.org/html/rfc2616#section-10.5.2)
`502` | Bad Gateway | "indicates that the server, while acting as a gateway or proxy, received an invalid response from an inbound server it accessed while attempting to fulfill the request." | [RFC7231#6.6.3](https://tools.ietf.org/html/rfc7231#section-6.6.3),<br>[RFC2616#10.5.4](https://tools.ietf.org/html/rfc2616#section-10.5.3)
`503` | Service Unavailable | "indicates that the server is currently unable to handle the request due to a temporary overload or scheduled maintenance, which will likely be alleviated after some delay." | [RFC7231#6.6.4](https://tools.ietf.org/html/rfc7231#section-6.6.4),<br>[RFC2616#10.5.5](https://tools.ietf.org/html/rfc2616#section-10.5.4)
`504` | Gateway Time-out | "indicates that the server, while acting as a gateway or proxy, did not receive a timely response from an upstream server it needed to access in order to complete the request." | [RFC7231#6.6.5](https://tools.ietf.org/html/rfc7231#section-6.6.5),<br>[RFC2616#10.5.6](https://tools.ietf.org/html/rfc2616#section-10.5.5)
`505` | HTTP Version Not Supported | "indicates that the server does not support, or refuses to support, the protocol version that was used in the request message." | [RFC7231#6.6.6](https://tools.ietf.org/html/rfc7231#section-6.6.6),<br>[RFC2616#10.5.6](https://tools.ietf.org/html/rfc2616#section-10.5.6)

## Extensions

code | reason | description | spec
---: | :----- | :---------- | :---
`102` | Processing | "is an interim response used to inform the client that the server has accepted the complete request, but has not yet completed it." | [RFC5218#10.1](https://tools.ietf.org/html/rfc2518#section-10.1)
`207` | Multi-Status | "provides status for multiple independent operations." | [RFC5218#10.2](https://tools.ietf.org/html/rfc2518#section-10.2)
`226` | IM Used | "The server has fulfilled a GET request for the resource, and the response is a representation of the result of one or more instance-manipulations applied to the current instance." | [RFC3229#10.4.1](https://tools.ietf.org/html/rfc3229#section-10.4.1)
`308` | Permanent Redirect | "The target resource has been assigned a new permanent URI and any future references to this resource outght to use one of the enclosed URIs. [...] This status code is similar to 301 Moved Permanently (Section 7.3.2 of rfc7231), except that it does not allow rewriting the request method from POST to GET." | [RFC7538](https://tools.ietf.org/html/rfc7538)
`422` | Unprocessable Entity | "means the server understands the content type of the request entity (hence a 415(Unsupported Media Type) status code is inappropriate), and the syntax of the request entity is correct (thus a 400 (Bad Request) status code is inappropriate) but was unable to process the contained instructions." | [RFC5218#10.3](https://tools.ietf.org/html/rfc2518#section-10.3)
`423` | Locked | "means the source or destination resource of a method is locked." | [RFC5218#10.4](https://tools.ietf.org/html/rfc2518#section-10.4)
`424` | Failed Dependency | "means that the method could not be performed on the resource because the requested action depended on another action and that action failed." | [RFC5218#10.5](https://tools.ietf.org/html/rfc2518#section-10.5)
`428` | Precondition Required | "indicates that the origin server requires the request to be conditional." | [RFC6585#3](https://tools.ietf.org/html/rfc6585#section-3)
`429` | Too Many Requests | "indicates that the user has sent too many requests in a given amount of time ("rate limiting")." | [RFC6585#4](https://tools.ietf.org/html/rfc6585#section-4)
`431` | Request Header Fields Too Large | "indicates that the server is unwilling to process the request because its header fields are too large." | [RFC6585#5](https://tools.ietf.org/html/rfc6585#section-5)
`451` | Unavailable For Legal Reasons | "This status code indicates that the server is denying access to the resource in response to a legal demand." | [draft-ietf-httpbis-legally-restricted-status](https://tools.ietf.org/html/draft-ietf-httpbis-legally-restricted-status)
`506` | Variant Also Negotiates | "indicates that the server has an internal configuration error: the chosen variant resource is configured to engage in transparent content negotiation itself, and is therefore not a proper end point in the negotiation process." | [RFC2295#8.1](https://tools.ietf.org/html/rfc2295#section-8.1)
`507` | Insufficient Storage | "means the method could not be performed on the resource because the server is unable to store the representation needed to successfully complete the request." | [RFC5218#10.6](https://tools.ietf.org/html/rfc2518#section-10.6)
`511` | Network Authentication Required | "indicates that the client needs to authenticate to gain network access." | [RFC6585#6](https://tools.ietf.org/html/rfc6585#section-6)
`7xx` | **Developer Error** | [err](http://www.urbandictionary.com/define.php?term=err) | [7xx-rfc](http://documentup.com/joho/7XX-rfc)



## HTTP request
- [Request - w3.org](https://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html)
- [Method Definitions - w3.org](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)

The set of common methods for HTTP/1.1 is defined below. Although this set can be expanded, additional methods cannot be assumed to share the same semantics for separately extended clients and servers.

**Safe Methods**  

In particular, the convention has been established that the **GET and HEAD** methods **SHOULD NOT** have the significance of **taking an action other than retrieval**. These methods ought to be considered "safe". This allows user agents to represent other methods, such as POST, PUT and DELETE, in a special way, so that the user is made aware of the fact that a possibly unsafe action is being requested.

**Idempotent Methods**  
Methods can also have the property of **"idempotence"** in that (aside from error or expiration issues) the side-effects of N > 0 identical requests is the same as for a single request. **The methods GET, HEAD, PUT and DELETE share this property**. **Also, the methods OPTIONS and TRACE SHOULD NOT have side effects, and so are inherently idempotent.**

### OPTIONS  
The OPTIONS method represents a request for information about the communication options available on the request/response chain identified by the Request-URI. This method allows the client to determine the options and/or requirements associated with a resource, or the capabilities of a server, without implying a resource action or initiating a resource retrieval.

**Responses to this method are not cacheable.**

If the OPTIONS request includes an entity-body (as indicated by the presence of Content-Length or Transfer-Encoding), then the media type MUST be indicated by a Content-Type field. Although this specification does not define any use for such a body, future extensions to HTTP might use the OPTIONS body to make more detailed queries on the server. A server that does not support such an extension MAY discard the request body.

If the Request-URI is an asterisk ("*"), the OPTIONS request is intended to apply to the server in general rather than to a specific resource. Since a server's communication options typically depend on the resource, the "*" request is only useful as a "ping" or "no-op" type of method; it does nothing beyond allowing the client to test the capabilities of the server. For example, this can be used to test a proxy for HTTP/1.1 compliance (or lack thereof).

If the Request-URI is not an asterisk, the OPTIONS request applies only to the options that are available when communicating with that resource.

A 200 response SHOULD include any header fields that indicate optional features implemented by the server and applicable to that resource (e.g., Allow), possibly including extensions not defined by this specification. The response body, if any, SHOULD also include information about the communication options. The format for such a

body is not defined by this specification, but might be defined by future extensions to HTTP. Content negotiation MAY be used to select the appropriate response format. If no response body is included, the response MUST include a Content-Length field with a field-value of "0".

The Max-Forwards request-header field MAY be used to target a specific proxy in the request chain. When a proxy receives an OPTIONS request on an absoluteURI for which request forwarding is permitted, the proxy MUST check for a Max-Forwards field. If the Max-Forwards field-value is zero ("0"), the proxy MUST NOT forward the message; instead, the proxy SHOULD respond with its own communication options. If the Max-Forwards field-value is an integer greater than zero, the proxy MUST decrement the field-value when it forwards the request. If no Max-Forwards field is present in the request, then the forwarded request MUST NOT include a Max-Forwards field.

### GET 
The GET method means **retrieve whatever information (in the form of an entity) is identified by the Request-URI.** If the Request-URI refers to a data-producing process, it is the produced data which shall be returned as the entity in the response and not the source text of the process, unless that text happens to be the output of the process.

The semantics of the GET method change to a "conditional GET" if the request message includes an If-Modified-Since, If-Unmodified-Since, If-Match, If-None-Match, or If-Range header field. A conditional GET method requests that the entity be transferred only under the circumstances described by the conditional header field(s). The conditional GET method is intended to reduce unnecessary network usage by allowing cached entities to be refreshed without requiring multiple requests or transferring data already held by the client.

The semantics of the GET method change to a "partial GET" if the request message includes a Range header field. A partial GET requests that only part of the entity be transferred, as described in section 14.35. The partial GET method is intended to reduce unnecessary network usage by allowing partially-retrieved entities to be completed without transferring data already held by the client.

The response to a GET request **is cacheable if and only if it meets the requirements for HTTP caching described in section 13.**


### HEAD  
The HEAD method is **identical to GET except that the server MUST NOT return a message-body in the response.** The metainformation contained in the HTTP headers in response to a HEAD request SHOULD be identical to the information sent in response to a GET request. This method can be used for **obtaining metainformation about the entity implied by the request without transferring the entity-body itself.** This method is often used for testing **hypertext links for validity, accessibility, and recent modification.**

The response to a **HEAD request MAY be cacheable in the sense that the information contained in the response MAY be used to update a previously cached entity from that resource**. If the new field values indicate that the cached entity differs from the current entity (as would be indicated by a change in Content-Length, Content-MD5, ETag or Last-Modified), then the cache MUST treat the cache entry as stale.

### POST  
The POST method is used to **request that the origin server accept the entity enclosed in the request as a new subordinate of the resource identified by the Request-URI in the Request-Line**. POST is designed to allow a uniform method to cover the following functions:
- Annotation of existing resources;
- Posting a message to a bulletin board, newsgroup, mailing list, or similar group of articles;
- Providing a block of data, such as the result of submitting a form, to a data-handling process;
- Extending a database through an append operation.

The actual function performed by the POST method is determined by the server and is usually dependent on the Request-URI. The posted entity is subordinate to that URI in the same way that a file is subordinate to a directory containing it, a news article is subordinate to a newsgroup to which it is posted, or a record is subordinate to a database.

The action performed by the POST method might not result in a resource that can be identified by a URI. In this case, either **200 (OK)** or **204 (No Content)** is the appropriate response status, depending on whether or not the response includes an entity that describes the result.

If a resource has been created on the origin server, the response **SHOULD be 201 (Created)** and contain an entity which describes the status of the request and refers to the new resource, and a Location header (see section 14.30).

**Responses to this method are not cacheable,** unless the response includes appropriate Cache-Control or Expires header fields. However, the **303 (See Other) response** can be used to direct the user agent to retrieve a cacheable resource.

### PUT  
The PUT method requests that the enclosed entity be stored under the supplied Request-URI. **If the Request-URI refers to an already existing resource**, the enclosed entity SHOULD be considered as a **modified version** of the one residing on the origin server. **If the Request-URI does not point to an existing resource**, and that URI is capable of being defined as a **new resource** by the requesting user agent, the origin server can create the resource with that URI. If a new resource is created, the origin server MUST inform the user agent via the **201 (Created) response**. If an existing resource is modified, either the **200 (OK) or 204 (No Content)** response codes SHOULD be sent to indicate successful completion of the request. If the resource could not be created or modified with the Request-URI, an appropriate error response SHOULD be given that reflects the nature of the problem. The recipient of the entity MUST NOT ignore any Content-* (e.g. Content-Range) headers that it does not understand or implement and MUST return a 501 (Not Implemented) response in such cases.

If the request passes through a cache and the Request-URI identifies one or more currently cached entities, those entries SHOULD be treated as stale. **Responses to this method are not cacheable.**

**The fundamental difference between the POST and PUT requests** is reflected in the different meaning of the Request-URI. The URI in a POST request identifies the resource that will handle the enclosed entity. That resource might be a data-accepting process, a gateway to some other protocol, or a separate entity that accepts annotations. In contrast, the URI in a PUT request identifies the entity enclosed with the request -- the user agent knows what URI is intended and the server MUST NOT attempt to apply the request to some other resource. If the server desires that the request be applied to a different URI,

it MUST send a 301 (Moved Permanently) response; the user agent MAY then make its own decision regarding whether or not to redirect the request.

A single resource MAY be identified by many different URIs. For example, an article might have a URI for identifying "the current version" which is separate from the URI identifying each particular version. In this case, a PUT request on a general URI might result in several other URIs being defined by the origin server.


### DELETE  
The DELETE method requests that the origin server delete the resource identified by the Request-URI. This method MAY be overridden by human intervention (or other means) on the origin server. The client cannot be guaranteed that the operation has been carried out, even if the status code returned from the origin server indicates that the action has been completed successfully. However, the server SHOULD NOT indicate success unless, at the time the response is given, it intends to delete the resource or move it to an inaccessible location.

A successful response SHOULD be **200 (OK)** if the response includes an entity describing the status, **202 (Accepted) if the action has not yet been enacted**, or **204 (No Content) if the action has been enacted but the response does not include an entity**.

If the request passes through a cache and the Request-URI identifies one or more currently cached entities, those entries SHOULD be treated as stale. **Responses to this method are not cacheable.**

### TRACE  
The TRACE method is used to invoke a remote, application-layer loop- back of the request message. The final recipient of the request SHOULD reflect the message received back to the client as the entity-body of a 200 (OK) response. The final recipient is either the origin server or the first proxy or gateway to receive a Max-Forwards value of zero (0) in the request (see section 14.31). A TRACE request MUST NOT include an entity.

TRACE allows the client to see what is being received at the other end of the request chain and use that data for testing or diagnostic information. The value of the Via header field (section 14.45) is of particular interest, since it acts as a trace of the request chain. Use of the Max-Forwards header field allows the client to limit the length of the request chain, which is useful for testing a chain of proxies forwarding messages in an infinite loop.

If the request is valid, the response SHOULD contain the entire request message in the entity-body, with a Content-Type of "message/http". Responses to this method MUST NOT be cached.

### CONNECT  
This specification reserves the method name CONNECT **for use with a proxy that can dynamically switch to being a tunnel** 


## HTTP response
- [Response - w3.org](https://www.w3.org/Protocols/rfc2616/rfc2616-sec6.html#sec6)

```
response-header = Accept-Ranges          ; Acceptance of range requests
               | Age                     ; Time since the response was generated.
               | ETag                    ; Current value of the entity tag
               | Location                ; Single absolute URI for a complementary ressource (201, 3xx)
               | Proxy-Authenticate      ; When 407
               | Retry-After             ; How long the service is expected to be unavailable (503, 3xx)
               | Server                  ; Contain multiple product tokens (Server Informations)
               | Vary                    ; Cache information
               | WWW-Authenticate        ; When 401
```

## HTTP methods
- [Method Definitions - w3.org](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)

## Cookies
- [HTTP cookie - wikipedia.org](https://en.wikipedia.org/wiki/HTTP_cookie)
- [Setting Cookies - symfony.com](https://symfony.com/doc/5.0/components/http_foundation.html#setting-cookies)

## Caching
See [HTTP Caching](./http-caching.md)

## Content negotiation
- [Content negotiation - developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation)

## Language detection
- [Accept-Language used for locale setting - w3.org](https://www.w3.org/International/questions/qa-accept-lang-locales)
- [Accept-Language - w3.org](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.4)

## Symfony HttpClient component
- [HttpClient - symfony.com](https://symfony.com/doc/5.0/http_client.html)
