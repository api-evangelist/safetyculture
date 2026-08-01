---
name: Provision users and groups
description: Create a group, add users to it, and list a group's members in SafetyCulture.
api: https://api.safetyculture.io
operations:
  - thepubservice_creategroup
  - thepubservice_addnewusertogroup
  - thepubservice_listusersingroup
---

# Provision users and groups

Authenticate with `Authorization: Bearer {api_token}` against
`https://api.safetyculture.io`. The token owner's permissions bound what you can
create or change.

## Steps

1. **Create a group** (`thepubservice_creategroup`) to model a team, site, or role.
2. **Add a user to the group** (`thepubservice_addnewusertogroup`).
3. **List group members** (`thepubservice_listusersingroup`) to verify membership and
   reconcile against your source of truth.

## When to use SCIM instead

For continuous, identity-provider-driven provisioning, prefer SafetyCulture's SCIM 2.0
integration with Microsoft Entra ID or Okta (see `conformance/` and the user-provisioning
guides) rather than scripting group membership directly. Use these operations for
lightweight or supplementary automation.

## Conventions

- Bulk user upsert is heavily rate-limited (5 req / 60s); batch accordingly
  (`rate-limits/safetyculture-rate-limits.yml`).
