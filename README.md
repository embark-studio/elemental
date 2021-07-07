# Elemental Design and Development Guide

## Developers
### Quick Reference
#### REMEMBER 
#### Element < Group < Partials < Templates < Yields
#### Smallest < Largest

|                 | Element   | Group | Partials | Templates |  Yields |
| :-------------- |:---------:| :---: | :-------:| :------:  | :-----: |
| Only 1 Element  |     X     |       |          |           |         | 
| 2+  Elements    |           |   X   |     X    |           |X        |
| Functional      |     X     |   X   |          |           |         |
| Class Based     |     X     |   X   |     X    |     X     |X        |
| Logic           |           |       |     X    |     X     |X        | 
| Routes          |           |       |          |     X     |X        |
| Can Be Top Most |           |       |          |           |X        |




## Designers
### Quick Reference

|                   | Element   | Group | Partials | Templates | Yields  |
| :---------------  |:---------:| :---: | :-------:| :------:  | :-----: |
| Only 1 Element    |     X     |       |          |           |         | 
| 2+  Elements      |           |   X   |     X    |           |X        |
| UI Design         |     X     |   X   |     X    |           |         |
| UX Design         |           |       |     X    |     X     |X        | 
| External Data     |           |       |     X    |     X     |X        | 
| URL Based Coices  |           |       |          |     X     |X        |
| Can Be Outer Most |           |       |          |           |X        |

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
Elements that require state should be placed in the elements folder since it should only exist in one location.

###### Appearance of type
If it appears to be an element, as in it looks like 1 element, a drop down etc., but requires extra divs, it is still an element.

#### UX
User experience design (UX, UXD, UED or XD) is the approach of using analytical tools to improve the mechanics of the interface.

#### UI
User interface design (UI) is used to describe graphical or aesthetic changes that improve the interface.  

#### Reasons for UX / UI breakdown
Good design is not focused only on mechanics or function, and good design is not focused entirely on what is the most aesthetically pleasing, and good design is not focusing on mechanics and aesthetics at the same time. Good design is focusing on mechanics and aesthetics separately, at different times, but giving them equal attention. 
This doesn't mean that in some way that can't drive one another, it just means that they are different things and what looks good won't always keep users, and what works well doesn't always draw in users, both areas must be addressed.

# Redux conventions

## Actions

### Action naming
* CREATE, FETCH, UPDATE, DESTROY/ARCHIVE are your crud actions (although DESTROY will sometimes archive)
* Name the crud actions using the singular

* The constants for the actions will be [verb] _ [noun] because it sounds good
* The functions that call the actions (imported from action/index.js) will be [verb][noun], in camel case, for the sake of consistency

* The main disadvantage of putting of the a verb first is that actions can quickly become disorganized, causing developers to potentially create actions that replicate already existing actions. This is bad. Therefore, make sure to organize actions according to the noun. 

The right way: (in the actions/types.js file)
```
  CREATE_ORGANIZATION: 'CREATE_ORGANIZATION',
  UPDATE_ORGANIZATION: 'UPDATE_ORGANIZATION',
  RETRIEVE_ORGANIZATION: 'RETRIEVE_ORGANIZATION'
```

The wrong way:
```
  RETRIEVE_ORGANIZATION: 'RETRIEVE_ORGANIZATION',
  RETRIEVE_USERS: 'RETRIEVE_USERS'
```
This way, if someone wants to fetch organizations, they won't accidentally do a search for "fetch" or "get", not see anything, and then create a new action "FETCH_ORGANIZATION"


### Action wrappers (aka, how to do asynchronous stuff)
In order to avoid dispatching unnecessary actions and to avoid unnecessary complexity, we are not going to use redux sagas or thunk. Instead, we will simply wrap our redux actions in a function, eg,

```
//in admin/actions/organizationActions.js
import adminActionTypes from 'admin/actions/types'
import sharedActionTypes from 'shared/actions/types'

export const createOrganization (payload) => {
  new Promise((resolve, reject) => {
    axios.post("/organizations", payload)  
  })
  .then((response) => {
    store.dispatch({
      type: adminActionTypes.CREATE_ORGANIZATION,
      payload: response
    })
  })
  .catch((err) => {
    //probably handle errors a little differently, but this is just an example 
    store.dispatch({
      type: sharedActionTypes.HANDLE_ERROR,
      payload: err
    })
  })
}

//in admin/components/partials/NewOrganization.js
import { organizationActions } from 'admin/actions'

...
handleSubmit (e, newOrganization) {
  e.preventDefault()
  organizationActions.createOrganization(newOrganization)
}

render ...
```

I like to call these functions that wrap the actions "action functions". 
As the example above shows, rather than dispatching actions from a component, a component will import all of the action functions it needs, and simply call the function. 

### Handling callbacks
Often, components will need to respond to the result of asynchronous actions.

Rather than having the action function returning a promise to the component, or even passing a call back to the action function from the component, we will keep our code clean and organized by only communicating with the component via actions. As the above example shows, even errors are handled through dispatching actions.

```
...
  .catch((err) => {
    //probably handle errors a little differently, but this is just an example 
    store.dispatch({
      type: sharedActionTypes.HANDLE_ERROR,
      payload: err
    })
  })
...
```
If a component needs to respond to this error, it should receive this error from props by subscribing via mapStateToProps. `this.componentWillReceiveProps` will often come in handy to respond to changes in the store.


Summary:
* Action constants and functions should be named verb first ("createUserForLine")
* Wrap actions in functions
* Even redux actions that do not require any asynchronous code should still be wrapped in functions, for consistency and organization
