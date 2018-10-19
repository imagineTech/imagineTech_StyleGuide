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

  ### Folder Naming
  Our naming convention will be based off Route/Feature. Such About, Contact, User, Products, Services, etc. Below is an folder example with 3 routes: 
  #### Components 
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

#### Screens
Only one slight difference, in the Screens folder we will start out with only the need files. Small scale websites will usually only have one Root.js screen file. 
```
class ScreenRoot extends Component {
  ...
   <Switch>
      <Route exact path="/" component={Home} />
      <Route path="/team" component={About} />
      <Route path="/contact" component={Contact} />
    </Switch>
  ...
}
```
As you can see, Screens are going to be for our View layer and where React Router will take place. If the site begans to scale than you would follow the saming folder naming conventation, seperated by Route/Feature. 

### File Naming
Our file naming will follow a top-down method. Let's start with our container / index.js file. The start of the name will be after the Route/Feature, and the last portion will be the name of the file within that Route/Feature. Example: 
  ```
  ...
  |-/src
  |--/components
  |---/Contact
  |---- Form.js
  |---- index.js
  ...
  Form.js
    const ContactForm = () => {
      ...
    } 
  ...
  index.js
    import ContactForm from './Form'
    ...
    class ContactContainer extends Component {
      ...
      <ContactForm />
    }
  ...
  ```
  We start off with Form.js, if follow the top-down folder naming, you can see how i came up with ContactForm and ContactContainer (index.js is our container) Something else to consider is that we will not be using extensions in our imports, as ES6 doesn't require '.js'. 
  ```
  import ContactForm from './Form'
  ```
  Also we will not include 'index.js' when importing our container, we will allow ES6 to choose it for us like so; 
  ```
  import Contact from '../components/Contact';
  ```
  ES6 is aware that by not including a file name after a folder, that it will default to index.js. 

## Component Building
This will consistof multiple ES6 features. Here is what we will be using: 
  * Arrow Functions
  * Destructuring Assignment
  * Spread Operator
  * Ternary Operators
  * Template Literals 
  * Promises
  * Default Parameters

To understand what these features are, please visit this [ES6 reference](http://es6-features.org).

## Github Etiquette
Being an efficent development team goes beyond just coding, we all have to work together to build a streamlined development process. One area of that process is Github. The following content will go over what it takes to be an maximize on what Github has to offer for teams 

#### Pull Requests: 
#### Forked Repos: 