---
title: Environment Variable Vault
badge: free
---

## Configuration

Saving secrets in Environment Variables is a common way as they can be injected at build time.
There is no prior configuration needed.

## Examples

Defining a secret in a Environment Variable

```bash
export MY_SECRET_VALUE=opensesame
```

We can now reference this variable

```bash
{vaults://env/my_secret_value}
```

## Entity

-- There should be some table like structure that shows what config options this vault has.
-- Just like in plugins

{% navtabs codeblock %}
{% navtab cURL %}

```bash
$ curl -i -X POST http://<hostname>:8001/vaults-beta/my-env-vault
        --data name=env
        --data description="Secret store in environment variables"
```

{% endnavtab %}
{% navtab HTTPie %}

```bash

$ http put :8001/vaults-beta/my-env-vault name=env \
                                          description="Secret store in environment variables" \
                                          -f 
```

{% endnavtab %}
{% endnavtabs %}

Result:

```json
{
    "config": {
        "prefix": null
    },
    "created_at": 1644942689,
    "description": "Secret store in environment variables",
    "id": "2911e119-ee1f-42af-a114-67061c3831e5",
    "name": "env",
    "prefix": "my-env-vault",
    "tags": null,
    "updated_at": 1644942689
}
```

With that entity in place you can reference secrets like this. 

```bash

{vaults://my-env-vault/my_secret_value}

```
