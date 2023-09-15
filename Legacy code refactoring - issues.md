#refactoring 
#valueObject 

URL: https://github.com/legacyfighter/cabs-java

relates to: [[Refactoring]], [[Value Object]], [[Legacy]]
## Issue of variety of presentation - [[Refactoring]] to [[Value Object]]

Issue when some value needs to be presented in multiple ways to API caller, while internal representation might not change. Example would be internally we store distance in kilometers only but caller would like to see it in [miles, yards, whatever]

Helpful analytical questions:
- How many different presentations are used in systems
- In how many places are they used
- Can presentation change into different one using calculation
	- Are those calculations changing dynamically? Or is it always same conversion. Eg Distance conversion is always the same, Money conversion is changing based on exchange rates
- Are there plans to add more ways of presentation value

Note: 
- We only need to change **presentation**. We don't need to store data in different units. 

## Issue of hidden Domain concept - [[Refactoring]] to [[Value Object]]

Can be noticed when there are multiple places in code that are tightly coupled (either by code, or by business concept) and always required changing together. Can be also noticed when multiple fields or object/class/concept are changing together often. 

Helpful analytical questions:
- When adding new function or modifying existing one do many places need to be changed at once? Maybe with similar logic. 
- Can you find logical connection between data that creates cohesive unit. Why there is such connection? Maybe it can be found on buisness level for example in a way that buisness is talking about feature.
- Can you find specific wording for given business in source code? What is it form?

Solve with: Make the implicit explicit  - Tells you that if you have to reason about some domain concept from code you can make it explicit by expressing it in code. 

## Problem of lack of cohesion of data between fields - [[Refactoring]] to [[Value Object]]

Can  be noticed when multiple fields of a class always have to change together but code does not express that due to no encapsulation being applied. You can often notice that class itself is just a data carrier and does not contain business logic. 

Helpful questions
- Do different parts of code always modify same fields together?
- Does missing modification of one of the coupled fields leads to inconsistent data?
- Can you put object into any state using setters/public fields?
- Can you detect cycles of "get state" -> "check something" -> "modify something"? 
- Is [[feature envy]] present

Bringing back encapsulation
- create new access methods describing business logic
- remove public accessors/setters/getters
- move rules/logic into business logic into objects
- should not have dependencies to other services

When refactoring state intention
- how do business call this operation
- does name tell you about implementation details
- does name suggest only one specific solution (does it say how not what its doing?) but be pragmatic

Solve with: increasing encapsulation. Create functions that contain buisness logic and remove public fields/setters/getters. 