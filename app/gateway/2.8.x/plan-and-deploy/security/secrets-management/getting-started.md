---
title: Kong Secrets Management
---

{:.warning .no-icon}
> **Beta warning:** 
> In this version of the feature, you have to explicitly enable this feature. 
> <br>
> <br>
> KONG_VAULTS=vault-name
> <br>
> ⚠️This feature is currently in beta state and isn't fully supported. APIs are subject to change.

## Overview

todo: do we want a preface on _why_ secrets management is useful and what it actually is?

Kong offers a mechanism to reference secrets that are stored "somewhere else"(remotely isn't accurate here as "env" and "file" stores them locally).

## Getting Started

In the following example we use the most basic form of secrets management. We are storing our secrets in an "Environment Variable".

A list of supported vault "backend" implementations can be found [here](/gateway/2.8.x/plan-and-deploy/security/secrets-management/backends-overview)


In this example we'll replace our plaintext password to our Postgres database with a reference. To do so, please define your environment variable and assign a secret value to it.


### Defining a reference

```bash
export MY_SECRET_POSTGRES_PASSWORD="opensesame"
```

For Kong to be able to find this secret we have to set up a `reference` to this environment variable. We use a Uniform Resource Locator (URL) format for this. [See the Reference Format Section](/gateway/2.8.x/plan-and-deploy/security/secrets-management/reference-format)

In this case the reference would look like this:

```bash
{vault://env/my_secret_postgres_password}
```

Note that "vault" is just the scheme(protocol) that we use to indicate that this a secret.

`env` is the name of the backend [(EnvironmentVariable)](/gateway/2.8.x/plan-and-deploy/security/secrets-management/backends/env) since we're storing the secret in a ENV variable.

`my_secret_postgres_password` corresponds to the environment variable that we just defined.

### Using the reference

Kong offers multiple ways to specify configuration options. Choose either of these options.

* Environment variable

```bash
KONG_PG_PASSWORD={vault://env/my_secret_postgres_password}
```

* Configuration file

the kong.conf has a key called "pg_password". Replace the original value with

```bash
pg_password={vault://env/my_secret_postgres_password}
```

Upon startup, Kong will try to detect and transparently resolve references.


{:.note}
>  For quick debug/testing you can use the new [CLI for vaults](/gateway/2.8.x/plan-and-deploy/security/secrets-management/advanced-usage/#vaults-cli)


Some vault backends accept a multitude of configurations. Visit the [Advanced Usage Section](/gateway/2.8.x/plan-and-deploy/security/secrets-management/advanced-usage) for more information.


