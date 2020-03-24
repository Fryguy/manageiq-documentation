# Specification

## HTTP Basics

Unresolved directive in chap-Specification.adoc -
include::REST\_API\_Entry\_Point.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Supported\_Content\_Types.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::URL\_Paths.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Methods\_and\_related\_URLs.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Updating\_Resources.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Modifying\_Resource\_Attributes.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Return\_Codes.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::CRUD\_Examples.adoc\[\]

## Authentication

There are two methods of authentication for the {product-title} REST
API:

  - **Basic Authentication**: The user and password credentials are
    passed in with each HTTP request.

  - **Token based Authentication**: The client requests a token for the
    username/password credentials specified. Then the token is used in
    lieu of the username/password for each subsequent API call.

Unresolved directive in chap-Specification.adoc -
include::Using\_Basic\_Authentication.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Using\_Authentication\_Tokens.adoc\[\]

## JSON Specification

The API uses JSON throughout; the Content-Type for all requests and
responses is `application/json`.

As is general practice with REST, clients should not make assumptions
about the server’s URL space. Clients are expected to discover all URL’s
by navigating the API. To keep this document readable, we still mention
specific URL’s, generally in the form of an absolute path. Clients
should not use these, or assume that the actual URL structure follows
these examples, and instead use discovered URL’s. Any client should
start its discovery with the API entry point, here denoted with `/api`.

Unresolved directive in chap-Specification.adoc -
include::Basic\_types.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Common\_Attributes\_and\_Actions.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Collections4.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Actions4.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Forms1.adoc\[\]

## Query Specification

This specification identifies the controls available when querying
collections.

Unresolved directive in chap-Specification.adoc -
include::Control\_Attributes.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Filtering.adoc\[\]

Unresolved directive in chap-Specification.adoc -
include::Expanding\_Collections1.adoc\[\]
