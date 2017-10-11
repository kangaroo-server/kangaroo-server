---
layout: page
---

## An OAuth2 Server

Kangaroo is an open source, multi-tenant, OAuth2 Authorization server. It
fully supports RFC 6749 (The original OAuth2 Specification), and aspires to 
be a reference implementation thereof. We intend to expand the scope of this
project to include other OAuth2 related RFC's.

Curious? The following command will start a standalone version of our server at
[https://localhost:8080/](https://localhost:8080/])

    docker run -d -p 8080:8080 kangaroo/kangaroo-authz:latest

{:.note}
> Note: OAuth2 requires HTTP TLS encryption, so the standalone server will 
> generate and sign its own certificate. Your browser will notify you of the 
> untrusted nature of this certificate every time the procel
ss is restarted.

### Tell me more?

What would you like to know?

### How can I help?

We maintain an active list of [issues](https://github.com/kangaroo-server/kangaroo/issues), and use 
github's [project tracker](https://github.com/kangaroo-server/kangaroo/projects)
for larger bodies of work. To coordinate and ensure that your work is not 
being duplicated, please reach out the the community in the [IRC Channel](http://webchat.freenode.net/?channels=kangaroo)
channel.

