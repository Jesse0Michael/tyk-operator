# Tyk Operator

- [Quickstart API Definitions](#quickstart-api-definitions)
- [Installation](#installation)
- [IDE Integration](#ide-integration)
  - [VS Code](#vs-code)
- [Community](#community)

Tyk Operator contains various custom resources and controllers which enable Full-Lifecycle API Management with Tyk by
extending the Kubernetes API.

Read more about the [concepts here](./docs/concepts.md).

Custom Tyk Objects are available as [CRDs](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
and documentation for each of these custom resources are available:

- [API Definitions](./docs/api_definitions.md)
- [WebHooks](./docs/webhooks.md)
- [Security Policies](./docs/policies.md)

Tyk Operator also contains an [Ingress Controller](./docs/ingress.md).

![Demo](./docs/img/demo.svg)

## Quickstart API Definitions

<details><summary>HTTP Proxy</summary>
<p>

```yaml
apiVersion: tyk.tyk.io/v1alpha1
kind: ApiDefinition
metadata:
  name: httpbin
spec:
  name: httpbin
  use_keyless: true
  protocol: http
  active: true
  org_id: acme.com
  proxy:
    target_url: http://httpbin.org
    listen_path: /httpbin
    strip_listen_path: true
```

</p>
</details>

<details><summary>TCP Proxy</summary>
<p>

```yaml
apiVersion: tyk.tyk.io/v1alpha1
kind: ApiDefinition
metadata:
  name: redis-tcp
spec:
  name: redis-tcp
  active: true
  protocol: tcp
  listen_port: 6380
  proxy:
    target_url: tcp://localhost:6379
```

</p>
</details>

<details><summary>GraphQL Proxy</summary>
<p>

```yaml
apiVersion: tyk.tyk.io/v1alpha1
kind: ApiDefinition
metadata:
  name: trevorblades
spec:
  name: trevorblades
  use_keyless: true
  protocol: http
  active: true
  proxy:
    target_url: https://countries.trevorblades.com
    listen_path: /trevorblades
    strip_listen_path: true
  graphql:
    enabled: true
    execution_mode: proxyOnly
    schema: |
      directive @cacheControl(maxAge: Int, scope: CacheControlScope) on FIELD_DEFINITION | OBJECT | INTERFACE

      enum CacheControlScope {
        PUBLIC
        PRIVATE
      }

      type Continent {
        code: ID!
        name: String!
        countries: [Country!]!
      }

      input ContinentFilterInput {
        code: StringQueryOperatorInput
      }

      type Country {
        code: ID!
        name: String!
        native: String!
        phone: String!
        continent: Continent!
        capital: String
        currency: String
        languages: [Language!]!
        emoji: String!
        emojiU: String!
        states: [State!]!
      }

      input CountryFilterInput {
        code: StringQueryOperatorInput
        currency: StringQueryOperatorInput
        continent: StringQueryOperatorInput
      }

      type Language {
        code: ID!
        name: String
        native: String
        rtl: Boolean!
      }

      input LanguageFilterInput {
        code: StringQueryOperatorInput
      }

      type Query {
        continents(filter: ContinentFilterInput): [Continent!]!
        continent(code: ID!): Continent
        countries(filter: CountryFilterInput): [Country!]!
        country(code: ID!): Country
        languages(filter: LanguageFilterInput): [Language!]!
        language(code: ID!): Language
      }

      type State {
        code: String
        name: String!
        country: Country!
      }

      input StringQueryOperatorInput {
        eq: String
        ne: String
        in: [String]
        nin: [String]
        regex: String
        glob: String
      }

      """The `Upload` scalar type represents a file upload."""
      scalar Upload
    playground:
      enabled: true
      path: /playground
```

</p>
</details>

<details><summary>Universal Data Graph - Stitching REST with GraphQL</summary>
<p>

```yaml
apiVersion: tyk.tyk.io/v1alpha1
kind: ApiDefinition
metadata:
  name: udg
spec:
  name: Universal Data Graph Example
  use_keyless: true
  protocol: http
  active: true
  proxy:
    target_url: ""
    listen_path: /udg
    strip_listen_path: true
  graphql:
    enabled: true
    execution_mode: executionEngine
    schema: |
      type Country {
        name: String
        code: String
        restCountry: RestCountry
      }

      type Query {
        countries: [Country]
      }

      type RestCountry {
        altSpellings: [String]
        subregion: String
        population: String
      }
    type_field_configurations:
      - type_name: Query
        field_name: countries
        mapping:
          disabled: false
          path: countries
        data_source:
          kind: GraphQLDataSource
          data_source_config:
            url: "https://countries.trevorblades.com"
            method: POST
            status_code_type_name_mappings: []
      - type_name: Country
        field_name: restCountry
        mapping:
          disabled: true
          path: ""
        data_source:
          kind: HTTPJSONDataSource
          data_source_config:
            url: "https://restcountries.eu/rest/v2/alpha/{{ .object.code }}"
            method: GET
            default_type_name: RestCountry
            status_code_type_name_mappings:
              - status_code: 200
    playground:
      enabled: true
      path: /playground
```

</p>
</details>

## Installation

[Installing the Tyk Operator](./docs/installation/installation.md).

Tyk Operator is under active development.

We are building the operator to enable you to build and ship your APIs faster and more safely. We are actively working
on improving & stabilising our v1alpha1 custom resources, whilst also working on a helm chart so that you can manage
your tyk-operator deployment.

If you find any defects, please [raise an issue](https://github.com/TykTechnologies/tyk-operator/issues/new).
We welcome code contributions as well.

If you require any features that we have not yet implemented, please take the time to
[write a GH issue](https://github.com/TykTechnologies/tyk-operator/issues/new/choose) detailing your use case so that
we may prioritise accordingly.

For larger and more in-depth feature requests, please consider [starting an RFC thread](https://github.com/TykTechnologies/tyk-operator/discussions/new)
in the [Discussions area](https://github.com/TykTechnologies/tyk-operator/discussions).

## IDE Integration

This section details the steps required to add K8s extensions to popular IDEs.

### VS Code

[Watch video tutorial here](http://www.youtube.com/watch?v=Kdrfp6aAZEU).

Steps:

1. Go to the following link: <https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools>
2. Click on Install. This will prompt you to open Visual Studios.
3. Click Open Visual Studios at the subsequent prompt. This will open VS Code and take you to the Extensions' section.
4. Click Install in the Kubernetes extension page.

Note: The extension should take effect immediately. In case it doesn't, simply restart VS Code.

## Community

- [Configuring your development environment](./docs/development.md)
- [Request a feature](https://github.com/TykTechnologies/tyk-operator/issues)
- [Got an Idea or RFC](https://github.com/TykTechnologies/tyk-operator/discussions/categories/ideas)
- [Found a Defect](https://github.com/TykTechnologies/tyk-operator/issues)
- [Got a Question](https://github.com/TykTechnologies/tyk-operator/discussions/categories/q-a)
- [Show and Tell](https://github.com/TykTechnologies/tyk-operator/discussions/categories/show-and-tell)
