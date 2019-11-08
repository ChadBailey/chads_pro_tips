# Config

Note that by default edits are scoped locally. If you want to edit your config 
globally, you would include the `--global` switch. This means it applies for 
all accounts on the current machine. Since I sometimes have to toggle between 
accounts I typically always include the global switch. For this reason, the 
below commands will include the optional `--global` switch.

## Show Current Config

`git config -l`

## Manually edit config

`git config --global --edit`


## Remove setting

`git config --unset [--global] setting.identifier`

i.e. `git config --unset --global http.proxy`

## Proxy/Network

### Proxy without NTLM auth

`git config --global http.proxy http://proxy.mycompany:80`

### Proxy with NTLM auth

`git config --global http.proxy http://mydomain\\myusername:mypassword@myproxyserver:8080/`

