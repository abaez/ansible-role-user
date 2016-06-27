ansible-role-user
=========
[![license][2i]][2p]
[![twitter][3i]][3p]

A small user creation for [docker] based provision.

Description
-----------

Provisions the client to have a new **super** user and **main** user. The **super** user is a user who will be used to administer the provisioned client. As such, it has direct access to all root capabilities but has no password associated with it. The only way to access the user would be through a **RSA** key connected for access to the user through the install. The **main** user is provisioned similar to that of **super** except that it only has access to running docker containers, journalctl, and systemctl programs. It does not have write access to anything on the system and is only used to manage the currently working setup of the containers running on the client.

Role Variables
--------------

The role has two variable maps that need to be changed, both dealing with user creation:

``` yaml
users.super:
  name: # some user name to be the super user.
  home: # the home for this super user.
  pub: # the ssh  pubkey you want to use for access to user.

users.main:
  name: # some user name for the regular user.
  home: # some home for this regular user.
  pub: # the ssh  pubkey you want to use for access to user.
```

All the home, pub, and user name need to be changed to accomadate the use of the role.

Requirements
------------

Does not need to have **docker** installed, but can be helpful in the process when adding the groups usage. It will create the **docker** group if the group does not exist on the client.

Usage
-----

You **need** the `.pub` key value, listed in *Role Variables* above, to gain access to the user.

The container also needs the `defaults/main.yml` variables of **super** and **main** changed as detailed on the description and *role variables*. Other than that, nothing else needs to be appended to be changed to run the role.

``` yaml
- hosts: servers
    roles:
        - users
```

Author Information
------------------

[Alejandro Baez][1]

[docker]: https://www.docker.com/

[1]: https://keybase.io/baez
[2i]: https://img.shields.io/badge/license-BSD_2-green.svg
[2p]: ./LICENSE
[3i]: https://img.shields.io/badge/twitter-a_baez-blue.svg
[3p]: https://twitter.com/a_baez
