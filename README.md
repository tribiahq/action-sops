# GitHub Action for Mozilla Sops
This action for [sops](https://github.com/mozilla/sops) enables 
arbitrary actions with the `sops` command.

The underlying container used is maintained at 
[sops-dockeere](https://github.com/tribiahq/sops-docker). 

### Parameters
| Argument   | Description |
|------------|-------------|
| gpgPrivateKey  | GPG Private key, e.g. `gpg --export-secret-keys -a <key> | pbcopy` |

### Usage
An example configuration deploying tenant configuration from the project where this 
workflow is running. The tenant input file is expected to be at `./tenant.yml`.

```yaml
name: Decrypt secret key
on: [push]

jobs:
  decrypt:
    name: Decrypt secret
    uses: tribiahq/action-sops@master
    args: -d /secret.yaml > 
    with:
      gpgPrivateKey: ${{ secrets.MY_GPG_PRIVATE_KEY }}
```

### Environment Variables
Any environment variable respected by the underlying `sops` command can be passed in 
via `env`.
