---
url: /jwt
title: JSON Web Tokens
description: JSON Web Token (JWT) is an open standard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. Learn the concepts needed to fully understand JWTs.
toc: false
topics:
  - tokens
  - jwt
  - id-token
  - access-token
contentType:
  - concept
useCase:
  - development
  - add-login
  - invoke-api
  - secure-api
---
# JSON Web Token

::: note
This doc describes the general use of JSON Web Tokens (JWTs). Understanding the general use, structure, and format of JWTs will make it easier to understand how most tokens are used with Auth0. If you already know about JWTs and want more info on the different types of tokens used with Auth0, see [Tokens](/tokens).
:::

JSON Web Token (JWT), pronounced "jot", is an open standard ([RFC 7519](https://tools.ietf.org/html/rfc7519)) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.

* **Compact**: Because of its relatively small size, a JWT can be sent through a URL, through a POST parameter, or inside an HTTP header, and it is transmitted quickly.
* **Self-contained**: A JWT contains all the required information about an entity to avoid querying a database more than once. The recipient of a JWT also does not need to call a server to validate the token.

::: note
For info about why to use JWT over other token formats, including Simple Web Tokens (SWT) and <dfn data-key="security-assertion-markup-language">SAML</dfn> tokens, see [Why Use JSON Web Token](/tokens/concepts/why-use-jwt).
:::

## Use of JWTs

JWT is a standard, which means that **all JWTs are tokens, but not all tokens are JWTs**. JWTs can be used in varying ways:

- **Authentication**: When a user successfully logs in using their credentials, an [ID Token](/tokens/id-tokens) is returned. According to the <dfn data-key="openid">[OpenID Connect (OIDC) specs](https://openid.net/specs/openid-connect-core-1_0.html#IDToken)</dfn>, an ID Token is always a JWT. To learn more about how to get and validate an ID Token using Auth0, see [ID Tokens](/tokens/id-tokens).

- **Authorization**: Once a user is successfully logged in, an application may request to access routes, services, or resources (e.g., APIs) on behalf of that user. To do so, in every request, it must pass an <dfn data-key="access-token">Access Token</dfn>, which *may* be in the form of a JWT. <dfn data-key="single-sign-on">Single Sign-on (SSO)</dfn> widely uses JWT because of the small overhead of the format, and its ability to easily be used across different domains. To learn more about how to use Access Tokens with Auth0, see [Access Tokens](/tokens/access-tokens).

- **Information Exchange**: JWTs are a good way of securely transmitting information between parties because they can be signed, which means you can be sure that the senders are who they say they are. Additionally, the structure of a JWT allows you to verify that the content hasn't been tampered with.

::: warning
However you use JWTs, be sure to follow [best practices for tokens](/tokens/concepts/token-best-practices) and make sure you [verify the signature](/tokens/guides/id-token/validate-id-token#verify-the-signature) before storing and using a JWT. For more information on how to implement JWT, see [Validate a JSON Web Token](/tokens/guides/jwt/validate-jwt).
:::

## Security

The information contained within the JSON object can be verified and trusted because it is digitally signed. Although JWTs can also be encrypted to provide secrecy between parties, Auth0-issued JWTs are JSON Web Signatures (JWS), meaning they are signed rather than encrypted. As such, we will focus on *signed* tokens, which can *verify the integrity* of the claims contained within them, while encrypted tokens *hide* those claims from other parties.

In general, JWTs can be signed using a secret (with the **HMAC** algorithm) or a public/private key pair using **RSA** or **ECDSA** (although Auth0 supports only HMAC and RSA). When tokens are signed using public/private key pairs, the signature also certifies that only the party holding the private key is the one that signed it.

Before a received JWT is used, it should be [properly validated using its signature](/tokens/guides/id-token/validate-id-token#verify-the-signature). Note that a successfully validated token only means that the information contained within the token has not been modified by anyone else. This doesn't mean that others weren't able to see the content, which is stored in plain text. Because of this, you should never store sensitive information inside a JWT and should take other steps to ensure that JWTs are not intercepted, such as by sending JWTs only over HTTPS, following [best practices](/tokens/concepts/token-best-practices), and using only secure and up-to-date libraries.

## Next steps

::: next-steps
* [Why Use JSON Web Token](/tokens/concepts/why-use-jwt)
* [JSON Web Token Structure](/tokens/reference/jwt/jwt-structure)
* [JSON Web Token Claims](/tokens/jwt-claims)
* [Validate a JSON Web Token](/tokens/guides/jwt/validate-jwt)
* [Best Practices for Tokens](/tokens/concepts/token-best-practices)
:::

## Read more

* [JWT Handbook](https://auth0.com/resources/ebooks/jwt-handbook)
* [Web Apps vs Web APIs / Cookies vs Tokens](/design/web-apps-vs-web-apis-cookies-vs-tokens)
* [10 Things You Should Know About Tokens](https://auth0.com/blog/ten-things-you-should-know-about-tokens-and-cookies/)

