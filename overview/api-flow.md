# APIRegistry API Introduction 

The API for API Insights, known internally to the code as `APIRegistry`, supports the following use cases:

* Checking an OAS spec file for API guideline compliance. 
* Generating a diff report for two versions of the same API spec file.
* Identifying non-backwards-compatible breaking changes.

# General Workflow for the API

* Create a new service.
* Create a new spec file with a specific revision value.
* Create a new service spec filerevision `("revision": "2" w/ revised doc)` -> `9a457aec-a101-11ec-ae2e-12664ff946ef`
* Get all service spec files or get a specific service spec file ID
* Create (perform) a service spec file **diff** between spec files `4c9c06c7-a100-11ec-93e7-ca285bf7ce4c` and `9a457aec-a101-11ec-ae2e-12664ff946ef`
* Create (perform) a new service spec file **analysis** for spec file `4c9c06c7-a100-11ec-93e7-ca285bf7ce4c` using `guidelines` analyzer

You can use the reference documentation included here to explore the API. Some examples are included in the following section as well.

## Create a New Service

Submit the following request to create a new service on the API Insights remote service.

**POST /v1/apiregistry/services**

**Request**
```json
{
    "additional_info": {},
    "contact": {},
    "description": "https://wwwin-github.cisco.com/DevNet/Eng_DevEnv",
    "name_id": "devenv",
    "organization_id": "DevNet",
    "product_tag": "devenv",
    "title": "DevEnv"
}
```
**Response (201)**:
```json
{
    "id": "434e6653-a0f3-11ec-a2db-9eaf91c11259",
    "additional_info": {},
    "contact": {},
    "description": "https://wwwin-github.cisco.com/DevNet/Eng_DevEnv",
    "name_id": "devenv",
    "organization_id": "DevNet",
    "product_tag": "devenv",
    "title": "DevEnv"
}
```

Note the service ID given in the `id` field (in this case, `434e6653-a0f3-11ec-a2db-9eaf91c11259`).

## Create a New Spec File

Submit the following request to create a new spec file with a specific revision number. Here, the revision number is `1`, specified in the `revision` field.

**POST /v1/apiregistry/services/434e6653-a0f3-11ec-a2db-9eaf91c11259/specs**

**Request**
```json
{
    "doc_type": "Swagger2",
    "version": "1.0.0",
    "revision": "1",
    "state": "latest",
    "doc": "{\r\n  \"openapi\": \"3.0.1\",\r\n  \"info\": {\r\n    \"title\": \"User Service\",\r\n    \"version\": \"1.0.0\"\r\n  },\r\n  \"paths\": {\r\n    \"\/users\": {\r\n      \"post\": {\r\n        \"requestBody\": {\r\n          \"content\": {\r\n            \"application\/json\": {\r\n              \"schema\": {\r\n                \"properties\": {\r\n                  \"name\": {\r\n                    \"type\": \"string\"\r\n                  }\r\n                },\r\n                \"required\": [\r\n                  \"name\"\r\n                ],\r\n                \"type\": \"object\"\r\n              }\r\n            }\r\n          },\r\n          \"required\": true\r\n        },\r\n        \"responses\": {\r\n          \"201\": {\r\n            \"description\": \"Created\",\r\n            \"content\": {\r\n              \"application\/json\": {\r\n                \"schema\": {\r\n                  \"properties\": {\r\n                    \"id\": {\r\n                      \"type\": \"string\"\r\n                    }\r\n                  },\r\n                  \"required\": [\r\n                    \"id\"\r\n                  ],\r\n                  \"type\": \"object\"\r\n                }\r\n              }\r\n            }\r\n          }\r\n        }\r\n      }\r\n    },\r\n    \"\/users\/{userId}\": {\r\n      \"get\": {\r\n        \"parameters\": [\r\n          {\r\n            \"name\": \"userId\",\r\n            \"in\": \"path\",\r\n            \"required\": true,\r\n            \"schema\": {\r\n              \"type\": \"string\"\r\n            }\r\n          }\r\n        ],\r\n        \"responses\": {\r\n          \"200\": {\r\n            \"description\": \"The user\",\r\n            \"content\": {\r\n              \"application\/json\": {\r\n                \"schema\": {\r\n                  \"properties\": {\r\n                    \"name\": {\r\n                      \"type\": \"string\"\r\n                    }\r\n                  },\r\n                  \"required\": [\r\n                    \"name\"\r\n                  ],\r\n                  \"type\": \"object\"\r\n                }\r\n              }\r\n            }\r\n          }\r\n        }\r\n      }\r\n    }\r\n  }\r\n}"
}
```
**Response (201)**:
```json
{
    "id": "4c9c06c7-a100-11ec-93e7-ca285bf7ce4c",
    "doc": "{\r\n  \"openapi\": \"3.0.1\",\r\n  \"info\": {\r\n    \"title\": \"User Service\",\r\n    \"version\": \"1.0.0\"\r\n  },\r\n  \"paths\": {\r\n    \"/users\": {\r\n      \"post\": {\r\n        \"requestBody\": {\r\n          \"content\": {\r\n            \"application/json\": {\r\n              \"schema\": {\r\n                \"properties\": {\r\n                  \"name\": {\r\n                    \"type\": \"string\"\r\n                  }\r\n                },\r\n                \"required\": [\r\n                  \"name\"\r\n                ],\r\n                \"type\": \"object\"\r\n              }\r\n            }\r\n          },\r\n          \"required\": true\r\n        },\r\n        \"responses\": {\r\n          \"201\": {\r\n            \"description\": \"Created\",\r\n            \"content\": {\r\n              \"application/json\": {\r\n                \"schema\": {\r\n                  \"properties\": {\r\n                    \"id\": {\r\n                      \"type\": \"string\"\r\n                    }\r\n                  },\r\n                  \"required\": [\r\n                    \"id\"\r\n                  ],\r\n                  \"type\": \"object\"\r\n                }\r\n              }\r\n            }\r\n          }\r\n        }\r\n      }\r\n    },\r\n    \"/users/{userId}\": {\r\n      \"get\": {\r\n        \"parameters\": [\r\n          {\r\n            \"name\": \"userId\",\r\n            \"in\": \"path\",\r\n            \"required\": true,\r\n            \"schema\": {\r\n              \"type\": \"string\"\r\n            }\r\n          }\r\n        ],\r\n        \"responses\": {\r\n          \"200\": {\r\n            \"description\": \"The user\",\r\n            \"content\": {\r\n              \"application/json\": {\r\n                \"schema\": {\r\n                  \"properties\": {\r\n                    \"name\": {\r\n                      \"type\": \"string\"\r\n                    }\r\n                  },\r\n                  \"required\": [\r\n                    \"name\"\r\n                  ],\r\n                  \"type\": \"object\"\r\n                }\r\n              }\r\n            }\r\n          }\r\n        }\r\n      }\r\n    }\r\n  }\r\n}",
    "doc_type": "Swagger2",
    "revision": "1",
    "score": 0,
    "service_id": "434e6653-a0f3-11ec-a2db-9eaf91c11259",
    "state": "latest",
    "valid": "",
    "version": "1.0.0"
}
```

