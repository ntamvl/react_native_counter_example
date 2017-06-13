# React Native Counter Example
Use `create-react-native-app` and `redux`

## Install `create-react-native-app`
Following https://facebook.github.io/react-native/docs/getting-started.html

Use npm to install the create-react-native-app command line utility:
```
npm install -g create-react-native-app
```

## Create App
```
cd && mkdir react_native_counter_example && cd react_native_counter_example && create-react-native-app .
```

## Create folders
```
mkdir -p src/{components,containers,store}
```

## Add package `react-redux`, `redux`
```
yarn add redux react-redux
```

## Create Counter component
Create file `src/components/Counter.js`

```JavaScript
import React, { Component } from 'react';
import {
  Button,
  StyleSheet,
  Text,
  View,
} from 'react-native';

const propTypes = {};

const defaultProps = {};

export default class Counter extends Component {

  constructor(props) {
    super(props);
    this.state = {};
  }

  render() {
    return (
      <View>
        <Button
          title="Up"
          onPress={this.props.increment}/>
        <Text
          style={styles.counter}
          onPress={this.props.reset}>
          {this.props.count}
        </Text>
        <Button
          title="Down"
          onPress={this.props.decrement}/>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  counter: {
    padding: 30,
    alignSelf: 'center',
    fontSize: 26,
    fontWeight: 'bold',
  },
});
```

## Create store
Create file `src/store/store.js`

```JavaScript
import { createStore } from 'redux'

export const counter = (state = 0, action) => {
  switch (action.type) {
  case 'INCREMENT':
    return state + 1;
  case 'DECREMENT':
    return state - 1;
  case 'RESET':
    return 0;
  default:
    return state;
  }
}

let store = createStore(counter);

export default store;
```

## Create Counter container
Create file `src/containers/CounterContainer.js`

```JavaScript
import React, { Component } from 'react';
import { bindActionCreators } from 'redux';
import { connect } from 'react-redux';
import Counter from '../components/Counter';

const mapStateToProps = state => ({
  count: state
})

const mapDispatchToProps = (dispatch) => ({
  increment: () => { dispatch({ type: 'INCREMENT' }) },
  decrement: () => { dispatch({ type: 'DECREMENT' }) },
  reset: () => { dispatch({ type: 'RESET' }) }
})

export default connect(mapStateToProps, mapDispatchToProps)(Counter)
```

## Edit file `App.js`

```JavaScript
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import { Provider } from 'react-redux';
import store from './src/store/store';
import CounterContainer from './src/containers/CounterContainer';

export default class App extends React.Component {
  render() {
    return (
      <Provider store={store}>
        <View style={styles.container}>
          <Text style={styles.title}>Counter</Text>
          <CounterContainer />
        </View>
      </Provider>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  title: {
    fontSize: 30
  }
});
```

## To run App
```
yarn start
```
OR
```
yarn run ios
```

NOTE: If you see errors:
```
Duplicate module name: fb-watchman
```

To Resolve, run this command:
```
yarn cache clear
```
