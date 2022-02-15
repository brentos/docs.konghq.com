---
title: Kong Secrets Management
---

## Reference Format

TODO: This section needs work. In the current state this is too complicated.


We use the URL syntax to describe references to a secret store.

        {vault://<vault-backend|entity>/<secret-id>[/<secret-key][?query][#fragment]}


### Protocol/Scheme

```
{vault://<vault-backend|entity>/<secret-id>[/<secret-key]} 

 ^^^^^
```

The `vault` in the URL is used as an identifier for Kong. This we're using a reference to a vault. 


### Path

```
{vault://<vault-prefix>/<secret-id>[/<secret-key]}

         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```
        
The `path` of the URL defines the following:


### Vault Prefix

The prefix for a vault can be either the name of the used backend or the name of vault entity that you created.

Examples:

``` {vault://env/<secret-id>[/<secret-key]} ```

or

``` {vault://my-env-vault/<secret-id>[/<secret-key]} ```


### Secret ID


.....

### Secret Key


.....


### Query

.....

### Fragment

.....