## Create a new service spec file `("revision": "2" w/ revised doc)`

**POST /v1/apiregistry/services/434e6653-a0f3-11ec-a2db-9eaf91c11259/specs**

**Request**
```json
{
  "doc_type": "Swagger2",
  "version": "1.0.0",
  "revision": "2",
  "state": "latest",
  "doc": "{\r\n  \"openapi\": \"3.0.1\",\r\n  \"info\": {\r\n    \"title\": \"User Service\",\r\n    \"version\": \"1.0.0\"\r\n  },\r\n  \"paths\": {\r\n    \"\/users\": {\r\n      \"post\": {\r\n        \"requestBody\": {\r\n          \"content\": {\r\n            \"application\/json\": {\r\n              \"schema\": {\r\n                \"properties\": {\r\n                  \"name\": {\r\n                    \"type\": \"string\"\r\n                  }\r\n                },\r\n                \"required\": [\r\n                  \"name\"\r\n                ],\r\n                \"type\": \"object\"\r\n              }\r\n            }\r\n          },\r\n          \"required\": true\r\n        },\r\n        \"responses\": {\r\n          \"201\": {\r\n            \"description\": \"Created\",\r\n            \"content\": {\r\n              \"application\/json\": {\r\n                \"schema\": {\r\n                  \"properties\": {\r\n                    \"id\": {\r\n                      \"type\": \"string\"\r\n                    }\r\n                  },\r\n                  \"required\": [\r\n                    \"id\"\r\n                  ],\r\n                  \"type\": \"object\"\r\n                }\r\n              }\r\n            }\r\n          }\r\n        }\r\n      }\r\n    }\r\n  }\r\n}"
}
```
**Response (201)**:
```json
{
  "id": "9a457aec-a101-11ec-ae2e-12664ff946ef",
  "doc": "{\r\n  \"openapi\": \"3.0.1\",\r\n  \"info\": {\r\n    \"title\": \"User Service\",\r\n    \"version\": \"1.0.0\"\r\n  },\r\n  \"paths\": {\r\n    \"/users\": {\r\n      \"post\": {\r\n        \"requestBody\": {\r\n          \"content\": {\r\n            \"application/json\": {\r\n              \"schema\": {\r\n                \"properties\": {\r\n                  \"name\": {\r\n                    \"type\": \"string\"\r\n                  }\r\n                },\r\n                \"required\": [\r\n                  \"name\"\r\n                ],\r\n                \"type\": \"object\"\r\n              }\r\n            }\r\n          },\r\n          \"required\": true\r\n        },\r\n        \"responses\": {\r\n          \"201\": {\r\n            \"description\": \"Created\",\r\n            \"content\": {\r\n              \"application/json\": {\r\n                \"schema\": {\r\n                  \"properties\": {\r\n                    \"id\": {\r\n                      \"type\": \"string\"\r\n                    }\r\n                  },\r\n                  \"required\": [\r\n                    \"id\"\r\n                  ],\r\n                  \"type\": \"object\"\r\n                }\r\n              }\r\n            }\r\n          }\r\n        }\r\n      }\r\n    }\r\n  }\r\n}",
  "doc_type": "Swagger2",
  "revision": "2",
  "score": 0,
  "service_id": "434e6653-a0f3-11ec-a2db-9eaf91c11259",
  "state": "latest",
  "valid": "",
  "version": "1.0.0"
}
```

