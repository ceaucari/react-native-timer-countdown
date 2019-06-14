
<p align="center">
<a href="https://www.npmjs.com/package/react-native-timer-countdown" alt="npm version"><img src="https://badge.fury.io/js/react-native-timer-countdown.svg" /></a>
<a href="https://travis-ci.com/noelyoo/react-native-timer-countdown" alt="npm license"><img src="https://travis-ci.com/noelyoo/react-native-timer-countdown.svg?branch=master" /></a>
<a href="https://www.npmjs.com/package/react-native-timer-countdown" alt="npm downloads monthly"><img src="https://img.shields.io/npm/dm/react-native-timer-countdown.svg" /></a>
<a href="https://www.npmjs.com/package/react-native-timer-countdown" alt="npm license"><img src="https://img.shields.io/npm/l/react-native-timer-countdown.svg" /></a>
</p>

<h2 align="center">React Native Timer Countdown</h2>

<p align="center">
⏱ A minimal and customizable countdown timer<br/>
for React Native (iOS and Android)
</p>

<p align="center"><img src="https://raw.githubusercontent.com/noelyoo/react-native-timer-countdown/master/demo.gif" align="center" width="175px" /></p>

## Installation

```sh
npm install --save react-native-timer-countdown
```

or

```sh
yarn add react-native-timer-countdown
```

## Example

```javascript
import React from "react";
import { StyleSheet, View } from "react-native";
import TimerCountdown from "react-native-timer-countdown";

const App = () => (
  <View style={styles.container}>
    <TimerCountdown
      initialMilliseconds={1000 * 60}
      onTick={(milliseconds) => console.log("tick", milliseconds)}
      onExpire={() => console.log("complete")}
      formatMilliseconds={(milliseconds) => {
        const remainingSec = Math.round(milliseconds / 1000);
        const seconds = parseInt((remainingSec % 60).toString(), 10);
        const minutes = parseInt(((remainingSec / 60) % 60).toString(), 10);
        const hours = parseInt((remainingSec / 3600).toString(), 10);
        const s = seconds < 10 ? '0' + seconds : seconds;
        const m = minutes < 10 ? '0' + minutes : minutes;
        let h = hours < 10 ? '0' + hours : hours;
        h = h === '00' ? '' : h + ':';
        return h + m + ':' + s;
      }}
      allowFontScaling={true}
      style={{ fontSize: 20 }}
    />
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center"
  }
});

export default App;
```

## Props

| Name | Type | Description | Required |
| :--- | :--- | :--- | :---: |
| initialMilliseconds | number | The remaining milliseconds for the countdown | Yes |
| formatMilliseconds | function<br/><sub>(milliseconds: number) => void</sub> | A function that formats the milliseconds | No |
| onTick | function<br/><sub>(milliseconds: number) => void</sub> | A function to call each tick |  No |
| onExpire | function<br/><sub>() => void</sub> | A function to call when the countdown finishes | No |
| allowFontScaling | boolean | A boolean for [allowFontScaling](https://facebook.github.io/react-native/docs/text#allowfontscaling). The default is `false` | No |
| style | object | Custom style to be applied to the [Text component](https://facebook.github.io/react-native/docs/text) | No |

## FAQ

### Why does this timer restart whenever I click any button?

#### What's happening

buttons clicked -> state changes -> react rerenders -> timer restarts

#### How to not to restart the timer component

Provided the state changes only occur in component B, A component will not rerender. As a result, no more unintended timer restarts.

```javascript
import React, { Component } from "react";
import { StyleSheet, Button, View } from "react-native";
import TimerCountdown from "react-native-timer-countdown";

const A = () => (
  <View style={styles.container}>
    <B />
    <TimerCountdown initialMilliseconds={1000 * 60} />
  </View>
);
export default A;

class B extends Component {
  state = { isPressed: false };
  render() {
    return (
      <View styles={{ flex: 1 }}>
        <Button
          title={`${this.state.isPressed ? "Button Pressed" : "Button"}`}
          onPress={() => {
            this.setState({ isPressed: true });
          }}
        />
      </View>
    );
  }
}


const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center"
  }
});
```
## Contributing

We recommend the community help us make improvements. To report bugs please create an issue in this repository.

#### Read our [contribution guidelines](./CONTRIBUTING.md).

## Author

[Noel Yoo](https://noelyoo.github.io/resume)

## License

MIT
