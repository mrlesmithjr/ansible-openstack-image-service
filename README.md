<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ansible-openstack-image-service](#ansible-openstack-image-service)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
    - [Ansible Roles](#ansible-roles)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-openstack-image-service

An [Ansible](https://www.ansible.com) role to install/configure [OpenStack Image Service](https://docs.openstack.org/ocata/install-guide-ubuntu/common/get-started-image-service.html)

## Requirements

None

## Role Variables

```yaml
---
# defaults file for ansible-openstack-image-service

# glance_store
openstack_image_service_glance_store:
  default_store: 'file'
  filesystem_store_datadir: '/var/lib/glance/images/'
  stores:
    - 'file'
    - 'http'

# Defines Glance DB info
openstack_image_service_glance_db_info:
  db: 'glance'
  user: 'glance'
  pass: 'glance'
  host: 'localhost'

openstack_image_service_keystone_service_endpoint_region: 'RegionOne'

# Defines the default Keystone endpoint url
# Do not append the port or api version
openstack_image_service_keystone_service_endpoint_url: 'http://{{ inventory_hostname }}'

# Defines Glance user info
openstack_image_service_glance_user_info:
  name: 'glance'
  # Generate with openssl rand -hex 10
  password: []
  description: 'Glance user'
  domain_id: 'default'
  state: 'present'
  enabled: true
  role: 'admin'
  project: 'service'

# keystone_authtoken
openstack_image_service_keystone_authtoken:
  auth_type: 'password'
  auth_uri: 'http://{{ openstack_image_service_keystone_service_endpoint_url }}:5000'
  auth_url: 'http://{{ openstack_image_service_keystone_service_endpoint_url }}:35357'
  memcached_servers:
    - 'localhost'
  password: "{{ openstack_image_service_glance_user_info['password'] }}"
  project_domain_name: "{{ openstack_image_service_glance_user_info['domain_id'] }}"
  project_name: "{{ openstack_image_service_glance_user_info['project'] }}"
  user_domain_name: "{{ openstack_image_service_glance_user_info['domain_id'] }}"
  username: "{{ openstack_image_service_glance_user_info['name'] }}"
```

## Dependencies

### Ansible Roles

The following [Ansible](https://www.ansible.com) roles are required as part of
this role.

-   [ansible-chrony](https://github.com/mrlesmithjr/ansible-chrony)
-   [ansible-config-interfaces](https://github.com/mrlesmithjr/ansible-config-interfaces)
-   [ansible-etc-hosts](https://github.com/mrlesmithjr/ansible-etc-hosts)
-   [ansible-memcached](https://github.com/mrlesmithjr/ansible-memcached)
-   [ansible-mysql](https://github.com/mrlesmithjr/ansible-mysql)
-   [ansible-openstack-base](https://github.com/mrlesmithjr/ansible-openstack-base)
-   [ansible-openstack-identity-service](https://github.com/mrlesmithjr/ansible-openstack-identity-service)
-   [ansible-openstack-openrc](https://github.com/mrlesmithjr/ansible-openstack-openrc)
-   [ansible-rabbitmq](https://github.com/mrlesmithjr/ansible-rabbitmq)

The above roles can be installed using `ansible-galaxy` along with [requirements.yml](./requirements.yml):

```bash
ansible-galaxy install -r requirements.yml
```

## Example Playbook

[Example Playbook](./playbook.yml)

## License

MIT

## Author Information

Larry Smith Jr.

-   [@mrlesmithjr](https://www.twitter.com/mrlesmithjr)
-   [EverythingShouldBeVirtual](http://www.everythingshouldbevirtual.com)
-   mrlesmithjr [at] gmail.com
