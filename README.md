<!-- BEGIN_ANSIBLE_DOCS -->
# ansible-proserver-mailhog

Mailhog role for Proserver

## Supported Operating Systems

- FreeBSD [Proserver](https://infrastructure.punkt.de/de/produkte/proserver.html)

## Role Arguments



Configure MailHog with optional nginx reverse proxy, TLS via dehydrated, and oauth2_proxy for IAP.

#### Options for `mailhog`

|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| `use_dehydrated` | Use dehydrated role for TLS certificates and HTTPS. | bool | no | True |
| `bind_addr` | Address MailHog SMTP/API/UI bind to. | str | no | 127.0.0.1 |
| `smtp_port` | SMTP port. | int | no | 1025 |
| `api_port` | API port. Omit or set to null to leave unset. | int | no |  |
| `ui_port` | Web UI port. | int | no | 8025 |
| `domain` | Domain name for nginx server_name and TLS certificates. | str | no |  |
| `nginx` | Nginx listener configuration. | dict of 'nginx' options | no | {} |
| `oauth2_proxy` | Key into oauth2_proxy.config to enable IAP for the MailHog UI. When set, the dehydrated and oauth2_proxy role dependencies are used. | str | no |  |

#### Options for `mailhog.nginx`

|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| `bind_addr` | Addresses nginx listens on (e.g. ["::1"]). | list of 'str' | no | ['::1'] |

## Dependencies
- nginx
- dehydrated
  - **Condition**: `mailhog.use_dehydrated`
- oauth2_proxy
  - **Condition**: `(mailhog.oauth2_proxy is defined and mailhog.oauth2_proxy != None)`

## Installation
Add this role to the requirements.yml of your playbook as follows:
```yaml
roles:
  - name: ansible-proserver-mailhog
    src: https://github.com/punktDe/ansible-proserver-mailhog
```

Afterwards, install the role by running `ansible-galaxy install -r requirements.yml`

## Example Playbook

```yaml
- hosts: all
  roles:
    - name: mailhog
```

<!-- END_ANSIBLE_DOCS -->
