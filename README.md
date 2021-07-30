English | [中文](README_zh.md) 




# NOTE

React-context-mutation is a lighter and more convenient state manager designed for react applications. It aims to replace the Redux in react applications and solve the problems of too large Redux and difficult state maintenance and management in the project.




# Install

```
npm install react-context-mutation
```




# Usage

```js
// App.js
import reactContextMutation from "react-context-mutation"
const { AppConsumer, AppProvider } = reactContextMutation

// Header
function Header(props) {
  const { ctx } = props
  const { mutation, context, useActions } = ctx

  handleButtonClick() {
    mutation.setTitle("哈哈")
  }

  return (
    <>
      <header>
        {ctx.context.title}
      </header>
      <button onClick={handleButtonClick}>点我设置标题为“哈哈”</button>
    </>
  )
}

// provider
<AppProvider>
// consumer
  <AppConsumer>
    {(ctx) => {
      // ctx contain context mutation useActions
      return (
        <Header ctx={ctx}></Header>
      )
    }}
  </AppConsumer>
</AppProvider>
```




# AppProvider
The provider receives a config attribute and passes it to the consumer component. A provider can have corresponding relationships with multiple consumer components. Multiple providers can also be nested, and the data in the inner layer will cover the data in the outer layer.

```
<AppProvider config={/* 某个值 */}>...</AppProvider>
```




# AppConsumer
The consumer component can subscribe to the change of context. This component allows you to subscribe to context in functional components.


```
<AppConsumer>
  {value => /* 基于 context 值进行渲染*/}
</.AppConsumer>
```




# Context
Context provides a way to share such values among components without explicitly passing props layer by layer through the component tree, in order to share the data that is "global" to a component tree.
```
<AppConsumer>
  {(ctx) => {
    // ctx contain context mutation useActions
    return (
      <Header ctx={ctx}></Header>
    )
  }}
</AppConsumer>

function Header(props) {
  const { ctx } = props
  const { context } = ctx

  return (
    <header>
      {context.title}
    </header>
  )
}

```




# Mutation
Mutation is used to update the status of components.
```
const { mutation } = ctx
mutation([type](newState))
```




# useActions
Useactions is used to obtain the changes of update status in functional components.
```
const { useActions } = ctx
const action = useAction()
```


