# Elemental Design and Development Guide

## Developers
### Quick Reference
#### REMEMBER 
#### Element < Group < Partials < Templates < Yields
#### Smallest < Largest

|                 | Element   | Group | Partials | Templates |  Wireframes |
| :-------------  |:---------:| :---: | :-------:| :------:  | ----------: |
| Only 1 Element  |     X     |       |          |           |             | 
| 2+  Elements    |           |   X   |     X    |           |      X      |
| Functional      |     X     |   X   |          |           |             |
| Class Based     |           |       |     X    |     X     |      X      |
| Logic           |           |       |     X    |     X     |      X      | 
| Routes          |           |       |          |     X     |      X      |
| Can Be Top Most |           |       |          |           |      X      |




## Designers
### Quick Reference

|                   | Element   | Group | Partials | Templates | Wireframes |
| :---------------  |:---------:| :---: | :-------:| :------:  | ---------: |
| Only 1 Element    |     X     |       |          |           |            | 
| 2+  Elements      |           |   X   |     X    |           |      X     |
| UI Design         |     X     |   X   |     X    |           |            |
| UX Design         |           |       |     X    |     X     |      X     | 
| Data Flow         |           |       |     X    |     X     |      X     | 
| URL Based Coices  |           |       |          |     X     |      X     |
| Can Be Outer Most |           |       |          |           |      X     |

### Note: Data Flow is how / when data is introduced to the component

# Nesting Components:
All types of components can have another component of their own level or less

Example Breakdown

#### Example:
* A Group can have a Group
* A Group can have an Element
* A Group **Can't** have a Template
![example image](/example.png?raw=true)

# Folder Structure
* component type (Group)
  * ComponentName
    * index.js
    * style.scss

### Example:
* groups
  * InputField
    * index.js
    * style.scss
#### Note - Export all components in each component type with an index.js
## Definition of Terms


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
###### Loading Symbols
A loading symbol can be used in an element as long as there isn't
a duplicate element without a loading symbol.

###### Elements That Require State
It is more important that what appears to be a single element that requires state exists in the only location a single element may exist in

#### UX
User experience design (UX, UXD, UED or XD) is the approach of using analytical tools to improve the mechanics of the interface.

#### UI
User interface design (UI) is used to describe graphical or aesthetic changes that improve the interface.  

#### Reasons for UX / UI breakdown
Good design is not focused only on mechanics or function, and good design is not focused entirely on what is the most aesthetically pleasing, and good design is not focusing on mechanics and aesthetics at the same time. Good design is focusing on mechanics and aesthetics separately, at different times, but giving them equal attention. 
This doesn't mean that in some way that can't drive one another, it just means that they are different things and what looks good won't always keep users, and what works well doesn't always draw in users, both areas must be addressed.
