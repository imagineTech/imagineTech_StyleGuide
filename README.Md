# ImagineTech's Style Guide

### Overview:
We will go over the Architecture and Style Guide for ImagineTech. Here are some things we will be covering:
  * Design Pattern
  * Folder Structure
  * Component Building
  * Github Etiquette

## Design Pattern: 
ImagineTech will be using a MVVM design pattern. Here's how we're breaking the parts down; 
  * _View:_ Presentational Components, only data that is displaying to the user either hard coded or from the Parent Component
    ```
    const PresComp = props => {
        return (
          <div>
            <h1>Hello</h1>
            <p>{props.parentDataValue}</p>
          </div>
        )
      }
      ```
  * _View Controller:_ Telling our View how to think, this will be our container file. It's gets it's methods from the View Model.
    ```
    class ContainerComp extends Component {
      handlingFunction = () => {
        ...
        partentDataValue = "A parent value" 
      }

      render() {
        return (
          <div>
            <PresCompOne />
            <PresCompTwo 
              parentDataValue={this.handlingFunction} />
          </div>
        )
      }
    }
    ```
  * _View Model:_ Here will contain the neeeded methods/functions for the View Controller to work. The VM in our case will usually be our Redux Actions and Reducers as it is updating the View Layer via the VC. For the VM we will use vanilla functions or vanilla classes. This will allow for cross reference with other JS libaries such as Angluar, Vue, etc. 
    ```
    export const reduxAction = payload => {
      return {
        type: "REDUX_TYPE", 
        payload
      }
    }

    export const reduxReducer = (state, action) {
      case "REDUX_TYPE: 
        return {
          ...
        }
    }
    ```
  * _Model:_ For this last porition, here we will place our 3rd party library methods. If none are avaiable then we can use the View Model in it's place.  And just like the VM, we use vanilla JS classes or functions. These methods will talk to the VM which in turn will be used in the VC which will update the View. 
    ```
    export const thirdPartyMethod = data => {
      return ThirdParth.someMethod(data);
    }
    ```
## Folder Structure
Now with the design pattern explained, i want to go over how it will now correlate with our Folder Structure. This structure can be broken down into 4 parts: 
  * Components
    * Any presentational, or container style type of component that pertain to the project. 
  * Screens
    * You can consider this our View folder. As these components will only be used to display other components back to the user. We will also place our routing in this folder. 
  * Repeats 
    * And repeat type of components, such as, navigation, buttons, css-based components, etc.
  * Config
    * This folder will contain our one off type files, such as the configuration for a redux store. We will also hold our gitignore files here as this folder will hold senstive API key information.

  ### Folder and File Naming
  Our naming convention will be based off Route/Feature. Such About, Contact, User, Products, Services, etc. Below is an folder example with 3 routes: 
  ### Components 
  ```
  ...
  |-/src
  |--/components
  |---/Home
  |---/About
  |---/Contact
  ...
  ```
  Here's what each individual Route/Feature folder will include: 
  ```
  ...
  |-/Home
  |---index.js
  |---Content.js
  |---Video.js 
  ...
  ```
  * _index.js_ - This is our container, every Route/Feature folder __WILL__ contain a index.js regardless of size. 
  * _Content.js and Video.js_ - These are the components that would make up this Home page. If it was contact, it would be the form and so on. 

### Screens
Only one slight difference, in the Screens folder we will start out with only the need files. Small scale websites will usually only have one Root.js screen file. 
```
class ScreenRoot extends Component {
  ...
   <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/team" component={Team} />
      <Route path="/portfolio" component={Portfolio} />
      <Route path="/services" component={Services} />
      <Route path="/contact" component={Contact} />
    </Switch>
  ...
}
```
