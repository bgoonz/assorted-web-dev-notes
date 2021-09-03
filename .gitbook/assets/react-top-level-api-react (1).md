`React` is the entry point to the React library. If you load React from a `<script>` tag, these top-level APIs are available on the `React` global. If you use ES6 with npm, you can write `import React from 'react'`. If you use ES5 with npm, you can write `var React = require('react')`.

## [](https://reactjs.org/docs/react-api.html#overview)Overview

### [](https://reactjs.org/docs/react-api.html#components)Components

React components let you split the UI into independent, reusable pieces, and think about each piece in isolation. React components can be defined by subclassing `React.Component` or `React.PureComponent`.

-   [`React.Component`](https://reactjs.org/docs/react-api.html#reactcomponent)
-   [`React.PureComponent`](https://reactjs.org/docs/react-api.html#reactpurecomponent)

If you don’t use ES6 classes, you may use the `create-react-class` module instead. See [Using React without ES6](https://reactjs.org/docs/react-without-es6.html) for more information.

React components can also be defined as functions which can be wrapped:

-   [`React.memo`](https://reactjs.org/docs/react-api.html#reactmemo)

### [](https://reactjs.org/docs/react-api.html#creating-react-elements)Creating React Elements

We recommend [using JSX](https://reactjs.org/docs/introducing-jsx.html) to describe what your UI should look like. Each JSX element is just syntactic sugar for calling [`React.createElement()`](https://reactjs.org/docs/react-api.html#createelement). You will not typically invoke the following methods directly if you are using JSX.

-   [`createElement()`](https://reactjs.org/docs/react-api.html#createelement)
-   [`createFactory()`](https://reactjs.org/docs/react-api.html#createfactory)

See [Using React without JSX](https://reactjs.org/docs/react-without-jsx.html) for more information.

### [](https://reactjs.org/docs/react-api.html#transforming-elements)Transforming Elements

`React` provides several APIs for manipulating elements:

-   [`cloneElement()`](https://reactjs.org/docs/react-api.html#cloneelement)
-   [`isValidElement()`](https://reactjs.org/docs/react-api.html#isvalidelement)
-   [`React.Children`](https://reactjs.org/docs/react-api.html#reactchildren)

### [](https://reactjs.org/docs/react-api.html#fragments)Fragments

`React` also provides a component for rendering multiple elements without a wrapper.

-   [`React.Fragment`](https://reactjs.org/docs/react-api.html#reactfragment)

### [](https://reactjs.org/docs/react-api.html#refs)Refs

-   [`React.createRef`](https://reactjs.org/docs/react-api.html#reactcreateref)
-   [`React.forwardRef`](https://reactjs.org/docs/react-api.html#reactforwardref)

### [](https://reactjs.org/docs/react-api.html#suspense)Suspense

Suspense lets components “wait” for something before rendering. Today, Suspense only supports one use case: [loading components dynamically with `React.lazy`](https://reactjs.org/docs/code-splitting.html#reactlazy). In the future, it will support other use cases like data fetching.

-   [`React.lazy`](https://reactjs.org/docs/react-api.html#reactlazy)
-   [`React.Suspense`](https://reactjs.org/docs/react-api.html#reactsuspense)

### [](https://reactjs.org/docs/react-api.html#hooks)Hooks

_Hooks_ are a new addition in React 16.8. They let you use state and other React features without writing a class. Hooks have a [dedicated docs section](https://reactjs.org/docs/hooks-intro.html) and a separate API reference:

-   [Basic Hooks](https://reactjs.org/docs/hooks-reference.html#basic-hooks)
    
    -   [`useState`](https://reactjs.org/docs/hooks-reference.html#usestate)
    -   [`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect)
    -   [`useContext`](https://reactjs.org/docs/hooks-reference.html#usecontext)
-   [Additional Hooks](https://reactjs.org/docs/hooks-reference.html#additional-hooks)
    
    -   [`useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer)
    -   [`useCallback`](https://reactjs.org/docs/hooks-reference.html#usecallback)
    -   [`useMemo`](https://reactjs.org/docs/hooks-reference.html#usememo)
    -   [`useRef`](https://reactjs.org/docs/hooks-reference.html#useref)
    -   [`useImperativeHandle`](https://reactjs.org/docs/hooks-reference.html#useimperativehandle)
    -   [`useLayoutEffect`](https://reactjs.org/docs/hooks-reference.html#uselayouteffect)
    -   [`useDebugValue`](https://reactjs.org/docs/hooks-reference.html#usedebugvalue)

___

## [](https://reactjs.org/docs/react-api.html#reference)Reference

### [](https://reactjs.org/docs/react-api.html#reactcomponent)`React.Component`

`React.Component` is the base class for React components when they are defined using [ES6 classes](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes):

```
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

See the [React.Component API Reference](https://reactjs.org/docs/react-component.html) for a list of methods and properties related to the base `React.Component` class.

___

### [](https://reactjs.org/docs/react-api.html#reactpurecomponent)`React.PureComponent`

`React.PureComponent` is similar to [`React.Component`](https://reactjs.org/docs/react-api.html#reactcomponent). The difference between them is that [`React.Component`](https://reactjs.org/docs/react-api.html#reactcomponent) doesn’t implement [`shouldComponentUpdate()`](https://reactjs.org/docs/react-component.html#shouldcomponentupdate), but `React.PureComponent` implements it with a shallow prop and state comparison.

If your React component’s `render()` function renders the same result given the same props and state, you can use `React.PureComponent` for a performance boost in some cases.

> Note
> 
> `React.PureComponent`’s `shouldComponentUpdate()` only shallowly compares the objects. If these contain complex data structures, it may produce false-negatives for deeper differences. Only extend `PureComponent` when you expect to have simple props and state, or use [`forceUpdate()`](https://reactjs.org/docs/react-component.html#forceupdate) when you know deep data structures have changed. Or, consider using [immutable objects](https://facebook.github.io/immutable-js/) to facilitate fast comparisons of nested data.
> 
> Furthermore, `React.PureComponent`’s `shouldComponentUpdate()` skips prop updates for the whole component subtree. Make sure all the children components are also “pure”.

___

### [](https://reactjs.org/docs/react-api.html#reactmemo)`React.memo`

```
const MyComponent = React.memo(function MyComponent(props) {
  
});
```

`React.memo` is a [higher order component](https://reactjs.org/docs/higher-order-components.html).

If your component renders the same result given the same props, you can wrap it in a call to `React.memo` for a performance boost in some cases by memoizing the result. This means that React will skip rendering the component, and reuse the last rendered result.

`React.memo` only checks for prop changes. If your function component wrapped in `React.memo` has a [`useState`](https://reactjs.org/docs/hooks-state.html), [`useReducer`](https://reactjs.org/docs/hooks-reference.html#usereducer) or [`useContext`](https://reactjs.org/docs/hooks-reference.html#usecontext) Hook in its implementation, it will still rerender when state or context change.

By default it will only shallowly compare complex objects in the props object. If you want control over the comparison, you can also provide a custom comparison function as the second argument.

```
function MyComponent(props) {
  
}
function areEqual(prevProps, nextProps) {
  
}
export default React.memo(MyComponent, areEqual);
```

This method only exists as a **[performance optimization](https://reactjs.org/docs/optimizing-performance.html).** Do not rely on it to “prevent” a render, as this can lead to bugs.

> Note
> 
> Unlike the [`shouldComponentUpdate()`](https://reactjs.org/docs/react-component.html#shouldcomponentupdate) method on class components, the `areEqual` function returns `true` if the props are equal and `false` if the props are not equal. This is the inverse from `shouldComponentUpdate`.

___

### [](https://reactjs.org/docs/react-api.html#createelement)`createElement()`

```
React.createElement(
  type,
  [props],
  [...children]
)
```

Create and return a new [React element](https://reactjs.org/docs/rendering-elements.html) of the given type. The type argument can be either a tag name string (such as `'div'` or `'span'`), a [React component](https://reactjs.org/docs/components-and-props.html) type (a class or a function), or a [React fragment](https://reactjs.org/docs/react-api.html#reactfragment) type.

Code written with [JSX](https://reactjs.org/docs/introducing-jsx.html) will be converted to use `React.createElement()`. You will not typically invoke `React.createElement()` directly if you are using JSX. See [React Without JSX](https://reactjs.org/docs/react-without-jsx.html) to learn more.

___

### [](https://reactjs.org/docs/react-api.html#cloneelement)`cloneElement()`

```
React.cloneElement(
  element,
  [props],
  [...children]
)
```

Clone and return a new React element using `element` as the starting point. The resulting element will have the original element’s props with the new props merged in shallowly. New children will replace existing children. `key` and `ref` from the original element will be preserved.

`React.cloneElement()` is almost equivalent to:

```
<element.type {...element.props} {...props}>{children}</element.type>
```

However, it also preserves `ref`s. This means that if you get a child with a `ref` on it, you won’t accidentally steal it from your ancestor. You will get the same `ref` attached to your new element.

This API was introduced as a replacement of the deprecated `React.addons.cloneWithProps()`.

___

### [](https://reactjs.org/docs/react-api.html#createfactory)`createFactory()`

```
React.createFactory(type)
```

Return a function that produces React elements of a given type. Like [`React.createElement()`](https://reactjs.org/docs/react-api.html#createelement), the type argument can be either a tag name string (such as `'div'` or `'span'`), a [React component](https://reactjs.org/docs/components-and-props.html) type (a class or a function), or a [React fragment](https://reactjs.org/docs/react-api.html#reactfragment) type.

This helper is considered legacy, and we encourage you to either use JSX or use `React.createElement()` directly instead.

You will not typically invoke `React.createFactory()` directly if you are using JSX. See [React Without JSX](https://reactjs.org/docs/react-without-jsx.html) to learn more.

___

### [](https://reactjs.org/docs/react-api.html#isvalidelement)`isValidElement()`

```
React.isValidElement(object)
```

Verifies the object is a React element. Returns `true` or `false`.

___

### [](https://reactjs.org/docs/react-api.html#reactchildren)`React.Children`

`React.Children` provides utilities for dealing with the `this.props.children` opaque data structure.

#### [](https://reactjs.org/docs/react-api.html#reactchildrenmap)`React.Children.map`

```
React.Children.map(children, function[(thisArg)])
```

Invokes a function on every immediate child contained within `children` with `this` set to `thisArg`. If `children` is an array it will be traversed and the function will be called for each child in the array. If children is `null` or `undefined`, this method will return `null` or `undefined` rather than an array.

> Note
> 
> If `children` is a `Fragment` it will be treated as a single child and not traversed.

#### [](https://reactjs.org/docs/react-api.html#reactchildrenforeach)`React.Children.forEach`

```
React.Children.forEach(children, function[(thisArg)])
```

Like [`React.Children.map()`](https://reactjs.org/docs/react-api.html#reactchildrenmap) but does not return an array.

#### [](https://reactjs.org/docs/react-api.html#reactchildrencount)`React.Children.count`

```
React.Children.count(children)
```

Returns the total number of components in `children`, equal to the number of times that a callback passed to `map` or `forEach` would be invoked.

#### [](https://reactjs.org/docs/react-api.html#reactchildrenonly)`React.Children.only`

```
React.Children.only(children)
```

Verifies that `children` has only one child (a React element) and returns it. Otherwise this method throws an error.

> Note:
> 
> `React.Children.only()` does not accept the return value of [`React.Children.map()`](https://reactjs.org/docs/react-api.html#reactchildrenmap) because it is an array rather than a React element.

#### [](https://reactjs.org/docs/react-api.html#reactchildrentoarray)`React.Children.toArray`

```
React.Children.toArray(children)
```

Returns the `children` opaque data structure as a flat array with keys assigned to each child. Useful if you want to manipulate collections of children in your render methods, especially if you want to reorder or slice `this.props.children` before passing it down.

> Note:
> 
> `React.Children.toArray()` changes keys to preserve the semantics of nested arrays when flattening lists of children. That is, `toArray` prefixes each key in the returned array so that each element’s key is scoped to the input array containing it.

___

### [](https://reactjs.org/docs/react-api.html#reactfragment)`React.Fragment`

The `React.Fragment` component lets you return multiple elements in a `render()` method without creating an additional DOM element:

```
render() {
  return (
    <React.Fragment>
      Some text.
      <h2>A heading</h2>
    </React.Fragment>
  );
}
```

You can also use it with the shorthand `<></>` syntax. For more information, see [React v16.2.0: Improved Support for Fragments](https://reactjs.org/blog/2017/11/28/react-v16.2.0-fragment-support.html).

### [](https://reactjs.org/docs/react-api.html#reactcreateref)`React.createRef`

`React.createRef` creates a [ref](https://reactjs.org/docs/refs-and-the-dom.html) that can be attached to React elements via the ref attribute.

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.inputRef = React.createRef();  }

  render() {
    return <input type="text" ref={this.inputRef} />;  }

  componentDidMount() {
    this.inputRef.current.focus();  }
}
```

### [](https://reactjs.org/docs/react-api.html#reactforwardref)`React.forwardRef`

`React.forwardRef` creates a React component that forwards the [ref](https://reactjs.org/docs/refs-and-the-dom.html) attribute it receives to another component below in the tree. This technique is not very common but is particularly useful in two scenarios:

-   [Forwarding refs to DOM components](https://reactjs.org/docs/forwarding-refs.html#forwarding-refs-to-dom-components)
-   [Forwarding refs in higher-order-components](https://reactjs.org/docs/forwarding-refs.html#forwarding-refs-in-higher-order-components)

`React.forwardRef` accepts a rendering function as an argument. React will call this function with `props` and `ref` as two arguments. This function should return a React node.

```
const FancyButton = React.forwardRef((props, ref) => (  <button ref={ref} className="FancyButton">    {props.children}
  </button>
));


const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

In the above example, React passes a `ref` given to `<FancyButton ref={ref}>` element as a second argument to the rendering function inside the `React.forwardRef` call. This rendering function passes the `ref` to the `<button ref={ref}>` element.

As a result, after React attaches the ref, `ref.current` will point directly to the `<button>` DOM element instance.

For more information, see [forwarding refs](https://reactjs.org/docs/forwarding-refs.html).

### [](https://reactjs.org/docs/react-api.html#reactlazy)`React.lazy`

`React.lazy()` lets you define a component that is loaded dynamically. This helps reduce the bundle size to delay loading components that aren’t used during the initial render.

You can learn how to use it from our [code splitting documentation](https://reactjs.org/docs/code-splitting.html#reactlazy). You might also want to check out [this article](https://medium.com/@pomber/lazy-loading-and-preloading-components-in-react-16-6-804de091c82d) explaining how to use it in more detail.

```

const SomeComponent = React.lazy(() => import('./SomeComponent'));
```

Note that rendering `lazy` components requires that there’s a `<React.Suspense>` component higher in the rendering tree. This is how you specify a loading indicator.

> **Note**
> 
> Using `React.lazy`with dynamic import requires Promises to be available in the JS environment. This requires a polyfill on IE11 and below.

### [](https://reactjs.org/docs/react-api.html#reactsuspense)`React.Suspense`

`React.Suspense` lets you specify the loading indicator in case some components in the tree below it are not yet ready to render. Today, lazy loading components is the **only** use case supported by `<React.Suspense>`:

```

const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    
    <React.Suspense fallback={<Spinner />}>
      <div>
        <OtherComponent />
      </div>
    </React.Suspense>
  );
}
```

It is documented in our [code splitting guide](https://reactjs.org/docs/code-splitting.html#reactlazy). Note that `lazy` components can be deep inside the `Suspense` tree — it doesn’t have to wrap every one of them. The best practice is to place `<Suspense>` where you want to see a loading indicator, but to use `lazy()` wherever you want to do code splitting.

While this is not supported today, in the future we plan to let `Suspense` handle more scenarios such as data fetching. You can read about this in [our roadmap](https://reactjs.org/blog/2018/11/27/react-16-roadmap.html).

> Note:
> 
> `React.lazy()` and `<React.Suspense>` are not yet supported by `ReactDOMServer`. This is a known limitation that will be resolved in the future.