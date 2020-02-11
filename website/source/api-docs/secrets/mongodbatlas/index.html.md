---
layout: "api"
page_title: "MongoDB Atlas - Secrets Engines - HTTP API"
sidebar_title: "MongoDB Atlas"
sidebar_current: "docs-secrets-engines-mongodbatlas"
description: |-
  The MongoDB Atlas Secrets Engine for Vault generates MongoDB Atlas Programmatic API Keys dynamically.
---

# MongoDB Atlas Secrets Engine

The MongoDB Atlas Secrets Engine generates Programmatic API keys. This allows one to manage the
lifecycle of these MongoDB Atlas secrets programmatically. The created MongoDB Atlas secrets are
time-based and are automatically revoked when the Vault lease expires, unless renewed.

This MongoDB Atlas Secrets Engine supports the creation of Programmatic API keys. Vault will create
a Programmatic API key for each lease that provide appropriate access to the defined MongoDB Atlas
project or organization with appropriate role(s) . The MongoDB Atlas Programmatic API Key Public and
Private Key is returned to the caller. To learn more about Programmatic API Keys visit the
[Programmatic API Keys Doc](https://docs.atlas.mongodb.com/reference/api/apiKeys/).

## Configure Connection

In addition to the parameters defined by the Secrets Engines Backend, this plugin has a number of parameters to further configure a connection.

| Method   | Path                         |
| :--------------------------- | :--------------------- |
| `POST`   | `/mongodbatlas/config`     |


## Parameters

- `public_key` `(string: <required>)` – The Public Programmatic API Key used to authenticate with the MongoDB Atlas API.
- `private_key` `(string: <required>)` - The Private Programmatic API Key used to connect with MongoDB Atlas API.
- `project_id` `(string: <required>)` - .
- `organization` `(string: <required>)` - .
- `roles` `(string: <required>)` - .
- `cidr_blocks` `(string: <required>)` - .
- `ip_addresses` `(string: <required>)` - .

### Sample Payload

```json
{
  "plugin_name": "mongodbatlas-secrets-engines-plugin",
  // "allowed_roles": "readonly",
  "public_key": "aPublicKey",
  "private_key": "aPrivateKey",
  // "project_id": "aProjectID"
}
```

### Sample Request

```bash
$ curl \
    --header "X-Vault-Token: ..." \
    --request POST \
    --data @payload.json \
    http://127.0.0.1:8200/v1/mongodbatlas/config
```
