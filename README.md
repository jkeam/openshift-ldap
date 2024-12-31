# OpenShift LDAP

OpenShift LDAP Example.  All values in the `yaml` are fake and for example only.

## Running

### Update Values

Update fake values in the following files:

1. `./openshift/secret.yaml` to reflect password for ldap service account user
2. `./openshift/config-map.yaml` to reflect entire cert chain for ldap server
3. `./openshift/oauth.yaml` to reflect ldap attributes, bindDN, and url

### Applying

Create resources used by LDAP identity provider (secret and configmap)
and then add the LDAP identity provider

```shell
oc apply -k ./openshift
```

or

```shell
oc apply -f ./openshift/secret.yaml
oc apply -f ./openshift/config-map.yaml
oc edit oauth/cluster
```

and add the ldap identity provider as reflected in `./openshift/oauth.yaml`.

## Links

1. [Docs](https://docs.openshift.com/container-platform/4.17/authentication/identity_providers/configuring-ldap-identity-provider.html#identity-provider-ldap-CR_configuring-ldap-identity-provider)
2. [JumpCloud](https://jumpcloud.com/support/use-cloud-ldap)
3. [LDAP Tester](https://github.com/TheJumpCloud/support/blob/master/scripts/jumpcloud_test_utility.sh)
4. [JumpCloud Certs](https://jumpcloud.com/support/connect-to-ldap-with-tls-ssl)
