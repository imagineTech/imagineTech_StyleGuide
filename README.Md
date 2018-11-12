# ImagineTech's Style Guide

### Overview:

We will go over the Architecture and Style Guide for ImagineTech. Here are some things we will be covering:

- Design Pattern
- Folder Structure
- Component Building
- Github Etiquette
- Prettier Configuration

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

## Folder Structure

Now with the design pattern explained, i want to go over how it will now correlate with our Folder Structure. This structure can be broken down into 4 parts:

- Components
  - Any presentational, or container style type of component that pertain to the project.
- Screens
  - You can consider this our View folder. As these components will only be used to display other components back to the user. We will also place our routing in this folder.
- Repeats
  - And repeat type of components, such as, navigation, buttons, css-based components, etc.
- Config
  - This folder will contain our one off type files, such as the configuration for a redux store. We will also hold our gitignore files here as this folder will hold senstive API key information.

### Folder Naming

Our naming convention will be based off page/feature. Such About, Contact, User, Products, Services, etc. Below is an folder example with 3 routes:

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

Here's what each individual page/feature folder will include:

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

- _index.js_ - This is our container, every page/feature folder **WILL** contain a index.js regardless of size.
- _Content.js and Video.js_ - These are the components that would make up this Home page. If it was contact, it would be the form and so on.
- _css and main.css_ - Each page/feature will have either one main css file, when a directory reaches over 5 css files, then it will be moved into it's own css sub-directory.

#### Screens

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

The components being used in this directory are the page/feature containers from components directory. If the site begans to scale than you would follow the saming folder naming conventation, seperated by page/feature.

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

- Arrow Functions
- Destructuring Assignment
- Spread Operator
- Ternary Operators
- Template Literals
- Promises
- Default Parameters

To understand what these features are, please visit this [ES6 reference](http://es6-features.org).

#### Things to consider when building your Components

---

_Size of the Component_

- You may come across a situation where the amount of content for a page/feature doesn't need more than one component and it would seem logical to write all of that content in the `index.js` file. However, while keeping scalability and testing in mind, we must leave `index.js` as a container that holds the components together. Any JSX should be written as an individual component regardless of the size.

_Composition (Referencing other Components)_

- To continue following a MVVM pattern, any reference of one particular page/feature component in another must be done via the **Screens** directory. This sort of referencing is dealing with how the user _views_ the screen, which means this is part of the **View** layer.
- Currently, any reason not to follow this pattern would be because components need to share data from other sources. And if so, it would be best to use React's `this.props.children` for this sort of reference.

## Github Etiquette

Being an efficent development team goes beyond just coding, we all have to work together to build a streamlined development process. One area of that process is Github. The following content will go over what it takes to maximize on what Github has to offer for teams. Please note that this under the assumption you're connected with the ImagineTech Organization.

#### Forked Repos:

All assigned team members to a project will have to fork over a copy to their local machine. No one should work directly with repo's master branch unless specifically assigned to.

#### Branches:

As we won't be monitoring how branches are setup in your Forked Copy, however it is recommended to create your branches based off the feature you're working. As for the Mater repo, there will only be two main branches. One is the Main Master and the other is the Development branch. All Pull Requests will be merged onto the Main Master, once the project is ready for deployment, we will use the Development branch.

#### Pull Requests:

Before diving in, please understand that Pull Requests aren't just about Merging. At it's core, it's meant to create a open-ended discussion on why you believe your code should be mergered into Main Master. If your request is denied, do not take it as insult to you and your coding ablities. For a basic understanding on how and what a Pull Request is, visit this [tutorial](https://help.github.com/articles/creating-a-pull-request/). Some things to keep in mind when working with PRs:

- All PRs will follow a Forked Master into Main Master merge flow. Once you have finish your commits/goal/feautre from your Forked Repo, you will then perform a PR onto the Main Master.
- We require at least one person to be assigned to review the PR, default is the Team Architect or your Team Lead.
- Make sure PRs are apporiate, if you have a question, or can't figure out a bug then that's not a good reason for a pull request. If you are wanting to imporve a feature/code base or even correct grammer and spelling, then submitting a pull request would be your best bet.

## Prettier Configuration

To make sure we also upkeep a consistent, best practice code style, we will be working with Prettier and with the use of CRA (Create-React-App), we can place the following configuration for prettier within our `package.json` file:

```
  "eslintConfig": {
    "extends": "react-app",
    "plugins": [
      "prettier"
    ],
    "rules": {
      "prettier/prettier": "error"
    },
    "husky": {
      "hooks": {
        "pre-commit": "pretty-quick --staged"
      }
    }
  }
```

Please note that we are using `devDependencies` such as `eslint-plugin-prettier`, `husky`, and `pretty-quick`. Also any additional prettier configuration should be done in a `.prettierrc.json` file.
