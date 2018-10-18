# ImagineTech's Style Guide

### Overview:
We will go over the Architecture and Style Guide for ImagineTech. Here are some things we will be covering:
  * Design Pattern
  * Folder Structure
  * Component Building

## Design Pattern: 
ImagineTech will be using a MVVM design pattern. Here's how design parts will corlate with our folder structure; 
  * _View_: Presentational Components, only data that is displaying to the user
    ` const PresComp = props => {
        return (
          <div>
            <h1>Hello</h1>
            <p>{props.parentDataValue}</p>
          </div>
        )
      }`