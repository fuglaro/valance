# Valance API

## Ideas (WIP)

### Examples

#### User table
| id | name | color |
| -- | ---- | ----- |
| 1  | John | red   |
| 2  | Ken  | blue  |

#### Basic row count query
```json
{
    "table": "mytable",
}
```
> ```json
> 2
> ```

#### Basic column query
```json
{
    "table": "mytable",
    "columns": ["color", "name"]
}
```
> ```json
> [
>     ["red", "John"],
>     ["blue", "Ken"]
> ]
> ```
