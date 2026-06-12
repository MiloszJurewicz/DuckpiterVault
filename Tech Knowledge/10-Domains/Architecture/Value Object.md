#refactoring
#TODO

Object which is representing some value.
### Characteristics
- describes attributes of some domain concepts
- is immutable
- binds multiple attributes into logical unit
- is easy to replace with use of stable interface
- does not have identity by itself. Its identified by values of attributes
- comparing with different object is based on comparison of object attributes

### Benefits of using value object
- Its representing specific business element in code 
- Encapsulates logic thats related to attributes. For example validation
- Improves readability of source code
- makes it easier to introduce new changes to code because of stable interface
