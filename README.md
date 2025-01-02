# OpenShift LDAP

OpenShift LDAP Example.  All values in the `yaml` are fake and for example only.

## Running

### Update Values

Update fake values in the following files:

1. `./users/secret.yaml` to reflect password for ldap service account user
2. `./users/config-map.yaml` to reflect entire cert chain for ldap server
3. `./users/oauth.yaml` to reflect ldap attributes, bindDN, and url
4. `./groups/group-config.yaml` to reflect ldap attributes, bindDN, password, and url

### Applying

#### Auth Provider

Create resources used by LDAP identity provider (secret and configmap)
and then add the LDAP identity provider

```shell
oc apply -k ./users
```

or

```shell
oc apply -f ./users/secret.yaml
oc apply -f ./users/config-map.yaml
oc edit oauth/cluster
```

and add the ldap identity provider as reflected in `./users/oauth.yaml`.

#### Groups

oc adm groups sync --sync-config=./groups/group-config.yaml --confirm

## Removing

If you want to undo/delete all that you've done, make sure to:

1. Delete any users/groups/[identities](https://github.com/openshift/origin/issues/14506) created by this process
2. Remove all associated secrets/configmaps
3. Remove identity provider from oauth/cluster

## Links

1. [OpenShift Docs for LDAP Identity Provider](https://docs.openshift.com/container-platform/4.17/authentication/identity_providers/configuring-ldap-identity-provider.html#identity-provider-ldap-CR_configuring-ldap-identity-provider)
2. [OpenShift Docs for LDAP Group Sync](https://docs.openshift.com/container-platform/4.17/authentication/ldap-syncing.html)
3. [JumpCloud Docs](https://jumpcloud.com/support/use-cloud-ldap)
4. [JumpCloud Certs Doc](https://jumpcloud.com/support/connect-to-ldap-with-tls-ssl)
5. [JumpCloud LDAP Tester](https://github.com/TheJumpCloud/support/blob/master/scripts/jumpcloud_test_utility.sh)
