---
title: "Remove multiTenantOrganizationMember"
description: "Remove a tenant from a multitenant organization."
author: "rolyon"
ms.localizationpriority: medium
ms.subservice: "entra-sign-in"
doc_type: apiPageType
---

# Remove multiTenantOrganizationMember
Namespace: microsoft.graph

Remove a tenant from a multitenant organization. A tenant can be removed in the following scenarios:

* An active member tenant can remove itself.
* An active owner tenant can remove any other tenant.
* An active owner tenant can remove itself as long as there is another active owner tenant remaining.
* An active owner tenant can remove itself as long as there is no other active tenant remaining, thereby deleting the entire multitenant organization.

[!INCLUDE [national-cloud-support](../../includes/global-only.md)]

## Permissions
Choose the permission or permissions marked as least privileged for this API. Use a higher privileged permission or permissions [only if your app requires it](/graph/permissions-overview#best-practices-for-using-microsoft-graph-permissions). For details about delegated and application permissions, see [Permission types](/graph/permissions-overview#permission-types). To learn more about these permissions, see the [permissions reference](/graph/permissions-reference).

<!-- { "blockType": "permissions", "name": "multitenantorganization_delete_tenants" } -->
[!INCLUDE [permissions-table](../includes/permissions/multitenantorganization-delete-tenants-permissions.md)]

[!INCLUDE [rbac-multitenantorganization-apis-write](../includes/rbac-for-apis/rbac-multitenantorganization-apis-write.md)]

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->
``` http
DELETE /tenantRelationships/multiTenantOrganization/tenants/{tenantId}
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|

## Request body
Don't supply a request body for this method.

## Response

If successful, this method returns a `204 No Content` response code.

## Examples

The following example removes a tenant from a multitenant organization.

### Request

<!-- {
  "blockType": "request",
  "name": "delete_multitenantorganizationmember"
}
-->
``` http
DELETE https://graph.microsoft.com/v1.0/tenantRelationships/multiTenantOrganization/tenants/5036a0a0-a7a4-4933-9086-5dd54535dd6e
```

### Response

<!-- {
  "blockType": "response",
  "truncated": true
}
-->
``` http
HTTP/1.1 204 No Content
```

