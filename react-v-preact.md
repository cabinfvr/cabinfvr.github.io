# ⚛️ React vs Preact | What's the difference?

Let's start off with some differences, shall we?

The first difference you might notice is that Preact actually passes `this.props` and `this.state` to `render()` for us. 
Although, you can still reference them manaully when you [deconstruct](https://2ality.com/2015/01/es6-destructuring.html) them.

Props in React:
```js
const expression = 'Happy';
<Greeting statement='Hello' expression={expression}/>

class Greeting extends Component {
  render() {
    return <h1>{this.props.statement} I am feeling {this.props.expression} today!</h1>;
  }
}
```
Props in Preact:
```js
const expression = 'Happy';
<Greeting statement='Hello' expression={expression}/>

function Gretting(props){
 return <h1>{props.statement} I am feeling {props.expression} today!</h1>
}
```

Preact doesn't use `className`, instead it uses `class` as in standard HTML applications. It's still supported, but it's easier to write.
React `className`:
```js
export default function(){
  return (
    <div className="hello">
      <h1> You are viewing an example of the React className feature. </h1>
    </div>
  );
}
```
Preact `class`:
```js
export default function() {
  return (
    <div class="hello">
      <h1> You are viewing an example of the Preact class feature.</h1>
    </div>
  );
}
```
---
## What's missing? 🔎

[`PropType`](https://github.com/developit/proptypes) validiation is missing, because not everyone uses it, so it's not part of Preact's core.
Although, they are supported in [Preact Compat](https://github.com/preactjs/preact-compat), or you can acces them manually.

[Children](https://reactjs.org/docs/react-api.html#reactchildren) are also missing. This is because as it stands, `React.Children` is essential useless, as `props.children` is always an array.

Synthetic Events are disabled because Preact's browser support does not require this. 
It's native browser uses `addEventListener` for event handling. See [`GlobalEventHandlers`](https://docs.w3cub.com/dom/globaleventhandlers) for a full list of DOM event handlers.

---
## What's different? 💼

The only two differences are:
- `render()` *does* accept a third argument, which is the root node, to replace or append.
- Also, components do not use `contextTypes` or `childContextTypes`. The entries here can be drawn from `getChildContext()`.

---
**Have a issue with this page? You can view the source code [here](https://carbon.now.sh/a4930d3c9ec45c0bd1d5b7d1f7e31c33) and can make a comment about it.**
