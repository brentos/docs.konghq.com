---
title: AWS Secrets-Manager
badge: enterprise
---

## Configuration

[AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) can be configured in multiple ways. The current version of Kong's implementation only supports
configuring via environment variables.

```bash
export AWS_ACCESS_KEY_ID=<access_key_id>
export AWS_SECRETS_ACCESS_KEY=<secrets_access_key>
export AWS_REGION=<aws-region>

```

## Examples

You've configured a AWS Secrets Manager Secret with a "Secret name" of "my-secret-name".

Lets's say you have multiple key=value pairs.

```json
{
  "foo": "bar",
  "snip": "snap",
}
```

Accessing these secrets can be done like this:

```bash
{vaults://aws/my-secret-name/foo}
{vaults://aws/my-secret-name/snap}
```

## Entity

-- There should be some table like structure that shows what config options this vault has.
-- Just like in plugins

{% navtabs codeblock %}
{% navtab cURL %}

```bash
$ curl -i -X POST http://<hostname>:8001/vaults-beta/my-aws-sm-vault  
        --data name=aws
        --data description="Secret store in AWS Secrets Manager"
        --data config.region="us-east-1"

```

{% endnavtab %}
{% navtab HTTPie %}

```bash

$ http put :8001/vaults-beta/my-aws-sm-vault name=aws \
                                             description="Secret store in AWS Secrets Manager" \
                                             config.region="us-east-1" \
                                             -f 
```

{% endnavtab %}
{% endnavtabs %}

Result:

```json
{
    "config": {
        "region": "us-east-1"
    },
    "created_at": 1644942689,
    "description": "Secret store in AWS Secrets Manager",
    "id": "2911e119-ee1f-42af-a114-67061c3831e5",
    "name": "aws",
    "prefix": "my-aws-sm-vault",
    "tags": null,
    "updated_at": 1644942689
}
```

With that entity in place you can reference secrets like this. This allows you do drop the `AWS_REGION`
environment variable.

```bash

{vaults://my-aws-sm-vault/my-secret-name/foo}
{vaults://my-aws-sm-vault/my-secret-name/snap}

```

## Advanced Examples

The creating multiple entities allows you to have secrets in different regions

```bash

http put :8001/vaults-beta/aws-eu-central-vault name=aws config.region="eu-central-1" -f 
http put :8001/vaults-beta/aws-us-west-vault name=aws config.region="us-west-1" -f 

```

Which then enables you to source secrets from different regions.

```bash
{vaults://aws-eu-central-vault/my-secret-name/foo}
{vaults://aws-us-west-vault/my-secret-name/snap}
```
