## api-insights-cli service

Manage services and related specs

### Options

```
  -h, --help   help for service
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
* [api-insights-cli service create](api-insights-cli_service_create.md)	 - Create a service for API spec analysis
* [api-insights-cli service delete](api-insights-cli_service_delete.md)	 - Delete a service by id or name_id
* [api-insights-cli service get](api-insights-cli_service_get.md)	 - Get service by id or name_id
* [api-insights-cli service list](api-insights-cli_service_list.md)	 - List services registered for spec analysis
* [api-insights-cli service uploadspec](api-insights-cli_service_uploadspec.md)	 - Upload local spec for a service under analysis