> **Note**: Fetchable via `GET /v1/apiregistry/services/434e6653-a0f3-11ec-a2db-9eaf91c11259/specs/9a457aec-a101-11ec-ae2e-12664ff946ef`.

## Get all service spec files or get a specific service spec file

**GET /v1/apiregistry/services/434e6653-a0f3-11ec-a2db-9eaf91c11259/specs**

**GET /v1/apiregistry/services/434e6653-a0f3-11ec-a2db-9eaf91c11259/specs/4c9c06c7-a100-11ec-93e7-ca285bf7ce4c**

**GET /v1/apiregistry/services/434e6653-a0f3-11ec-a2db-9eaf91c11259/specs/9a457aec-a101-11ec-ae2e-12664ff946ef**

## Create a service spec file diff between specs `4c9c06c7-a100-11ec-93e7-ca285bf7ce4c` & `9a457aec-a101-11ec-ae2e-12664ff946ef`

**POST /v1/apiregistry/services/434e6653-a0f3-11ec-a2db-9eaf91c11259/specs/diff**

**Request**
```json
{
    "old_spec_id": "4c9c06c7-a100-11ec-93e7-ca285bf7ce4c",
    "new_spec_id": "9a457aec-a101-11ec-ae2e-12664ff946ef"
}
```
<details>
<summary> Click for Response (200 OK)</summary>

