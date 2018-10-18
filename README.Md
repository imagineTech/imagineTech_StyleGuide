# ImagineTech's Style Guide

### Overview:
We will go over the Architecture and Style Guide for ImagineTech. Here are some things we will be covering:
  * Design Pattern
  * Folder Structure
  * Component Building

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
  * _View Controller:_ Telling our View how to think, this will be our container file which will always placed in a index.js. 
    ```
    class ContainerComp extends Component {
      handlingFunction = () => {
        /.../
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
          /.../
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
  * Screens
  * Repeats 
  * Config