#acid 
Isolation determines how transaction integrity is visible to other users and systems.

A lower isolation level increases the ability of many users to access the same data but increases the number of concurrency effects users might encounter. Higher isolation level reduces the types of concurrent effects but increase the chances that one transaction will block another. 

Isolation is typically defined at database level as a property that defines how or when the changes made by one operation become visible to others. On older systems, it may be implemented systemically, for example through the use of temporary tables.

#TODO 
## Read phenomena
[[dirty reads]]
[[non-repeatable reads]]
[[phantom reads]]

## Isolation Levels
[[serializable]]
[[repeatable read]]
[[read commited]]
[[read uncommitted]]



| Read phenomenon/Isolation level | Dirty read | Non-repeatable read | Phantom read |
| -------- | -------- | -------- | -------- |
| Serializable | No | No | No |
| Repeatable read | No | No | Yes |
| Read committed | No | Yes | Yes|
| Read uncommitted | Yes | Yes | Yes |