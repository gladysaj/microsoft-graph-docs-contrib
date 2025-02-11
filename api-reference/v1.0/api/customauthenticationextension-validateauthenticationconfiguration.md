---
title: "customAuthenticationExtension: validateAuthenticationConfiguration"
description: "An API to check validity of the endpoint and authentication configuration for a customAuthenticationExtension."
author: "soneff"
ms.localizationpriority: medium
ms.subservice: "entra-sign-in"
doc_type: apiPageType
---

# customAuthenticationExtension: validateAuthenticationConfiguration
Namespace: microsoft.graph

An API to check validity of the endpoint and and authentication configuration for a customAuthenticationExtension.

## Permissions
Choose the permission or permissions marked as least privileged for this API. Use a higher privileged permission or permissions [only if your app requires it](/graph/permissions-overview#best-practices-for-using-microsoft-graph-permissions). For details about delegated and application permissions, see [Permission types](/graph/permissions-overview#permission-types). To learn more about these permissions, see the [permissions reference](/graph/permissions-reference).

<!-- { "blockType": "permissions", "name": "customauthenticationextension_validateauthenticationconfiguration" } -->
[!INCLUDE [permissions-table](../includes/permissions/customauthenticationextension-validateauthenticationconfiguration-permissions.md)]

## HTTP request

To validate the endpoint and authentication configuration for a customAuthenticationExtension by its ID.
<!-- {
  "blockType": "ignored"
}
-->
``` http
POST /identity/customAuthenticationExtensions/{customAuthenticationExtensionId}/validateAuthenticationConfiguration
```

To validate the endpoint and authentication configuration that's specified in the request body for a customAuthenticationExtension. The custom authentication extension object may not exist yet and you can use this endpoint to validate the configuration before creating the custom authentication extension.
<!-- {
  "blockType": "ignored"
}
-->
``` http
POST /identity/customAuthenticationExtensions/validateAuthenticationConfiguration
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required. Learn more about [authentication and authorization](/graph/auth/auth-concepts).|

## Request body

In the request body, supply JSON representation of the parameters.

The following table shows the parameters that can be used with this action. Supply a endpointConfiguration and authenticationConfiguration if querying at the root level. Otherwise, for a specific custom extension, do not supply a request body for this method.

|Parameter|Type|Description|
|:---|:---|:---|
|endpointConfiguration|[customExtensionEndpointConfiguration](../resources/customextensionendpointconfiguration.md)|The HTTP endpoint for the custom authentication extension to be validated.|
|authenticationConfiguration|[customExtensionEndpointConfiguration](../resources/customextensionendpointconfiguration.md)|The authentication configuration for the custom authenticaion extension to validate.|

## Response

If successful, this action returns a `200 OK` response code and a [authenticationConfigurationValidation](../resources/authenticationconfigurationvalidation.md) in the response body.

## Examples

### Example 1: Supply and validate a potential custom authentication extension configuration

#### Request
The following example shows a request.
<!-- {
  "blockType": "request",
  "name": "customauthenticationextensionthis.validateauthenticationconfiguration"
}
-->
``` http
POST https://graph.microsoft.com/v1.0/customAuthenticationExtensions/validateAuthenticationConfiguration
Content-Type: application/json

{
    "endpointConfiguration": {
        "@odata.type": "#microsoft.graph.httpRequestEndpoint",
        "targetUrl": "https://australia.contoso.com/users"
    },
    "authenticationConfiguration": {
        "@odata.type": "#microsoft.graph.azureAdTokenAuthentication",
        "resourceId": "api://extensibilityapi.azurwebsites.net/f9c5dc6b-d72b-4226-8ccd-801f7a290428"
    }
}
```


#### Response
The following example shows the response.
>**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.authenticationConfigurationValidation"
}
-->
``` http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#microsoft.graph.authenticationConfigurationValidation",
    "errors": [
        {
            "code": "IncorrectResourceIdFormat",
            "message": "ResourceId should be in the format of 'api://{fully qualified domain name}/{appid}'"
        },
        {
            "code": "DomainNameDoesNotMatch",
            "message": "The fully qualified domain name in resourceId should match that of the targetUrl"
        },
        {
            "code": "ServicePrincipalNotFound",
            "message": "The appId of the resourceId should correspond to a real service principal in the tenant"
        }
    ],
    "warnings": [
        {
            "code": "PermissionNotGrantedToServicePrincipal",
            "message": "The permission CustomAuthenticationExtensions.Receive.Payload is not granted to the service principal of the resource app"
        },
    ]
}
```


### Example 2: Validate the configuration of a specific existing custom authentication extension

#### Request
The following example shows a request.

<!-- {
  "blockType": "request",
  "name": "customauthenticationextensionthis.validateauthenticationconfiguration_byId"
}
-->
``` http
POST https://graph.microsoft.com/v1.0/identity/customAuthenticationExtensions/9f39f3bb-457c-4a2a-8099-0e480e7ea142/validateAuthenticationConfiguration
```

#### Response
The following example shows the response.
>**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.authenticationConfigurationValidation"
}
-->
``` http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#microsoft.graph.authenticationConfigurationValidation",
    "errors": [
        {
            "code": "IncorrectResourceIdFormat",
            "message": "ResourceId should be in the format of 'api://{fully qualified domain name}/{appid}'"
        },
        {
            "code": "DomainNameDoesNotMatch",
            "message": "The fully qualified domain name in resourceId should match that of the targetUrl"
        },
        {
            "code": "ServicePrincipalNotFound",
            "message": "The appId of the resourceId should correspond to a real service principal in the tenant"
        }
    ],
    "warnings": [
        {
            "code": "PermissionNotGrantedToServicePrincipal",
            "message": "The permission CustomAuthenticationExtensions.Receive.Payload is not granted to the service principal of the resource app"
        },
    ]
}
```


