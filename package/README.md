# system-installer-brew

The [aux4 system installer](/r/public/packages/aux4/pkger/commands/aux4/pkger/system) is used to manage packages by another package system. It is used to install and uninstall system packages.

```json
{
  "scope": "<scope>",
  "name": "<name>",
  "version": "<version>",
  ...
  "system": [
    ["brew:awscli"],
    ["brew:jq"]
  ],
  "profiles": [
    ...
  ]
}
```

In this case when the *aux4 package is installed*, it will install the `awscli` and `jq` packages using the `brew` package manager.

```sh
> brew install awscli
```
```sh
> brew install jq
```

In the same way, when the *aux4 package is uninstalled*, it will uninstall `awscli` and `jq` packages using the `brew` package manager (only if they are not used by another aux4 package).

```sh
> brew uninstall awscli
```
```sh
> brew uninstall jq
```

Check out the [aux4 pkger system brew](commands/aux4/pkger/system/brew) command for more information.

