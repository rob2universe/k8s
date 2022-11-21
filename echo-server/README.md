## Setup

Follw the Keycloak setup instructions described in the [Oauth2 Proxy documentation](https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/oauth_provider/#keycloak-auth-provider):
- client in desired realm
- with Access Type *confidental*
- client protocol *openid-connect*
- redirect URIs *https://yourhostname/oauth2/callback*
- mapper with mapper type *Group Membership* and token claim name *groups*
- mapper with mapper type *Audience* and *Included Client Audience* set to client name

Configuire [oauth2-values.yaml](oauth2-values.yaml). Find the *client secret* required on the *Credentials* tab of the client configuration.


