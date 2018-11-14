# ImagineTech's Style Guide

### Overview:

We will go over the Architecture and Style Guide for ImagineTech. Here are some things we will be covering:

- Design Pattern
- Directory Structure
- Component Building

## Design Pattern:

ImagineTech will be using a MVVM design pattern. Here's how we're breaking the parts down;

- _View:_ Presentational Components, only data that is displaying to the user either hard coded or from the Parent Component
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
- _View Controller:_ Telling our View how to think, this will be our container file. It's gets it's methods from the View Model. General use from these files are holding all of the page/feature components together and placing any common VM/M methods that the components will need at some point in time.

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

- _View Model:_ Here will contain the neeeded methods/functions for the View Controller to work. The VM in our case will usually be our Redux Actions and Reducers as it is updating the View Layer via the VC. For the VM we will use vanilla functions or vanilla classes. This will allow for cross reference with other JS libaries such as Angluar, Vue, etc.

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

- _Model:_ For this last porition, here we will place our 3rd party library methods. If none are avaiable then we can use the View Model in it's place. And just like the VM, we use vanilla JS classes or functions. These methods will talk to the VM which in turn will be used in the VC which will update the View.
  ```
  export const thirdPartyMethod = data => {
    return ThirdParth.someMethod(data);
  }
  ```

## Directory Structure

Now with the design pattern explained, i want to go over how it will now correlate with our Directory Structure. This structure can be broken down into 4 parts:

- Components
  - Any presentational, or container style type of component that pertain to the project.
- Screens
  - You can consider this our View directory. As these components will only be used to display other components back to the user. We will also place our routing in this directory.
- Repeats
  - And repeat type of components, such as, navigation, buttons, css-based components, etc.
- Config
  - This directory will contain our one off type files, such as the configuration for a redux store. We will also hold our gitignore files here as this directory will hold senstive API key information.

  A quick example would like so: 
  ```
  ...
  |-/src
  |--/components
  |--/screens
  |--/repeats
  |--/config
  ...
  ```

### Directory and File setup

There are a few moving parts when looking creating directories for the project and the files that will correlate within them. Let us look at our two more domainant directories, Components and Screens.

#### Components

Our naming convention will be based off page/feature. Such as About, Contact, User, Products, Services, etc. Below is an directory example with 3 pages:

```
...
|-/src
|--/components
|---/Home
|---/About
|---/Contact
...
```

Now let's talk about what file(s) will be included in each directory. Here's what each individual page/feature directory will include:

```
...
|-/Home
|---/css
|----main.css
|---index.js
|---Content.js
|---Video.js
...
```

- _index.js_ - This is our container, every page/feature directory **WILL** contain a index.js regardless of size.
- _Content.js and Video.js_ - These are the components that would make up this Home page. If it was contact, it would be the form and so on.
- _css and main.css_ - Each page/feature will have either one main css file, when a directory reaches over 5 css files, then it will be moved into it's own css sub-directory.

#### Screens

We can expect most projects to contain no more than few files when looking within the Screen files. The most common one being Root.js (more on this later), any other file could be dealing with nested routes/components that need to have their own file. 
  ```
  ...
  |-/src
  |--/screens
  |---/Root.js
  |---/NestedRoute.js
  ...
  ```
In this example, `NestedRoute.js` has been seperated from the main `Root` due to it's volume. You'll see more on what that means later on the Component Building section. 

### File Naming

Our file naming will follow a top-down method. Let's start with our container / index.js file. The start of the name will be after the page/feature, and the last portion will be the name of the file within that page/feature. Example:

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

We start off with Form.js, if follow the top-down directory naming, you can see how i came up with ContactForm and ContactContainer (index.js is our container) Something else to consider is that we will __not__ be using extensions in our imports, as ES6 doesn't require `.js`.

```
import ContactForm from './Form'
```

Also we will not include `index.js` when importing our container, we will allow ES6 to choose it for us like so;

```
import Contact from '../components/Contact';
```

ES6 is aware that by not including a file name after a directory, that it will default to `index.js`.

## Component Building

Now we will look at what goes into building these files, what goes into building components for pages, features and screens. Before we can begin, there are ES6 features you should know ahead of time. Here's the list of those features:

- Arrow Functions
- Destructuring Assignment
- Spread Operator
- Ternary Operators
- Template Literals
- Promises
- Default Parameters

To understand what they are, please visit [here](http://es6-features.org).

### Components

#### Containers

To start off, let's look at how a simple `index.js` is build.   First, our container will host any methods that deal with redux, a 3rd party or an API call. 
  ```
  ...
  class PageContainer extends Component { 
    ...
    comoponentDidMount() {
      someAPIMethod()
    }

    someMethod = () => {
      aThirdPartyMethod();
    }
    ...
  }
  ```
Next, we need to look at how stateless components will be setup. We will arrange the stateless components based on how we want the page to initally look. Here's where we will also send data down via `this.props`. 
  ```
  class PageContainer extends Component {
    ...
    render() {
      <div>
        <PageContent />
        <PageForm submit={this.submit} />
        <PageImage />
      </div>
    }
    ...
  }
  ```
#### Presentational

During a project we will need to write components that show the user the releated page content. These presentational or stateless components will hold this content. Here's how a simple one is setup: 
  ```
  ...
  const PageContent = ({ somePropsMethod, anotherProps }) => {
    return (
      <div className="page-related-css-name">
        <p> I am some content related to the page. </p>
      </div>
    )
  }
  ...
  ```

#### Things to consider when building your Components

---

_Size of the Component_

- You may come across a situation where the amount of content for a page/feature doesn't need more than one component and it would seem logical to write all of that content in the `index.js` file. However, while keeping scalability and testing in mind, we must leave `index.js` as a container that holds the components together. Any JSX should be written as an individual component regardless of the size.

_Composition (Referencing other Components)_

- To continue following a MVVM pattern, any reference of one particular page/feature component in another must be done via the **Screens** directory. This sort of referencing is dealing with how the user _views_ the screen, which means this is part of the **View** layer.
- Currently, any reason not to follow this pattern would be because components need to share data from other sources. And if so, it would be best to use React's `this.props.children` for this sort of reference.

_Page versus Feature_

- At some point in a project, it will scale to where Features are clearly separate from Pages. An example would be creating, storing, and referencing User Data. This would require a lot more files that are more than just dealing with the View layer.

  Two subcategories will then be created from components, one for Page and the other for Feature. The real difference is that Feature(s) will store files relevant to the View-Model/Model layer, allowing for the `index.js` to be nothing more than a group of method/function/classes being exported at once for easier reference whenever needed. 

### Screens

This is where we build our View layer, this is what the user will see on their screen. Small scale websites will usually only have one Root.js screen file.

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

The components being used in this directory are the page/feature containers from components directory. If the site begans to scale than you would follow the saming directory naming conventation, seperated by page/feature.

If a project doesn't require React Router, you willd build the same way just without using any components from React Router:

```
...
<div>
  <Home />
  <About />
  <Contact />
</div>
...
```


