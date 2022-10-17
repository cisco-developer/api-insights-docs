# Detecting Breaking Backward Compatability Changes 

API Insights supports detecting backward compatibility of new API spec by comparing and identifying changes from the previous version. 

## Rules for backward compatible change detection

By default, API Insights provides these rules for detecting backwards compatibility from version-to-version. Examples are provided for each change, but this list of examples is not exhaustive, so you may need to study the differences between your two specification files to understand where the backward incompatible change exists.

The following list represents non-backward compatible API changes. Each example is described in more detail with example spec files further in the section.
1. Changes in URL path structure for previously existing resources.
2. Introduction of new required request query parameters.
3. Introduction of new required representation fields.
4. New resource access restrictions due to authorization policy changes.
5. Removal of previously existing resource operations.
6. Removal of fields previously included in response entities (example).
7. Rejection of previously recognized query parameters and entity fields.
8. Discontinued support of previously recognized media types.
9. Redefinition of existing error response keys and codes.
---
10. Change in expected behavior in the absence of new fields.
11. Change in interpretation of previously recognized query parameters or entity data.
12. Change in value type or format of previously recognized query parameters or entity data.

> **Note**: Rules 10 through 12 are not automatically detected by API Insights, so a developer must review the code. 
 
###  The following represent backward compatible API changes:

1. Introduction of new URL path structures and operations.
2. Introduction of new optional query parameters, and entity fields.
3. Disregarding previously recognized query parameters and entity fields (provided the expected behavior remains consistent).
4. Removal of access restrictions on existing resources.
5. Introduction of support for new media types.
6. Introduction of new error response keys and codes (as defined in STATUSCODES).
7. Deprecation of existing error response keys and codes.


## Changes in URL Path Structure Example

For example, if the spec URL path changed from one spec file to another, this is considered a breaking change and you would have to release a new version and deprecate the old path over time. In a YAML OpenAPI file, the breaking change could look like so, `/api/action/:id/collection/:id` replaced with: `/action/:id/collection/:id` for example. 

## New Required Request Query Parameters Example

Your spec file should not introduce requirements in query parameters that did not exist previously. So when you have a spec file that goes from this not requiring a minimum value in the query parameter:

```
- name: min
          in: query
          description: Minimum value of items to request
          required: false
          schema:
            type: integer
            format: int32
            example: 1
```

To a change making the `min` query parameter required, where the value has changed to `required: true`, you have a breaking change:
```
- name: min
          in: query
          description: Minimum value of items to request
          required: true
          schema:
            type: integer
            format: int32
            example: 1
```

## New Required Representation Fields Example

Often an API has a schema definition used in a request or response that represents an object. In the Petstore example cited with the OpenAPI specification, this representation can be for a pet. 

A breaking change in this example would be if the Petstore API first only required an `id` value to represent a Pet, but then made a change so that a Pet had to be represented in a request with an `id` and a `name` value. 
```
components:
  schemas:
    Pet:
      required:
        - id
      properties:
        id:
          type: integer
          format: int64
```

Here's an example showing the new representation with more required properties that would be flagged as a breaking change:

```
components:
  schemas:
    Pet:
      required:
        - id
        - name
      properties:
        id:
          type: integer
          format: int64
        name:
          type: string
```

## New Resource Access Restrictions

An example of a breaking change for having access restrictions where there were none previously could look like this example:

```
/collections:
    get:
      description: Get a collection of animal species.
      operationId: getSpeciesData
      tags:
        - Species
      security: []
```

```
/collections:
    get:
      description: Get a collection of animal species.
      operationId: getSpeciesData
      tags:
        - Species
      security:
        - bearer: []
```

Notice the addition of the `bearer` array in the `security` section. 

Those are a few examples. Next, you can learn how API Insights can display breaking changes in the Dashboard. 