<pre><code>
{
    "id": "3989cf5b-a102-11ec-ae2f-12664ff946ef",
    "new_spec_id": "9a457aec-a101-11ec-ae2e-12664ff946ef",
    "old_spec_id": "4c9c06c7-a100-11ec-93e7-ca285bf7ce4c",
    "result": {
        "changedElements": [
            null
        ],
        "changedExtensions": null,
        "changedOperations": [],
        "changedSchemas": [],
        "compatible": true,
        "deprecatedEndpoints": [],
        "different": false,
        "incompatible": false,
        "missingEndpoints": [],
        "newEndpoints": [],
        "newSpecOpenApi": {
            "components": null,
            "extensions": null,
            "externalDocs": null,
            "info": {
                "contact": null,
                "description": null,
                "extensions": null,
                "license": null,
                "termsOfService": null,
                "title": "User Service",
                "version": "1.0.0"
            },
            "openapi": "3.0.1",
            "paths": {
                "/users": {
                    "$ref": null,
                    "delete": null,
                    "description": null,
                    "extensions": null,
                    "get": null,
                    "head": null,
                    "options": null,
                    "parameters": null,
                    "patch": null,
                    "post": {
                        "callbacks": null,
                        "deprecated": null,
                        "description": null,
                        "extensions": null,
                        "externalDocs": null,
                        "operationId": null,
                        "parameters": null,
                        "requestBody": {
                            "$ref": null,
                            "content": {
                                "application/json": {
                                    "encoding": null,
                                    "example": null,
                                    "exampleSetFlag": false,
                                    "examples": null,
                                    "extensions": null,
                                    "schema": {
                                        "$ref": null,
                                        "additionalProperties": null,
                                        "default": null,
                                        "deprecated": null,
                                        "description": null,
                                        "discriminator": null,
                                        "enum": null,
                                        "example": null,
                                        "exampleSetFlag": false,
                                        "exclusiveMaximum": null,
                                        "exclusiveMinimum": null,
                                        "extensions": null,
                                        "externalDocs": null,
                                        "format": null,
                                        "maxItems": null,
                                        "maxLength": null,
                                        "maxProperties": null,
                                        "maximum": null,
                                        "minItems": null,
                                        "minLength": null,
                                        "minProperties": null,
                                        "minimum": null,
                                        "multipleOf": null,
                                        "not": null,
                                        "nullable": null,
                                        "pattern": null,
                                        "properties": {
                                            "name": {
                                                "$ref": null,
                                                "additionalProperties": null,
                                                "default": null,
                                                "deprecated": null,
                                                "description": null,
                                                "discriminator": null,
                                                "enum": null,
                                                "example": null,
                                                "exampleSetFlag": false,
                                                "exclusiveMaximum": null,
                                                "exclusiveMinimum": null,
                                                "extensions": null,
                                                "externalDocs": null,
                                                "format": null,
                                                "maxItems": null,
                                                "maxLength": null,
                                                "maxProperties": null,
                                                "maximum": null,
                                                "minItems": null,
                                                "minLength": null,
                                                "minProperties": null,
                                                "minimum": null,
                                                "multipleOf": null,
                                                "not": null,
                                                "nullable": null,
                                                "pattern": null,
                                                "properties": null,
                                                "readOnly": null,
                                                "required": null,
                                                "title": null,
                                                "type": "string",
                                                "uniqueItems": null,
                                                "writeOnly": null,
                                                "xml": null
                                            }
                                        },
                                        "readOnly": null,
                                        "required": [
                                            "name"
                                        ],
                                        "title": null,
                                        "type": "object",
                                        "uniqueItems": null,
                                        "writeOnly": null,
                                        "xml": null
                                    }
                                }
                            },
                            "description": null,
                            "extensions": null,
                            "required": true
                        },
                        "responses": {
                            "201": {
                                "$ref": null,
                                "content": {
                                    "application/json": {
                                        "encoding": null,
                                        "example": null,
                                        "exampleSetFlag": false,
                                        "examples": null,
                                        "extensions": null,
                                        "schema": {
                                            "$ref": null,
                                            "additionalProperties": null,
                                            "default": null,
                                            "deprecated": null,
                                            "description": null,
                                            "discriminator": null,
                                            "enum": null,
                                            "example": null,
                                            "exampleSetFlag": false,
                                            "exclusiveMaximum": null,
                                            "exclusiveMinimum": null,
                                            "extensions": null,
                                            "externalDocs": null,
                                            "format": null,
                                            "maxItems": null,
                                            "maxLength": null,
                                            "maxProperties": null,
                                            "maximum": null,
                                            "minItems": null,
                                            "minLength": null,
                                            "minProperties": null,
                                            "minimum": null,
                                            "multipleOf": null,
                                            "not": null,
                                            "nullable": null,
                                            "pattern": null,
                                            "properties": {
                                                "id": {
                                                    "$ref": null,
                                                    "additionalProperties": null,
                                                    "default": null,
                                                    "deprecated": null,
                                                    "description": null,
                                                    "discriminator": null,
                                                    "enum": null,
                                                    "example": null,
                                                    "exampleSetFlag": false,
                                                    "exclusiveMaximum": null,
                                                    "exclusiveMinimum": null,
                                                    "extensions": null,
                                                    "externalDocs": null,
                                                    "format": null,
                                                    "maxItems": null,
                                                    "maxLength": null,
                                                    "maxProperties": null,
                                                    "maximum": null,
                                                    "minItems": null,
                                                    "minLength": null,
                                                    "minProperties": null,
                                                    "minimum": null,
                                                    "multipleOf": null,
                                                    "not": null,
                                                    "nullable": null,
                                                    "pattern": null,
                                                    "properties": null,
                                                    "readOnly": null,
                                                    "required": null,
                                                    "title": null,
                                                    "type": "string",
                                                    "uniqueItems": null,
                                                    "writeOnly": null,
                                                    "xml": null
                                                }
                                            },
                                            "readOnly": null,
                                            "required": [
                                                "id"
                                            ],
                                            "title": null,
                                            "type": "object",
                                            "uniqueItems": null,
                                            "writeOnly": null,
                                            "xml": null
                                        }
                                    }
                                },
                                "description": "Created",
                                "extensions": null,
                                "headers": null,
                                "links": null
                            }
                        },
                        "security": null,
                        "servers": null,
                        "summary": null,
                        "tags": null
                    },
                    "put": null,
                    "servers": null,
                    "summary": null,
                    "trace": null
                },
                "/users/{userId}": {
                    "$ref": null,
                    "delete": null,
                    "description": null,
                    "extensions": null,
                    "get": {
                        "callbacks": null,
                        "deprecated": null,
                        "description": null,
                        "extensions": null,
                        "externalDocs": null,
                        "operationId": null,
                        "parameters": [],
                        "requestBody": null,
                        "responses": {
                            "200": {
                                "$ref": null,
                                "content": {
                                    "application/json": {
                                        "encoding": null,
                                        "example": null,
                                        "exampleSetFlag": false,
                                        "examples": null,
                                        "extensions": null,
                                        "schema": {
                                            "$ref": null,
                                            "additionalProperties": null,
                                            "default": null,
                                            "deprecated": null,
                                            "description": null,
                                            "discriminator": null,
                                            "enum": null,
                                            "example": null,
                                            "exampleSetFlag": false,
                                            "exclusiveMaximum": null,
                                            "exclusiveMinimum": null,
                                            "extensions": null,
                                            "externalDocs": null,
                                            "format": null,
                                            "maxItems": null,
                                            "maxLength": null,
                                            "maxProperties": null,
                                            "maximum": null,
                                            "minItems": null,
                                            "minLength": null,
                                            "minProperties": null,
                                            "minimum": null,
                                            "multipleOf": null,
                                            "not": null,
                                            "nullable": null,
                                            "pattern": null,
                                            "properties": {
                                                "name": {
                                                    "$ref": null,
                                                    "additionalProperties": null,
                                                    "default": null,
                                                    "deprecated": null,
                                                    "description": null,
                                                    "discriminator": null,
                                                    "enum": null,
                                                    "example": null,
                                                    "exampleSetFlag": false,
                                                    "exclusiveMaximum": null,
                                                    "exclusiveMinimum": null,
                                                    "extensions": null,
                                                    "externalDocs": null,
                                                    "format": null,
                                                    "maxItems": null,
                                                    "maxLength": null,
                                                    "maxProperties": null,
                                                    "maximum": null,
                                                    "minItems": null,
                                                    "minLength": null,
                                                    "minProperties": null,
                                                    "minimum": null,
                                                    "multipleOf": null,
                                                    "not": null,
                                                    "nullable": null,
                                                    "pattern": null,
                                                    "properties": null,
                                                    "readOnly": null,
                                                    "required": null,
                                                    "title": null,
                                                    "type": "string",
                                                    "uniqueItems": null,
                                                    "writeOnly": null,
                                                    "xml": null
                                                }
                                            },
                                            "readOnly": null,
                                            "required": [
                                                "name"
                                            ],
                                            "title": null,
                                            "type": "object",
                                            "uniqueItems": null,
                                            "writeOnly": null,
                                            "xml": null
                                        }
                                    }
                                },
                                "description": "The user",
                                "extensions": null,
                                "headers": null,
                                "links": null
                            }
                        },
                        "security": null,
                        "servers": null,
                        "summary": null,
                        "tags": null
                    },
                    "head": null,
                    "options": null,
                    "parameters": null,
                    "patch": null,
                    "post": null,
                    "put": null,
                    "servers": null,
                    "summary": null,
                    "trace": null
                }
            },
            "security": null,
            "servers": [
                {
                    "description": null,
                    "extensions": null,
                    "url": "/",
                    "variables": null
                }
            ],
            "tags": null
        },
        "oldSpecOpenApi": {
            "components": null,
            "extensions": null,
            "externalDocs": null,
            "info": {
                "contact": null,
                "description": null,
                "extensions": null,
                "license": null,
                "termsOfService": null,
                "title": "User Service",
                "version": "1.0.0"
            },
            "openapi": "3.0.1",
            "paths": {
                "/users": {
                    "$ref": null,
                    "delete": null,
                    "description": null,
                    "extensions": null,
                    "get": null,
                    "head": null,
                    "options": null,
                    "parameters": null,
                    "patch": null,
                    "post": {
                        "callbacks": null,
                        "deprecated": null,
                        "description": null,
                        "extensions": null,
                        "externalDocs": null,
                        "operationId": null,
                        "parameters": null,
                        "requestBody": {
                            "$ref": null,
                            "content": {
                                "application/json": {
                                    "encoding": null,
                                    "example": null,
                                    "exampleSetFlag": false,
                                    "examples": null,
                                    "extensions": null,
                                    "schema": {
                                        "$ref": null,
                                        "additionalProperties": null,
                                        "default": null,
                                        "deprecated": null,
                                        "description": null,
                                        "discriminator": null,
                                        "enum": null,
                                        "example": null,
                                        "exampleSetFlag": false,
                                        "exclusiveMaximum": null,
                                        "exclusiveMinimum": null,
                                        "extensions": null,
                                        "externalDocs": null,
                                        "format": null,
                                        "maxItems": null,
                                        "maxLength": null,
                                        "maxProperties": null,
                                        "maximum": null,
                                        "minItems": null,
                                        "minLength": null,
                                        "minProperties": null,
                                        "minimum": null,
                                        "multipleOf": null,
                                        "not": null,
                                        "nullable": null,
                                        "pattern": null,
                                        "properties": {
                                            "name": {
                                                "$ref": null,
                                                "additionalProperties": null,
                                                "default": null,
                                                "deprecated": null,
                                                "description": null,
                                                "discriminator": null,
                                                "enum": null,
                                                "example": null,
                                                "exampleSetFlag": false,
                                                "exclusiveMaximum": null,
                                                "exclusiveMinimum": null,
                                                "extensions": null,
                                                "externalDocs": null,
                                                "format": null,
                                                "maxItems": null,
                                                "maxLength": null,
                                                "maxProperties": null,
                                                "maximum": null,
                                                "minItems": null,
                                                "minLength": null,
                                                "minProperties": null,
                                                "minimum": null,
                                                "multipleOf": null,
                                                "not": null,
                                                "nullable": null,
                                                "pattern": null,
                                                "properties": null,
                                                "readOnly": null,
                                                "required": null,
                                                "title": null,
                                                "type": "string",
                                                "uniqueItems": null,
                                                "writeOnly": null,
                                                "xml": null
                                            }
                                        },
                                        "readOnly": null,
                                        "required": [
                                            "name"
                                        ],
                                        "title": null,
                                        "type": "object",
                                        "uniqueItems": null,
                                        "writeOnly": null,
                                        "xml": null
                                    }
                                }
                            },
                            "description": null,
                            "extensions": null,
                            "required": true
                        },
                        "responses": {
                            "201": {
                                "$ref": null,
                                "content": {
                                    "application/json": {
                                        "encoding": null,
                                        "example": null,
                                        "exampleSetFlag": false,
                                        "examples": null,
                                        "extensions": null,
                                        "schema": {
                                            "$ref": null,
                                            "additionalProperties": null,
                                            "default": null,
                                            "deprecated": null,
                                            "description": null,
                                            "discriminator": null,
                                            "enum": null,
                                            "example": null,
                                            "exampleSetFlag": false,
                                            "exclusiveMaximum": null,
                                            "exclusiveMinimum": null,
                                            "extensions": null,
                                            "externalDocs": null,
                                            "format": null,
                                            "maxItems": null,
                                            "maxLength": null,
                                            "maxProperties": null,
                                            "maximum": null,
                                            "minItems": null,
                                            "minLength": null,
                                            "minProperties": null,
                                            "minimum": null,
                                            "multipleOf": null,
                                            "not": null,
                                            "nullable": null,
                                            "pattern": null,
                                            "properties": {
                                                "id": {
                                                    "$ref": null,
                                                    "additionalProperties": null,
                                                    "default": null,
                                                    "deprecated": null,
                                                    "description": null,
                                                    "discriminator": null,
                                                    "enum": null,
                                                    "example": null,
                                                    "exampleSetFlag": false,
                                                    "exclusiveMaximum": null,
                                                    "exclusiveMinimum": null,
                                                    "extensions": null,
                                                    "externalDocs": null,
                                                    "format": null,
                                                    "maxItems": null,
                                                    "maxLength": null,
                                                    "maxProperties": null,
                                                    "maximum": null,
                                                    "minItems": null,
                                                    "minLength": null,
                                                    "minProperties": null,
                                                    "minimum": null,
                                                    "multipleOf": null,
                                                    "not": null,
                                                    "nullable": null,
                                                    "pattern": null,
                                                    "properties": null,
                                                    "readOnly": null,
                                                    "required": null,
                                                    "title": null,
                                                    "type": "string",
                                                    "uniqueItems": null,
                                                    "writeOnly": null,
                                                    "xml": null
                                                }
                                            },
                                            "readOnly": null,
                                            "required": [
                                                "id"
                                            ],
                                            "title": null,
                                            "type": "object",
                                            "uniqueItems": null,
                                            "writeOnly": null,
                                            "xml": null
                                        }
                                    }
                                },
                                "description": "Created",
                                "extensions": null,
                                "headers": null,
                                "links": null
                            }
                        },
                        "security": null,
                        "servers": null,
                        "summary": null,
                        "tags": null
                    },
                    "put": null,
                    "servers": null,
                    "summary": null,
                    "trace": null
                },
                "/users/{userId}": {
                    "$ref": null,
                    "delete": null,
                    "description": null,
                    "extensions": null,
                    "get": {
                        "callbacks": null,
                        "deprecated": null,
                        "description": null,
                        "extensions": null,
                        "externalDocs": null,
                        "operationId": null,
                        "parameters": [
                            {
                                "$ref": null,
                                "allowEmptyValue": null,
                                "allowReserved": null,
                                "content": null,
                                "deprecated": null,
                                "description": null,
                                "example": null,
                                "examples": null,
                                "explode": false,
                                "extensions": null,
                                "in": "path",
                                "name": "userId",
                                "required": true,
                                "schema": {
                                    "$ref": null,
                                    "additionalProperties": null,
                                    "default": null,
                                    "deprecated": null,
                                    "description": null,
                                    "discriminator": null,
                                    "enum": null,
                                    "example": null,
                                    "exampleSetFlag": false,
                                    "exclusiveMaximum": null,
                                    "exclusiveMinimum": null,
                                    "extensions": null,
                                    "externalDocs": null,
                                    "format": null,
                                    "maxItems": null,
                                    "maxLength": null,
                                    "maxProperties": null,
                                    "maximum": null,
                                    "minItems": null,
                                    "minLength": null,
                                    "minProperties": null,
                                    "minimum": null,
                                    "multipleOf": null,
                                    "not": null,
                                    "nullable": null,
                                    "pattern": null,
                                    "properties": null,
                                    "readOnly": null,
                                    "required": null,
                                    "title": null,
                                    "type": "string",
                                    "uniqueItems": null,
                                    "writeOnly": null,
                                    "xml": null
                                },
                                "style": "SIMPLE"
                            }
                        ],
                        "requestBody": null,
                        "responses": {
                            "200": {
                                "$ref": null,
                                "content": {
                                    "application/json": {
                                        "encoding": null,
                                        "example": null,
                                        "exampleSetFlag": false,
                                        "examples": null,
                                        "extensions": null,
                                        "schema": {
                                            "$ref": null,
                                            "additionalProperties": null,
                                            "default": null,
                                            "deprecated": null,
                                            "description": null,
                                            "discriminator": null,
                                            "enum": null,
                                            "example": null,
                                            "exampleSetFlag": false,
                                            "exclusiveMaximum": null,
                                            "exclusiveMinimum": null,
                                            "extensions": null,
                                            "externalDocs": null,
                                            "format": null,
                                            "maxItems": null,
                                            "maxLength": null,
                                            "maxProperties": null,
                                            "maximum": null,
                                            "minItems": null,
                                            "minLength": null,
                                            "minProperties": null,
                                            "minimum": null,
                                            "multipleOf": null,
                                            "not": null,
                                            "nullable": null,
                                            "pattern": null,
                                            "properties": {
                                                "name": {
                                                    "$ref": null,
                                                    "additionalProperties": null,
                                                    "default": null,
                                                    "deprecated": null,
                                                    "description": null,
                                                    "discriminator": null,
                                                    "enum": null,
                                                    "example": null,
                                                    "exampleSetFlag": false,
                                                    "exclusiveMaximum": null,
                                                    "exclusiveMinimum": null,
                                                    "extensions": null,
                                                    "externalDocs": null,
                                                    "format": null,
                                                    "maxItems": null,
                                                    "maxLength": null,
                                                    "maxProperties": null,
                                                    "maximum": null,
                                                    "minItems": null,
                                                    "minLength": null,
                                                    "minProperties": null,
                                                    "minimum": null,
                                                    "multipleOf": null,
                                                    "not": null,
                                                    "nullable": null,
                                                    "pattern": null,
                                                    "properties": null,
                                                    "readOnly": null,
                                                    "required": null,
                                                    "title": null,
                                                    "type": "string",
                                                    "uniqueItems": null,
                                                    "writeOnly": null,
                                                    "xml": null
                                                }
                                            },
                                            "readOnly": null,
                                            "required": [
                                                "name"
                                            ],
                                            "title": null,
                                            "type": "object",
                                            "uniqueItems": null,
                                            "writeOnly": null,
                                            "xml": null
                                        }
                                    }
                                },
                                "description": "The user",
                                "extensions": null,
                                "headers": null,
                                "links": null
                            }
                        },
                        "security": null,
                        "servers": null,
                        "summary": null,
                        "tags": null
                    },
                    "head": null,
                    "options": null,
                    "parameters": null,
                    "patch": null,
                    "post": null,
                    "put": null,
                    "servers": null,
                    "summary": null,
                    "trace": null
                }
            },
            "security": null,
            "servers": [
                {
                    "description": null,
                    "extensions": null,
                    "url": "/",
                    "variables": null
                }
            ],
            "tags": null
        },
        "unchanged": true
    },
    "service_id": "434e6653-a0f3-11ec-a2db-9eaf91c11259",
    "status": "Diffed"
}
</code></pre>
</details>

