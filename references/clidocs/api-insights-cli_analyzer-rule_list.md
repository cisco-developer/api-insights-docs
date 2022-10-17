## api-insights-cli analyzer-rule list

List analyzer rules

```
api-insights-cli analyzer-rule list [flags]
```

### Examples

```
  # List analyzer rules
  api-insights-cli analyzer-rule list --analyzer completeness
  api-insights-cli analyzer-rule ls --analyzer completeness
```

### Options

```
  -h, --help   help for list
```

### Options inherited from parent commands

```
  -a, --analyzer string               API spec file analyzer
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

* [api-insights-cli analyzer-rule](api-insights-cli_analyzer-rule.md)	 - Manage analyzer rules

