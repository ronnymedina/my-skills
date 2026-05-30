# Database — <PROJECT_NAME>

<PARAGRAPH_DESCRIBING_THE_DOMAIN_AND_HIGH_LEVEL_DATA_MODEL>

## Models

### 1. <ModelName>
<ONE_LINE_DESCRIPTION>
*   **id**: <TYPE_AND_NOTES>.
*   **<field>**: <TYPE_AND_NOTES>.
*   **<field>**: <TYPE_AND_NOTES> (nullable: <REASON>).
*   **<foreignKey>**: Foreign key to `<RelatedModel>` (required|nullable).

### 2. <ModelName>
<ONE_LINE_DESCRIPTION>
*   **id**: <TYPE_AND_NOTES>.
*   **<field>**: <TYPE_AND_NOTES>.

<REPEAT_FOR_EACH_MODEL>

## Enums

| Enum | Values |
|------|--------|
| <EnumName> | <VAL_1>, <VAL_2>, <VAL_3> |

## Relationships Diagram

```mermaid
erDiagram
    <ModelA> ||--o{ <ModelB> : <verb>
    <ModelB> ||--o{ <ModelC> : <verb>
```

> See `examples/database-example.md` in the skill for a fully filled-out reference.
