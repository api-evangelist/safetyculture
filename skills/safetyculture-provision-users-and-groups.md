---
name: safetyculture-provision-users-and-groups
description: Create a group, find users, add them to the group, and verify group membership.
api: https://api.mitti.com
operations:
- ThePubService_CreateGroup
- ThePubService_ListGroups
- UsersService_ListUsers
- ThePubService_AddNewUserToGroup
- ThePubService_ListUsersInGroup
- ThePubService_RemoveUser
---

# Provision users and groups

## Steps

1. **Check for the group** with `ThePubService_ListGroups`; create it with `ThePubService_CreateGroup` only if it is missing (this avoids duplicate groups).
2. **Find users** with `UsersService_ListUsers`.
3. **Add each user** to the group (`ThePubService_AddNewUserToGroup`).
4. **Verify membership** with `ThePubService_ListUsersInGroup`. Remove someone with `ThePubService_RemoveUser`.

## Conventions

- Base URL `https://api.mitti.com`; authenticate every call with `Authorization: Bearer {api_token}` (a user API token).
- Rate limits are per endpoint over a 60-second window; a throttled call returns `429 Too Many Requests`. Read the `x-ratelimit-*` headers and back off (see `rate-limits/`).
- No client-supplied idempotency key is documented (see `conventions/`), so do not blindly retry writes: after a timeout, re-read the resource with a list/get call before you resubmit.
- Prefer the current operations over the ones whose summary says `(legacy)`.
