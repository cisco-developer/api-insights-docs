## api-insights-cli spec-analysis list

List spec analyses available for a given service

```
api-insights-cli spec-analysis list [flags]
```

### Examples

```
  # List service spec analyses
  api-insights-cli spec-analysis list -s carts --spec_id f7fb047c-c219-11ec-b2ff-5a0acd2870c9
  api-insights-cli spec-analysis ls -s carts --spec_id f7fb047c-c219-11ec-b2ff-5a0acd2870c9
```

### Options

```
  -h, --help             help for list
  -s, --service string   service id or nameId for API spec
      --spec_id string   API spec id
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

* [api-insights-cli spec-analysis](api-insights-cli_spec-analysis.md)	 - Manage spec analyses

