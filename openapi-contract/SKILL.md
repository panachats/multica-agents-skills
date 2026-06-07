---
name: openapi-contract
description: Conventions for writing OpenAPI API contracts in this workspace. Use this skill when defining or updating REST API specs before implementation. Consult it so every contract uses the same structure, naming, error responses, and pagination patterns — backend and frontend can work from one consistent contract.
---

# OpenAPI contract conventions

Write API contracts as OpenAPI 3.x YAML in `/docs/api/<issue-key>.yaml`. The contract is the single source of truth — devs implement against it; do not change it during coding without architect approval.

## File structure

Every contract must include:

```yaml
openapi: 3.0.3
info:
  title: <Service or feature name>
  version: 1.0.0
paths:
  # endpoints here
components:
  schemas:
    # shared types here
  responses:
    # shared error responses here
```

## Naming

- Paths: plural nouns, kebab-case — `/api/orders`, `/api/order-items`
- Query params: camelCase — `fromDate`, `channelCode`
- JSON properties: camelCase — `orderNo`, `totalAmount`
- Use canonical segment/channel codes from `domain-context` in enums and descriptions

## Every endpoint must define

- Summary and description (one line each)
- All parameters with `required`, `schema`, and `description`
- All response codes the client will handle: at minimum `200`, `400`, `401`/`403` if auth applies, `404` where relevant, `500`
- Response body schema for success and error cases

## Shared error shape

Reuse this pattern in `components/schemas`:

```yaml
Error:
  type: object
  required: [code, message]
  properties:
    code:
      type: string
      example: VALIDATION_ERROR
    message:
      type: string
      example: End date must be on or after start date.
```

Reference it from `components/responses` and use `$ref` in each path.

## Pagination (list endpoints)

When a list can grow large, use cursor or offset pagination — document which in the contract:

```yaml
parameters:
  - name: page
    in: query
    schema: { type: integer, minimum: 1, default: 1 }
  - name: pageSize
    in: query
    schema: { type: integer, minimum: 1, maximum: 100, default: 20 }
```

Response includes `items` array plus `total` or `nextCursor`.

## Contract changes

If implementation reveals the contract must change:

1. Do not ship code that diverges from the yaml on disk.
2. Comment `@solution-architect` with the proposed change and rationale.
3. Architect updates `/docs/api/<issue-key>.yaml` and notifies `@backend-dev` and `@frontend-dev`.
4. Devs resume only after the updated contract is committed.

## Handoff

After the contract is final, tag `@backend-dev` (contract + DDL) and `@frontend-dev` (contract only). Link the yaml path in the issue description.
