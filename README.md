# OAuth2 Client generic provider for config by .env file

This package provides OAuth 2.0 generic support from config .env file for the PHP League's [OAuth 2.0 Client](https://github.com/thephpleague/oauth2-client).

## Installation

To install, use composer:

```
composer require mathieu-dumoutier/oauth2-envconfig
```

## Usage

Usage is the same as The League's OAuth client, using `\MathieuDumoutier\OAuth2\Client\Provider\EnvConfig` as the provider.

## knpuniversity/oauth2-client-bundle configuration example

```yaml
knpu_oauth2_client:
    clients:
        yourapp_oauth:
            type: generic
            provider_class: MathieuDumoutier\OAuth2\Client\Provider\EnvConfigProvider
            provider_options:
                "scopes": '%env(OAUTH2_SCOPES)%'
                "app_url": '%env(OAUTH2_BASE_APP_URL)%'    
                "api_url": '%env(OAUTH2_BASE_API_URL)%'    
            client_id: '%env(OAUTH2_CLIENT_ID)%'
            client_secret: '%env(OAUTH2_CLIENT_SECRET)%'
            redirect_route: oauth2_check
            redirect_params: {}
            use_state: false
```

You must define 6 environment variables :
* OAUTH2_CLIENT_ID 
* OAUTH2_CLIENT_SECRET
* OAUTH2_SCOPES (scopes would you want requested)
* OAUTH2_BASE_APP_URL
* OAUTH2_BASE_API_URL

You must create the route "oauth2_check" in a controller :

```php
#[Route('/oauth2_check', name: 'oauth2_check')]
public function oauth2Check(): void
{
    // This action is not executed because onAuthenticationSuccess() method of the OAuth2Authenticator class redirect before
}
```
