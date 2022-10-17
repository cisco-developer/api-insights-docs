## api-insights-cli spec

Manage specs

### Options

```
  -h, --help             help for spec
  -s, --service string   service id or nameId for api spec
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
* [api-insights-cli spec get](api-insights-cli_spec_get.md)	 - Get service spec by id
* [api-insights-cli spec list](api-insights-cli_spec_list.md)	 - List service specs

