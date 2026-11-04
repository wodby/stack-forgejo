# Forgejo application stack for Kubernetes on Wodby

Deploy Forgejo, a self-hosted Git service, on Kubernetes with Wodby.

This repository defines the Wodby stack manifest and its default service
composition.

<!-- wodby:generated:start -->

## Stack contract

- [Forgejo stack on Wodby](https://wodby.com/stacks/forgejo)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Service definitions

- [Forgejo service](https://github.com/wodby/service-forgejo)
- [PostgreSQL service](https://github.com/wodby/service-postgres)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)

## What's included

| Component / service | Default configuration |
| --- | --- |
| Forgejo<br>`forgejo` | required; enabled by default; links: `postgres` → `postgres`, `sendmail` → `opensmtpd` |
| PostgreSQL<br>`postgres` | required; enabled by default; volumes: `data` 20 GB |
| OpenSMTPD<br>`opensmtpd` | optional; enabled by default |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Validate the stack manifest

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

<!-- wodby:generated:end -->

## Operational scope

This stack runs one Forgejo replica with its repositories, Git LFS objects,
packages and attachments on one persistent volume, and its database in the
bundled PostgreSQL service.

Forgejo Actions is available, but no runner is included. Register an external
Forgejo Runner to run workflows.

## Deploy this stack

Set the **Admin password** setting of the Forgejo service when creating the
application. The first deployment creates that administrator account; the web
installer is never shown and sign-up is closed until you open it.

Git over HTTPS works through the application's domain. For Git over SSH,
publish the service's `ssh` port on the application's **Ports** page. Forgejo
is redeployed and shows clone addresses with the assigned public port.

Back up the PostgreSQL database and the Forgejo volume as one recovery set.

## Maintain a custom version

1. Fork this repository.
2. Edit `stack.yml`.
3. Import the repository as a [Git-backed stack](https://wodby.com/docs/2.0/stacks/create/#create-a-git-backed-stack).

When replacing or renaming a stack service, update every related link target.
Stack-local names and referenced service names are distinct identifiers.
