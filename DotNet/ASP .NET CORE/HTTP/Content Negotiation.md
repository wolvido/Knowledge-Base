---
keywords: what is content negotiation in HTML
---
Content Negotiation is the process of selecting the appropriate format or language of the content to be exchanged between the client and API.

For example, the client may ask for XML data instead of receiving content in JSON format:
- The client will send `Accept: application/xml` in the header.
- If the server supports xml or conversion to xml. then it will return header: `Content-Type:application/xml`
- If not then it will return http 415 unsupported.



