---
id: version-0.63-intro-react
title: React基础
description: To understand React Native fully, you need a solid foundation in React. This short introduction to React can help you get started or get refreshed.
original_id: intro-react
---

##### 本文档贡献者：[sunnylqm](https://github.com/search?q=sunnylqm&type=Users)(100.00%)

React Native 的基础是[React](https://zh-hans.reactjs.org/)， 是在 web 端非常流行的开源 UI 框架。要想掌握 React Native，先了解 React 框架本身是非常有帮助的。本文旨在为初学者介绍一些 react 的入门知识。

本文主要会探讨以下几个 React 的核心概念：

- components 组件
- JSX
- props 属性
- state 状态

如果你想更深一步学习，我们建议你阅读[React 的官方文档](https://zh-hans.reactjs.org/)，它也提供有中文版。

## 尝试编写一个组件

本文档会用“Cat”这种有个名字和咖啡馆就能开始工作的人畜无害的生物来作为例子。下面是我们的第一个 Cat 组件:

<div class="toggler">
  <ul role="tablist" class="toggle-syntax">
    <li id="functional" class="button-functional" aria-selected="false" role="tab" tabindex="0" aria-controls="functionaltab" onclick="displayTabs('syntax', 'functional')">
      函数组件示例
    </li>
    <li id="classical" class="button-classical" aria-selected="false" role="tab" tabindex="0" aria-controls="classicaltab" onclick="displayTabs('syntax', 'classical')">
      Class组件示例
    </li>
  </ul>
</div>

<block class="functional syntax" />

```SnackPlayer name=Your%20Cat
import React from 'react';
import { Text } from 'react-native';
export default function Cat() {
  return (
    <Text>Hello, I am your cat!</Text>
  );
}
```

要定义一个`Cat`组件，第一步要使用[`import`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)语句来引入`React`以及`React Native`的[`Text`](/react-native/docs/next/text)组件：

```jsx
import React from 'react';
import { Text } from 'react-native';
```

然后一个简单的函数就可以作为一个组件：

```jsx
function Cat() {}
```

这个函数的`返回值`就会被渲染为一个 React 元素。这里`Cat`会渲染一个`<Text>`元素：

```jsx
function Cat() {
  return <Text>Hello, I am your cat!</Text>;
}
```

这里我们还使用了[`export default`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)语句来导出这个组件，以使其可以在其他地方引入使用：

```jsx
export default function Cat() {
  return <Text>Hello, I am your cat!</Text>;
}
```

<block class="classical syntax" />

Class 组件比函数组件写起来要繁琐一些。

```SnackPlayer name=Your%20Cat
import React, { Component } from 'react';
import { Text } from 'react-native';
export default class Cat extends Component {
  render() {
    return (
      <Text>Hello, I am your cat!</Text>
    );
  }
}
```

你还需要从 React 中引入`Component`：

```jsx
import React, { Component } from 'react';
```

定义组件首先要继承(extends)自`Component`：

```jsx
class Cat extends Component {}
```

Class 组件必须有一个`render()`函数，它的返回值会被渲染为一个 React 元素：

```jsx
class Cat extends Component {
  render() {
    return <Text>Hello, I am your cat!</Text>;
  }
}
```

和函数组件一样，我们也可以导出 class 组件：

```jsx
export default class Cat extends Component {
  render() {
    return <Text>Hello, I am your cat!</Text>;
  }
}
```

<block class="endBlock syntax" />

> 上面只是导出组件的写法之一。你还可以看看这篇博客整理[handy cheatsheet on JavaScript imports and exports](https://www.samanthaming.com/tidbits/79-module-cheatsheet/)整理的各种不同的写法。下面我们来看看这个`return` 语句。`<Text>Hello, I am your cat!</Text>`是一种简化 React 元素的写法，这种语法名字叫做 JSX。

## JSX

React 和 React Native 都使用**JSX 语法**，这种语法使得你可以在 JavaScript 中直接输出元素：`<Text>Hello, I am your cat!</Text>`。React 的文档有一份完整的[JSX 指南](https://zh-hans.reactjs.org/docs/jsx-in-depth.html#gatsby-focus-wrapper)可供你参考。因为 JSX 本质上也就是 JavaScript，所以你可以在其中直接使用变量。这里我们为猫猫的名字声明了一个变量`name`，并且用括号把它放在了`<Text>`之中。

```SnackPlayer name=Curly%20Braces
import React from 'react';
import { Text } from 'react-native';
export default function Cat() {
  const name = "Maru";
  return (
    <Text>Hello, I am {name}!</Text>
  );
}
```

括号中可以使用任意 JavaScript 表达式，包括调用函数，例如`{getFullName("Rum", Tum", "Tugger")}`：

```SnackPlayer name=Curly%20Braces
import React from 'react';
import { Text } from 'react-native';
export default function Cat() {
  function getFullName(firstName, secondName, thirdName) {
    return firstName + " " + secondName + " " + thirdName;
  }
  return (
    <Text>
      Hello, I am {getFullName("Rum", "Tum", "Tugger")}!
    </Text>
  );
}
```

你可以把括号`{}`想象成在 JSX 中打开了一个可以调用 JS 功能的传送门！

> 因为 JSX 语法糖的实质是调用`React.createElement`方法，所以你必须在文件头部引用`import React from 'react'`。

## 自定义组件

你应该已经了解[React Native 的核心组件](intro-react-native-components)了。 React 使得你可以通过嵌套这些组件来创造新组件。这些可嵌套可复用的组件正是 React 理念的精髓。

例如你可以把[`Text`](text)和[`TextInput`](textinput)嵌入到[`View`](view) 中，React Native 会把它们一起渲染出来：

```SnackPlayer name=Custom%20Components
import React from 'react';
import { Text, TextInput, View } from 'react-native';
export default function Cat() {
  return (
    <View>
      <Text>Hello, I am...</Text>
      <TextInput
        style={{
          height: 40,
          borderColor: 'gray',
          borderWidth: 1
        }}
        defaultValue="Name me!"
      />
    </View>
  );
}
```

<div class="toggler">
  <span>对开发者的提示：</span>
  <span role="tablist" class="toggle-devNotes">
    <button role="tab" class="button-webNote" onclick="displayTabs('devNotes', 'webNote')">Web</button>
    <button role="tab" class="button-androidNote" onclick="displayTabs('devNotes', 'androidNote')">Android</button>
  </span>
</div>

<block class="webNote devNotes" />

> 如果你熟悉 web 开发，`<View>`和`<Text>`应该能让你想起 HTML。你可以把它们看作是应用开发中的`<div>`和`<p>`标签。

<block class="androidNote devNotes" />

> 在 Android 上，常见的做法是把视图放入`LinearLayout`, `FrameLayout`或是`RelativeLayout`等布局容器中来定义子元素如何排列。 In React Native, `View` uses Flexbox for its children’s layout. You can learn more in [our guide to layout with Flexbox](flexbox).

<block class="endBlock devNotes" />

这样你就可以在别处通过`<Cat>`来任意引用这个组件了：

```SnackPlayer name=Multiple%20Components
import React from 'react';
import { Text, TextInput, View } from 'react-native';
function Cat() {
  return (
    <View>
      <Text>I am a also cat!</Text>
    </View>
  );
}
export default function Cafe() {
  return (
    <View>
      <Text>Welcome!</Text>
      <Cat />
      <Cat />
      <Cat />
    </View>
  );
}
```

我们把包含着其他组件的组件称为**父组件或父容器**。这里`Cafe`是一个父组件，而每个`Cat`则是**子组件**。

You can put as many cats in your cafe as you like. Each `<Cat>` renders a unique element—which you can customize with props.

## Props 属性

**Props** 是“properties”（属性）的简写。Props 使得我们可以定制组件。.For example, here you pass each `<Cat>` a different `name` for `Cat` to render:

```SnackPlayer name=Multiple%20Props
import React from 'react';
import { Text, View } from 'react-native';
function Cat(props) {
  return (
    <View>
      <Text>Hello, I am {props.name}!</Text>
    </View>
  );
}
export default function Cafe() {
  return (
    <View>
      <Cat name="Maru" />
      <Cat name="Jellylorum" />
      <Cat name="Spot" />
    </View>
  );
}
```

React Native 的绝大多数核心组件都提供了可定制的 props。For example, when using [`Image`](image), you pass it a prop named [`source`](image#source) to define what image it shows:

```SnackPlayer name=Props
import React from 'react';
import { Text, View, Image } from 'react-native';
export default function CatApp() {
  return (
    <View>
      <Image
        source="https://facebook.github.ioassets/p_cat1.png"
        style={{width: 200, height: 200}}
      />
      <Text>Hello, I am your cat!</Text>
    </View>
  );
}
```

`Image` 有[很多不同的 props](image#props)，[`style`](image#style)也是其中之一，它接受对象形式的样式和布局键值对。

> Notice the double curly braces `{{ }}` surrounding `style`‘s width and height. In JSX, JavaScript values are referenced with `{}`. This is handy if you are passing something other than a string as props, like an array or number: `<Cat food={["fish", "kibble"]} /> age={2}`. However, JS objects are **_also_** denoted with curly braces: `{width: 200, height: 200}`. Therefore, to pass a JS object in JSX, you must wrap the object in **another pair** of curly braces: `{{width: 200, height: 200}}` You can build many things with props and the Core Components [`Text`](text), [`Image`](image), and [`View`](view)! But to build something interactive, you’ll need state.

## State 状态

While you can think of props as arguments you use to configure how components render, **state** is like a component’s personal data storage. Sate is useful for handling data that changes over time or that comes from user interaction. State gives your components memory!

> As a general rule, use props to configure a component when it renders. Use state to keep track of any component data that you expect to change over time. The following example takes place in a cat cafe where two hungry cats are waiting to be fed. Their hunger, which we expect to change over time (unlike their names), is stored as state. To feed the cats, press their buttons—which will update their state.

<div class="toggler">
  <ul role="tablist" class="toggle-syntax">
    <li id="functional" class="button-functional" aria-selected="false" role="tab" tabindex="0" aria-controls="functionaltab" onclick="displayTabs('syntax', 'functional')">
      函数组件的状态 State
    </li>
    <li id="classical" class="button-classical" aria-selected="false" role="tab" tabindex="0" aria-controls="classicaltab" onclick="displayTabs('syntax', 'classical')">
      Class 组件的状态 State
    </li>
  </ul>
</div>

<block class="functional syntax" />

You can add state to a component by calling [React’s `useState` Hook](https://zh-hans.reactjs.org/docs/hooks-state.html). A Hook is a kind of function that lets you “hook into” React features. For example, `useState` is a Hook that lets you add state to function components. You can learn more about [other kinds of Hooks in the React documentation.](https://zh-hans.reactjs.org/docs/hooks-intro.html)

```SnackPlayer name=State
import React, { useState } from "react";
import { Button, Text, View } from "react-native";
function Cat(props) {
  const [isHungry, setIsHungry] = useState(true);
  return (
    <View>
      <Text>
        I am {props.name}, and I am {isHungry ? "hungry" : "full"}!
      </Text>
      <Button
        onPress={() => {
          setIsHungry(false);
        }}
        disabled={!isHungry}
        title={isHungry ? "Pour me some milk, please!" : "Thank you!"}
      />
    </View>
  );
}
export default function Cafe() {
  return (
    <>
      <Cat name="Munkustrap" />
      <Cat name="Spot" />
    </>
  );
}
```

首先要从 react 中引入`useState`：

```jsx
import React, { useState } from 'react';
```

然后可以通过在函数内调用`useState`来为组件声明状态。In this example, `useState` creates an `isHungry` state variable:

```jsx
function Cat(props) {
  const [isHungry, setIsHungry] = useState(true);
  // ...
}
```

> 你可以使用`useState`来记录各种类型的数据： strings, numbers, Booleans, arrays, objects. For example, you can track the number of times a cat has been petted with `const [timesPetted, setTimesPetted] = useState(0)`! Calling `useState` does two things:

- it creates a “state variable” with an initial value—in this case the state variable is `isHungry` and its initial value is `true`
- it creates a function to set that state variable’s value—`setIsHungry`

It doesn’t matter what names you use. But it can be handy to think of the pattern as `[<getter>, <setter>] = useState(<initialValue>)`.

Next you add the [`Button`](button) Core Component and give it an `onPress` prop:

```jsx
<Button
  onPress={() => {
    setIsHungry(false);
  }}
  //..
/>
```

现在当用户点击按钮时，`onPress`函数会被触发，从而调用`setIsHungry(false)`。This sets the state variable `isHungry` to `false`. When `isHungry` is false, the `Button`’s `disabled` prop is set to `true` and its `title` also changes:

```jsx
<Button
  //..
  disabled={!isHungry}
  title={isHungry ? 'Pour me some milk, please!' : 'Thank you!'}
/>
```

> 你可能注意到虽然`isHungry`使用了常量关键字[const](https://developer.mozilla.org/Web/JavaScript/Reference/Statements/const)，但它看起来还是可以修改！ What is happening is when a state-setting function like `setIsHungry` is called, its component will re-render. In this case the `Cat` function will run again—and this time, `useState` will give us the next value of `isHungry`. Finally, put your cats inside a `Cafe` component:

```jsx
export default function Cafe() {
  return (
    <>
      <Cat name="Munkustrap" />
      <Cat name="Spot" />
    </>
  );
}
```

<block class="classical syntax" />

老式的 class 组件在使用 state 的写法上有所不同：

```SnackPlayer name=State%20and%20Class%20Components
import React, { Component } from "react";
import { Button, Text, View } from "react-native";
export class Cat extends Component {
  state = { isHungry: true };
  render(props) {
    return (
      <View>
        <Text>
          I am {this.props.name}, and I am
          {this.state.isHungry ? " hungry" : " full"}!
        </Text>
        <Button
          onPress={() => {
            this.setState({ isHungry: false });
          }}
          disabled={!this.state.isHungry}
          title={
            this.state.isHungry ? "Pour me some milk, please!" : "Thank you!"
          }
        />
      </View>
    );
  }
}
export default class Cafe extends Component {
  render() {
    return (
      <>
        <Cat name="Munkustrap" />
        <Cat name="Spot" />
      </>
    );
  }
}
```

再次强调，对于 class 组件始终要记得从 React 中引入`Component`：

```jsx
import React, { Component } from 'react';
```

在 class 组件中， state 以对象的形式存放：

```jsx
export class Cat extends Component {
  state = { isHungry: true };
  //..
}
```

As with accessing props with `this.props`, you access this object inside your component with `this.state`:

```jsx
<Text>
  I am {this.props.name}, and I am
  {this.state.isHungry ? ' hungry' : ' full'}!
</Text>
```

And you set individual values inside the state object by passing an object with the key value pair for state and its new value to `this.setState()`:

```jsx
<Button
  onPress={() => {
    this.setState({ isHungry: false });
  }}
  // ..
</Button>
```

> Do not change your component's state directly by assigning it a new value with `this.state.hunger = false`. Calling `this.setState()` allows React to track changes made to state that trigger rerendering. Setting state directly can break your app's reactivity! When `this.state.isHungry` is false, the `Button`’s `disabled` prop is set to `false` and its `title` also changes:

```jsx
<Button
  // ..
  disabled={!this.state.isHungry}
  title={
    this.state.isHungry
      ? 'Pour me some milk, please!'
      : 'Thank you!'
  }
/>
```

Finally, put your cats inside a `Cafe` component:

```jsx
export default class Cafe extends Component {
  render() {
    return (
      <>
        <Cat name="Munkustrap" />
        <Cat name="Spot" />
      </>
    );
  }
}
```

<block class="endBlock syntax" />

> See the `<>` and `</>` above? These bits of JSX are [fragments](https://zh-hans.reactjs.org/docs/fragments.html). Adjacent JSX elements must be wrapped in an enclosing tag. Fragments let you do that without nesting an extra, unnecessary wrapping element like `View`.

---

Now that you’ve covered both React and React Native’s Core Components, let’s dive deeper on some of these core components by looking at [handling `<TextInput>`](handling-text-input).
