# demo-identity-access-management

## lldap

### LDAP search

Install `ldapsearch`

```bash
sudo apt install ldap-utils
```

#### Returning all entries

```bash
ldapsearch -W -D "uid=admin,ou=people,dc=wicaksana,dc=id" \
  -H ldap://127.0.0.1:3890 \
  -b "dc=wicaksana,dc=id" \
  -s sub -x "(objectclass=*)"
```

Output example:
```bash
Enter LDAP Password:
# extended LDIF
#
# LDAPv3
# base <dc=wicaksana,dc=id> with scope subtree
# filter: (objectclass=*)
# requesting: ALL
#

# admin, people, wicaksana.id
dn: uid=admin,ou=people,dc=wicaksana,dc=id
cn: Administrator
createtimestamp: 20260306031318Z
entryuuid: 2eb62f6a-046e-3f9e-af84-3d119b6ac3a1
objectclass: inetOrgPerson
objectclass: posixAccount
objectclass: mailAccount
objectclass: person
uid: admin

# arif, people, wicaksana.id
dn: uid=arif,ou=people,dc=wicaksana,dc=id
cn: Arif
createtimestamp: 20260306032240Z
entryuuid: b6128ef3-ff5a-35ea-a3e4-b218cf9ffd45
first_name: Arif
givenname: Arif
last_name: Wicaksana
mail: arif@wicaksana.id
objectclass: inetOrgPerson
objectclass: posixAccount
objectclass: mailAccount
objectclass: person
sn: Wicaksana
uid: arif

# dunk, people, wicaksana.id
dn: uid=dunk,ou=people,dc=wicaksana,dc=id
cn: Dunk
createtimestamp: 20260306032734Z
entryuuid: 04419a97-3f19-3bb4-9939-06c56b342d0d
first_name: Duncan
givenname: Duncan
last_name: the Tall
mail: dunk@wicaksana.id
objectclass: inetOrgPerson
objectclass: posixAccount
objectclass: mailAccount
objectclass: person
sn: the Tall
uid: dunk

# administrator, groups, wicaksana.id
dn: cn=administrator,ou=groups,dc=wicaksana,dc=id
cn: administrator
entryuuid: 1426e368-ee99-370b-86b5-4a469b8bdbad
member: uid=arif,ou=people,dc=wicaksana,dc=id
member: uid=dunk,ou=people,dc=wicaksana,dc=id
objectclass: groupOfUniqueNames
objectclass: groupOfNames
uid: administrator
uniquemember: uid=arif,ou=people,dc=wicaksana,dc=id
uniquemember: uid=dunk,ou=people,dc=wicaksana,dc=id
...
```

#### Returning specific entries

Search for Dunk:

```bash
ldapsearch -W -D "uid=admin,ou=people,dc=wicaksana,dc=id" \
  -H ldap://127.0.0.1:3890 \
  -b "dc=wicaksana,dc=id" \
  -s sub -x "cn=Dunk"
```

Output example:
```bash
# dunk, people, wicaksana.id
dn: uid=dunk,ou=people,dc=wicaksana,dc=id
cn: Dunk
createtimestamp: 20260306032734Z
entryuuid: 04419a97-3f19-3bb4-9939-06c56b342d0d
first_name: Duncan
givenname: Duncan
last_name: the Tall
mail: dunk@wicaksana.id
objectclass: inetOrgPerson
objectclass: posixAccount
objectclass: mailAccount
objectclass: person
sn: the Tall
uid: dunk

# search result
search: 2
result: 0 Success
control: 1.2.840.113556.1.4.319 false MAUCAQEEAA==
pagedresults: estimate=1 cookie=

# numResponses: 2
# numEntries: 1
```

## Keycloak

### LDAP integration

Import [realm-import.json](./keycloak_data/import/realm-import.json) to Keycloak.

