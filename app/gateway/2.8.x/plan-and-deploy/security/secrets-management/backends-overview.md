---
title: Kong Secrets Management
---

{:.warning}
> **Beta warning:** 
> <br>
> Secrets Rotation is currently not supported in this version.

Table view of the currently supported Vault implementations.


|                  | [AWS SecretsManager](/gateway/2.8.x/plan-and-deploy/security/secrets-management/backends/aws-sm) | [Hashicorp Vault](/gateway/2.8.x/plan-and-deploy/security/secrets-management/backends/hashicorp-vault) | [Environment Variable](/gateway/2.8.x/plan-and-deploy/security/secrets-management/backends/env) |
|------------------|--------------------|-----------------|----------------------|
| Rotation support | -                  | -               | -                    |
| Get              | x                  | x               | x                    |
| Set              | -                  | -               | -                    |
| Tier             | Enterprise         | Enterprise      | Free                 |