> **Note**: Fetchable via `GET /v1/apiregistry/services/specs/diff/3989cf5b-a102-11ec-ae2f-12664ff946ef`.

## Create a new service spec file analysis for spec file `4c9c06c7-a100-11ec-93e7-ca285bf7ce4c` using `guidelines` analyzer

**POST /v1/apiregistry/services/434e6653-a0f3-11ec-a2db-9eaf91c11259/specs/4c9c06c7-a100-11ec-93e7-ca285bf7ce4c/analyze**

**Request**
```json
{
  "analyzers": [
    "guidelines"
  ]
}
```

<details>
<summary> Click for Response (200 OK) </summary>

<pre><code>
{
    "results": {
        "guidelines": {
            "id": "d99865d5-a106-11ec-8859-52d3a6b0066b",
            "analyzer": "guidelines",
            "result": [
                {
                    "code": "oas3-api-servers",
                    "message": "OpenAPI `servers` must be present and non-empty array.",
                    "path": [],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 0,
                            "line": 0
                        }
                    },
                    "severity": 0,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "oas3-path-based-versioning-error",
                    "message": "API uses path-based versioning. (https://apistyleguide.cisco.com/#rest-versioning/API.REST.VERSION.01)",
                    "path": [],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 0,
                            "line": 0
                        }
                    },
                    "severity": 0,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "openapi-tags",
                    "message": "OpenAPI object should have non-empty `tags` array.",
                    "path": [],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 0,
                            "line": 0
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "info-contact",
                    "message": "Info object should contain `contact` object.",
                    "path": [
                        "info"
                    ],
                    "range": {
                        "end": {
                            "character": 22,
                            "line": 4
                        },
                        "start": {
                            "character": 9,
                            "line": 2
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "info-description",
                    "message": "OpenAPI object info `description` must be present and non-empty string.",
                    "path": [
                        "info"
                    ],
                    "range": {
                        "end": {
                            "character": 22,
                            "line": 4
                        },
                        "start": {
                            "character": 9,
                            "line": 2
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "info-license",
                    "message": "OpenAPI object `info` should contain a `license` object.",
                    "path": [
                        "info"
                    ],
                    "range": {
                        "end": {
                            "character": 22,
                            "line": 4
                        },
                        "start": {
                            "character": 9,
                            "line": 2
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "license-url",
                    "message": "License object should include `url`.",
                    "path": [
                        "info"
                    ],
                    "range": {
                        "end": {
                            "character": 22,
                            "line": 4
                        },
                        "start": {
                            "character": 9,
                            "line": 2
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "authenticate-requests",
                    "message": "API.REST.SECURITY.03: My API authenticates and authorizes all requests (https://apistyleguide.cisco.com/#rest-security/API.REST.SECURITY.03)",
                    "path": [
                        "paths",
                        "/users",
                        "post"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 41
                        },
                        "start": {
                            "character": 13,
                            "line": 8
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "operation-description",
                    "message": "Operation `description` must be present and non-empty string.",
                    "path": [
                        "paths",
                        "/users",
                        "post"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 41
                        },
                        "start": {
                            "character": 13,
                            "line": 8
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "operation-operationId",
                    "message": "Operation should have an `operationId`.",
                    "path": [
                        "paths",
                        "/users",
                        "post"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 41
                        },
                        "start": {
                            "character": 13,
                            "line": 8
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "operation-tags",
                    "message": "Operation should have non-empty `tags` array.",
                    "path": [
                        "paths",
                        "/users",
                        "post"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 41
                        },
                        "start": {
                            "character": 13,
                            "line": 8
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "operation-default-response",
                    "message": "Operations must have a default response.",
                    "path": [
                        "paths",
                        "/users",
                        "post",
                        "responses"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 41
                        },
                        "start": {
                            "character": 20,
                            "line": 27
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "date-response-header-requirement",
                    "message": "All responses must include a 'Date' header (https://apistyleguide.cisco.com/#rest-style/API.REST.STYLE.16)",
                    "path": [
                        "paths",
                        "/users",
                        "post",
                        "responses",
                        "201"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 41
                        },
                        "start": {
                            "character": 16,
                            "line": 28
                        }
                    },
                    "severity": 0,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "post-header",
                    "message": "POST operations that create resources should include a Location header (https://apistyleguide.cisco.com/#rest-style/API.REST.STYLE.02)",
                    "path": [
                        "paths",
                        "/users",
                        "post",
                        "responses",
                        "201"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 41
                        },
                        "start": {
                            "character": 16,
                            "line": 28
                        }
                    },
                    "severity": 0,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "tracking-id-header-requirement",
                    "message": "All responses must include a 'TrackingID' header (https://apistyleguide.cisco.com/#rest-style/API.REST.STYLE.18)",
                    "path": [
                        "paths",
                        "/users",
                        "post",
                        "responses",
                        "201"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 41
                        },
                        "start": {
                            "character": 16,
                            "line": 28
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "authenticate-requests",
                    "message": "API.REST.SECURITY.03: My API authenticates and authorizes all requests (https://apistyleguide.cisco.com/#rest-security/API.REST.SECURITY.03)",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 12,
                            "line": 50
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "operation-description",
                    "message": "Operation `description` must be present and non-empty string.",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 12,
                            "line": 50
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "operation-operationId",
                    "message": "Operation should have an `operationId`.",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 12,
                            "line": 50
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "operation-tags",
                    "message": "Operation should have non-empty `tags` array.",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 12,
                            "line": 50
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "oas3-parameter-description",
                    "message": "Parameter objects should have a `description`.",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get",
                        "parameters",
                        "0"
                    ],
                    "range": {
                        "end": {
                            "character": 30,
                            "line": 57
                        },
                        "start": {
                            "character": 10,
                            "line": 52
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "operation-default-response",
                    "message": "Operations must have a default response.",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get",
                        "responses"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 20,
                            "line": 61
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "date-response-header-requirement",
                    "message": "All responses must include a 'Date' header (https://apistyleguide.cisco.com/#rest-style/API.REST.STYLE.16)",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get",
                        "responses",
                        "200"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 16,
                            "line": 62
                        }
                    },
                    "severity": 0,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "tracking-id-header-requirement",
                    "message": "All responses must include a 'TrackingID' header (https://apistyleguide.cisco.com/#rest-style/API.REST.STYLE.18)",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get",
                        "responses",
                        "200"
                    ],
                    "range": {
                        "end": {
                            "character": 34,
                            "line": 75
                        },
                        "start": {
                            "character": 16,
                            "line": 62
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                },
                {
                    "code": "reason-phrase",
                    "message": "Reason phrase \"The user\" needs to match \"OK\"",
                    "path": [
                        "paths",
                        "/users/{userId}",
                        "get",
                        "responses",
                        "200",
                        "description"
                    ],
                    "range": {
                        "end": {
                            "character": 37,
                            "line": 63
                        },
                        "start": {
                            "character": 27,
                            "line": 63
                        }
                    },
                    "severity": 1,
                    "source": "/tmp/lint-1646981127460320742-in-3458901767.json"
                }
            ],
            "score": 0,
            "service_id": "434e6653-a0f3-11ec-a2db-9eaf91c11259",
            "spec_id": "4c9c06c7-a100-11ec-93e7-ca285bf7ce4c",
            "status": "Analyzed"
        }
    }
}
</code></pre>
</details>

With these examples, you can see the general workflow for using the API for the API Insights use cases.