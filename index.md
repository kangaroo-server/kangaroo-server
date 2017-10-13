---
layout: default
---

Kangaroo is an open source, multi-tenant, OAuth2 Authorization server. It
fully supports RFC 6749 (The original OAuth2 Specification), and aspires to 
be a reference implementation thereof. We intend to expand the scope of this
project to include other OAuth2 related RFC's.

``` bash
docker run -d -p 8080:8080 kangaroo/kangaroo-authz:latest
```

The above command will start a standalone server at [https://localhost:8080/](https://localhost:8080/]).
This server will sign its own SSL certificate on startup; Your browser will notify you of the 
untrusted nature of this certificate, every time the process is restarted.

{% for item in site.documentation %}
### {{ item.title }} {#{{item.title}}}
{{item}}
{% endfor %}
