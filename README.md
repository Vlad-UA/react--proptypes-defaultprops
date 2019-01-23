# propTypes and defaultProps
Info about propTypes and defaultProps in React.

## What for?
**propTypes** -- To run typechecking on the props for a component<br>
**defaultProps** -- define default values for your props


## Links
1. Source code React - https://github.com/facebook/prop-types
2. Documentation - https://reactjs.org/docs/typechecking-with-proptypes.html
3. Article - https://blog.logrocket.com/validating-react-component-props-with-prop-types-ef14b29963fc
4. My contribution into reactjs.org - https://github.com/reactjs/reactjs.org/pull/1581


## Installation
npm install --save prop-types

## Importing
import PropTypes from 'prop-types';

## Types
```javascript
import PropTypes from 'prop-types';

MyComponent.propTypes = {
  // You can declare that a prop is a specific JS type. By default, these
  // are all optional.
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,


  // Anything that can be rendered: numbers, strings, elements or an array
  // (or fragment) containing these types.
  optionalNode: PropTypes.node,


  // A React element.
  //
  // https://blog.logrocket.com/validating-react-component-props-with-prop-types-ef14b29963fc
  // One common usage of the PropTypes.element validator is in ensuring that a component has a single child. 
  // If the component has no children or multiple children, a warning is displayed on the JavaScript console. 
  optionalElement: PropTypes.element,


  // You can also declare that a prop is an instance of a class. This uses
  // JS's instanceof operator.
  optionalMessage: PropTypes.instanceOf(Message),


  // You can ensure that your prop is limited to specific values by treating
  // it as an enum.
  optionalEnum: PropTypes.oneOf(['News', 'Photos']),


  // An object that could be one of many types
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),


  // An array of a certain type
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number),
    
        // Examples:
        peopleArrayProp: PropTypes.arrayOf(
          PropTypes.instanceOf(Person)
        ),
        
        multipleArrayProp: PropTypes.arrayOf(
          PropTypes.oneOfType([
            PropType.number,
            PropType.string
          ])
        ),
      

  // An object with property values of a certain type
  optionalObjectOf: PropTypes.objectOf(PropTypes.number),
        
        // Example:
          booleanObjectProp: PropTypes.objectOf(
            PropTypes.bool
          ),
          
          multipleObjectProp: PropTypes.objectOf(
            PropTypes.oneOfType([
              PropType.func,
              PropType.number,
              PropType.string,
              PropType.instanceOf(Person)
            ])
          ),


  // An object taking on a particular shape
  //
  // MY COMMENT: may be better consider PropTypes.exact
  optionalObjectWithShape: PropTypes.shape({
    color: PropTypes.string,
    fontSize: PropTypes.number
  }),
        // Example:
        // can be used when a more detailed validation of an object prop is required. 
        // It ensures that the prop is an object that contains a set of specified keys with values of the specified types.
          profileProp: PropTypes.shape({
            id: PropTypes.number,
            fullname: PropTypes.string,
            gender: PropTypes.oneOf(['M', 'F']),
            birthdate: PropTypes.instanceOf(Date),
            isAuthor: PropTypes.bool
          }),
          
  // An object with warnings on extra properties
  // https://github.com/facebook/prop-types
  optionalObjectWithStrictShape: PropTypes.exact({
    optionalProperty: PropTypes.string,
    requiredProperty: PropTypes.number.isRequired
  }),                          


  // You can chain any of the above with `isRequired` to make sure a warning
  // is shown if the prop isn't provided.
  requiredFunc: PropTypes.func.isRequired,


  // A value of any data type
  requiredAny: PropTypes.any.isRequired,


  // You can also specify a custom validator. It should return an Error
  // object if the validation fails. Don't `console.warn` or throw, as this
  // won't work inside `oneOfType`.
  //
  // MY COMMENT: more about Custom Validation with example
  // https://blog.logrocket.com/validating-react-component-props-with-prop-types-ef14b29963fc#4a62
  customProp: function(props, propName, componentName) {
    if (!/matchme/.test(props[propName])) {
      return new Error(
        'Invalid prop `' + propName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  },


  // You can also supply a custom validator to `arrayOf` and `objectOf`.
  // It should return an Error object if the validation fails. The validator
  // will be called for each key in the array or object. The first two
  // arguments of the validator are the array or object itself, and the
  // current item's key.
  customArrayProp: PropTypes.arrayOf(function(propValue, key, componentName, location, propFullName) {
    if (!/matchme/.test(propValue[key])) {
      return new Error(
        'Invalid prop `' + propFullName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  })
};
```

## Requiring Single Child
With PropTypes.element you can specify that only a single child can be passed to a component as children.
```javascript
import PropTypes from 'prop-types';

class MyComponent extends React.Component {
  render() {
    // This must be exactly one element or it will warn.
    const children = this.props.children;
    return (
      <div>
        {children}
      </div>
    );
  }
}

MyComponent.propTypes = {
  children: PropTypes.element.isRequired
};
```

## Default Prop Values
```javascript
class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

// Specifies the default values for props:
Greeting.defaultProps = {
  name: 'Stranger'
};

// Renders "Hello, Stranger":
ReactDOM.render(
  <Greeting />,
  document.getElementById('example')
);
```
