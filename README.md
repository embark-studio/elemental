# Elemental Design and Development

## Developers
### Quick Reference

|                 | Element   | Group | Templates  | Wrappers| Yields |
| :-------------  |:---------:| :---: | :---------:| :-----: | -----: |
| Only 1 Element  |     X     |       |            |    X    |        | 
| 2+  Elements    |           |   X   |      X     |         |    X   |
| Functional      |     X     |   X   |            |         |        |
| Class Based     |           |       |      X     |    X    |    X   |
| Logic           |           |       |      X     |    X    |    X   | 
| Routes          |           |       |            |    X    |    X   |
| Can Be Top Most |           |       |            |         |    X   |




## Designers
### Quick Reference

|                   | Element   | Group | Templates  | Wrappers| Yields |
| :---------------  |:---------:| :---: | :---------:| :-----: | -----: |
| Only 1 Element    |     X     |       |            |    X    |        | 
| 2+  Elements      |           |   X   |      X     |         |    X   |
| Simple UI         |     X     |   X   |            |         |        |
| Complex UI        |           |       |      X     |    X    |    X   |
| Complex UX        |           |       |      X     |    X    |    X   | 
| URL Based Coices  |           |       |            |    X    |    X   |
| Can Be Outer Most |           |       |            |         |    X   |


# Nesting Components:
All types of components can have another component of their own level or less

#### Example:
* A Group can have a Group
* A Group can have an Element
* A Group **Can't** have a wrapper

# Folder Structure
* component type (Group)
  * ComponentName
    * index.js
    * style.scss
### Example:
* groups
  * InputField
    * index.js
    * style.js
#### Note - Export all components in each component type with an index.js
## Definition of Term

### Element
A single HTML Element
##### Examples: 
* Password Field
* Text Field
* Button
* Image
* Label
* Form (Container)

##### Examples of What is Not an Element:
* A form that contains inputs or buttons
* An input group i.e. an input with a label

##### Caveats
A loading symbol can be used in an element as long as there isn't
a duplicate element without a loading symbol.


