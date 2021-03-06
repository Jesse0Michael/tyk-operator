# API Definitions

An API Definition describes the configuration of an API. It instructs Tyk Gateway how to configure the API.

## Implemented Capabilities / Support Status

| Symbol | Description |
| --------- | --------- |
| ✅ | Fully supported |
| ⚠️ | Untested / Requires Documentation |
| ❌️ | Not currently supported |

## API Types

| Type | Support | Comments |
| --------- | --------- | --------- |
| [GraphQL - Proxy](./../config/samples/trevorblades_graphql_proxy.yaml) | ✅ | - |
| [GraphQL - Universal Data Graph](./../config/samples/udg_1.yaml) | ⚠️ | API Change ETA December 2020 |
| HTTP | ✅ | - |
| [HTTPS](./../config/samples/01-tls/example.yaml)️ | ✅️ | - |
| TCP | ✅ | - |
| TLS | ✅ | - |

## Routing

| Type | Supported | Comments |
| ----------- | --------- | --------- |
| [Path-Based](./../config/samples/httpbin.yaml) | ✅ | - |
| [Host-Based](./../config/samples/httpbin_routing_by_hostname.yaml) | ⚠️ | Implemented - Untested |
| Version-Based (Header) | ⚠️ | Untested |
| Version-Based (QueryString) | ⚠️ | Untested |
| Version-Based (Subdomain) | ⚠️ | Untested |

## Client to Gateway Authentication

| Type | Supported | Comments |
| ----------- | --------- | --------- |
| [Keyless (open)](./../config/samples/httpbin.yaml) | ✅ | - |
| [Static Bearer Token](./../config/samples/httpbin_protected.yaml) | ✅ | - |
| JWT | ❌️ | Not implemented |
| OpenID Connect | ❌ | Not implemented |
| OAuth2 | ❌ | Not implemented |
| mTLS | ❌ | Not implemented |
| HMAC | ❌ | Not implemented |
| Basic Authentication | ❌ | Not implemented |
| Plugin Auth - Go | ❌ | Not implemented |
| [Plugin Auth - gRPC](./../bdd/features/api_http_grpc_plugin.feature) | ✅ | - |
| [IP Whitelisting](./api_definitions/ip.md#whitelisting) | ✅ | - |
| [IP Blacklisting](./api_definitions/ip.md#blacklisting) | ✅ | - |

## Gateway to Upstream Authentication

| Type | Supported | Comments |
| ----------- | --------- | --------- |
| Public Key Certificate Pinning | ❌ | Not implemented |
| Upstream Certificates mTLS | ❌ | Not implemented |
| Request Signing | ❌ | Not implemented |

## Features

| Feature | Supported | Comments |
| ----------- | --------- | --------- |
| API Tagging | ✅ | - |
| Config Data | ❌ | Not Implemented |
| Context Variables | ✅ | - |
| [Cross Origin Resource Sharing (CORS)](./../config/samples/httpbin_cors.yaml) | ⚠️  | [See ISSUE #3396 ](https://github.com/TykTechnologies/tyk/issues/3396) |
| Custom Plugins - Go | ⚠️ | Untested |
| [Custom Plugins - gRPC](./../bdd/features/api_http_grpc_plugin.feature) | ✅ | - |
| [Custom Plugins - Javascript](./api_definitions/custom_plugin.md) | ✅ | - |
| Custom Plugins - Lua | ⚠️ | Untested |
| Custom Plugins - Python | ⚠️ | Untested |
| Global Rate Limit | ❌ | Not Implemented |
| [Segment Tags](./../config/samples/httpbin_tagged.yaml) | ✅ | - |
| Tag Headers | ❌ | Not Implemented |
| [Webhooks](./webhooks.md) | ❌ | [WIP #62](https://github.com/TykTechnologies/tyk-operator/issues/62) |

# Pro features

These are features which are only available to tyk PRO users

| Feature | Supported | Comment |
|---------|-----------|---------|
| [Active API](./api_definitions/fields.md#active) |✅ | Untested|

## APIDefinition - Endpoint Middleware

| Endpoint Middleware  | Supported | Comments |
| ----------- | --------- | --------- |
| Analytics - Endpoint Tracking | ⚠️ | Untested |
| [Availability - Circuit Breaker](./../config/samples/httpbin_timeout.yaml) | ❌ | Incompatible types string vs float64 |
| [Availability - Enforced Timeouts](./../config/samples/httpbin_timeout.yaml) | ✅ | - |
| [Headers - Global Request Add](../config/samples/httpbin_global-headers.yaml) | ✅ | - |
| [Headers - Global Request Remove](../config/samples/httpbin_global-headers.yaml) | ✅ | - |
| [Headers - Global Response Add](../config/samples/httpbin_global-headers.yaml) | ✅ | - |
| [Headers - Global Response Remove](../config/samples/httpbin_global-headers.yaml) | ✅ | - |
| [Performance - Cache](./../config/samples/httpbin_cache.yaml) | ✅ | - |
| [Plugin - Virtual Endpoint](./api_definitions/custom_plugin.md) | ✅ | - |
| Security - Allow list | ⚠️ | [Untested #92](https://github.com/TykTechnologies/tyk-operator/issues/93) |
| Security - Block list | ⚠️ | [Untested #92](https://github.com/TykTechnologies/tyk-operator/issues/93) |
| Security - Ignore list | ⚠️ | [Untested #92](https://github.com/TykTechnologies/tyk-operator/issues/93) |
| Transform - Internal | ⚠️ | [Untested #93](https://github.com/TykTechnologies/tyk-operator/issues/93) |
| Transform - Method | ⚠️ | [Untested #93](https://github.com/TykTechnologies/tyk-operator/issues/93) |
| Transform - Mock | ⚠️ | [Untested #93](https://github.com/TykTechnologies/tyk-operator/issues/93) |
| [Transform - Request Body](../config/samples/httpbin_transform.yaml) | ✅ | - |
| [Transform - Response Body](../config/samples/httpbin_transform.yaml) | ✅ | - |
| Transform - Request Body JQ | ⚠️ | Untested - Requires JQ on Gateway Docker Image |
| Transform - Response Body JQ | ⚠️ | Untested - Requires JQ on Gateway Docker Image |
| [Transform - URL Rewrite Basic](../config/samples/url_rewrite_basic.yaml) | ✅️ | - |
| Transform - URL Rewrite Advanced | ⚠️ | Untested |
| [Validate - JSON Schema](../config/samples/httpbin_validate.yaml) | ❌️ | [Issue #59](https://github.com/TykTechnologies/tyk-operator/issues/59) |
| [Validate - Limit Request Size](../config/samples/httpbin_validate.yaml) | ✅️ | - |

## APIDefinition - Migrating Existing APIs

Please visit the [API migration page](./api_definitions/migration.md) for more info
