# ImagineTech's Style Guide

### Overview:
We will go over the Architecture and Style Guide for ImagineTech. Here are some things we will be covering:
  * Design Pattern
  * Folder Structure
  * Component Building

## Design Pattern: 
ImagineTech will be using a MVVM design pattern. Here's how design parts will corlate with our folder structure; 
  * _View:_ Presentational Components, only data that is displaying to the user
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
      }

      render() {
        return (
          <div>
            <PresCompOne />
            <PresCompTwo />
          </div>
        )
      }
    }
    ```