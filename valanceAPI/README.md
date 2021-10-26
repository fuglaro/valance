# Valance API

## Ideas (WIP)

### Examples

> #### User table
> | id | name | color |
> | -- | ---- | ----- |
> | 1  | John | red   |
> | 2  | Ken  | blue  |

> #### Basic query
> ```json
> {
>     "table": "mytable",
>     "columns": ["color", "name"]
> }
> ```
>> ```json
>> [
>>     ["red", "John"],
>>     ["blue", "Ken"]
>> ]
>> ```
