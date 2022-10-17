## api-insights-cli analyzer-rule

Manage analyzer rules

### Options

```
  -a, --analyzer string   API spec file analyzer
  -h, --help              help for analyzer-rule
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
* [api-insights-cli analyzer-rule get](api-insights-cli_analyzer-rule_get.md)	 - Get analyzer rule by id or name_id
* [api-insights-cli analyzer-rule import](api-insights-cli_analyzer-rule_import.md)	 - Import analyzer rules from a local rules file
* [api-insights-cli analyzer-rule list](api-insights-cli_analyzer-rule_list.md)	 - List analyzer rules

