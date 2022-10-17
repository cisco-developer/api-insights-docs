## api-insights-cli diff

Diff local and remote API specs

```
api-insights-cli diff LOCAL_SPEC [flags]
```

### Examples

```
  # Diff local test data carts spec and latest remote spec for service carts
  api-insights-cli diff testdata/carts.json -s carts --latest

  # Diff local test data carts spec and specific remote spec and fail if API changes broke backward compatibility
  api-insights-cli diff testdata/carts.json -s carts --latest --fail-on-incompatible

  # Diff local test data carts spec and specific remote spec for service carts
  api-insights-cli diff testdata/carts.json -s carts --version 0.0.1 --state Release
  api-insights-cli diff testdata/carts.json -s carts --version 0.0.1 --revision 1

  # Diff specs with specific output format, defaults to text
  api-insights-cli diff testdata/carts.json -s carts --latest -o text
  api-insights-cli diff testdata/carts.json -s carts --latest -o json
  api-insights-cli diff testdata/carts.json -s carts --latest -o markdown
  api-insights-cli diff testdata/carts.json -s carts --latest -o html
```

### Options

```
      --fail-on-incompatible   fail only if API changes broke backward compatibility
  -h, --help                   help for diff
  -l, --latest                 use latest remote spec
  -o, --output string          diff output, one of text (default), json, markdown, html (default "text")
      --revision string        API spec revision
  -s, --service string         service id or nameId for API spec
      --state string           API spec state
      --version string         API spec version
```

### Options inherited from parent commands

```
      --auth-type string              auth type, for example: basic, bearer, oauth2
      --base-path string              API base path, for example: /v1/apiregistry
      --bearer-token string           bearer token for 'bearer-token' auth-type
      --config string                 config file (default is $HOME/.api-insights.yaml)
      --debug                         verbose output
      --header stringArray            API header(s), for example: --header 'Content-Type: application/json' --header 'Accept: application/json'
  -H, --host string                   API host, for example: https://host.example.com
      --oauth2-client-id string       client ID for 'oauth2' auth-type
      --oauth2-client-secret string   client secret for 'oauth2' auth-type
      --oauth2-grant-type string      grant type for 'oauth2' auth-type, for example: client_credentials
      --oauth2-token-url string       token URL for 'oauth2' auth-type
      --password string               password for 'basic' auth-type
      --username string               username for 'basic' auth-type
```

### SEE ALSO

* [api-insights-cli](api-insights-cli.md)	 - api-insights-cli is a CLI for API Insights.

