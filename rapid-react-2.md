# Rapid React: Step 2 - Introduction to Components

_This page is part of a <a href="https://link.lavell.xyz/rapid-react" target="_blank">Step-by-Step Tutorial</a> 
to build a <a href="http://trello.com/" target="_blank">Trello</a> clone in <a href="http://reactjs.org/" target="_blank">React</a>._

<a href="https://link.lavell.xyz/rapid-react-demo" target="_blank">![Screenshot](images/demo.png)</a>

<a href="https://link.lavell.xyz/rapid-react-demo" target="_blank">_Click here to run the Demo of the Complete Prototype_</a>

## Pre-Requisites

Make sure you've completed <a href="https://link.lavell.xyz/rapid-react-1" target="_blank">Step 1</a>, which will explain how the development environments work, and help you brush up on Javascript / web technologies.

## Follow Along in Code

<a href="https://link.lavell.xyz/rapid-react-dev-2" target="_blank">Step 2 Development Environment</a>

## What is a Component?

When designing a program, it is helpful to break it down into modular units that fit
together to make a greater whole. This is true not just in UIs, but across the 
range of types of things a program might try to model. React's focus on components makes this concept easy to put into practice. 

## Breaking Trello into Components

Let's start at the conceptual level. We can analyze Trello and break 
it down into a set of components:

* **Cards**, which contain the text for tasks

![Card](images/card.png)

* **Lists**, which contain sequences of Cards

![List](images/list.png)
* **Boards**, which contain sequences of Lists

![Board](images/small-trello.png)
  
Simple structure, right? Trello has even
more concepts, like **Users**, **Organizations**, and **Powerups** for
example - but we are only going to focus on core components. This is
a prototype, not a full-fledged product!

## Creating Components in React

To define a React Component, you need:

* A set of parameters that get passed to the component, called **props**
* A **render** method which tells React how to draw the component

Components can be defined as **classes** or **functions**. For now, we are
going to define our components as functions, as that is the simplest possible
form!

### Card.js

If you haven't already, open up the <a href="https://link.lavell.xyz/rapid-react-dev-2" target="_blank">Development Environment</a>. Mouse
over the _Files_ pane on the left-hand side, and click _New File_. Name
it **Card.js**, and type in the following code: 

```javascript
import React from 'react';

function Card(props) {
  return (
    <div className="Card"> 
      {props.title}
    </div>
  );
}

export default Card;
```

### App.js

Now, go to **App.js**, and add the following line at the top of the file,
after the other imports:

```javascript
import Card from './Card.js';
```

In the main ```App()``` function, in the ```<div>``` tag, add the following:

```javascript
<Card title="Learn to code" />
<Card title="Do a flip" />
<Card title="Go outside" />
```

You should see the app auto-reload on the right side of the screen,
displaying each of your cards in order, without any fancy formatting -
just text!

Here's the full **App.js**:

```javascript
import React from 'react';
import './App.css';
import Card from './Card.js';

function App() {
  return (
    <div className="App">
      <Card title="Learn to code" />
      <Card title="Do a flip" />
      <Card title="Go outside" />
    </div>
  );
}

export default App;
```

You've just created the basis of a data model for your app. Good work!
Might not look like much, but there's a lot of flexibility and future
potential in this little island of code. 

### Checkpoint

![app](images/app-2-1.png)

Your code should now match this: <a href="https://link.lavell.xyz/rapid-react-dev-2-1" target="_blank">Step 2 - Checkpoint 1</a>

_Feel free to just open from this checkpoint if you're having issues
getting the code running and don't want to get stuck debugging right now._

## Line-by-Line

Okay, so what did we just _do_, exactly? Let's go through line-by-line.

### Card.js

```javascript
import React from 'react';
```

This line may be somewhat puzzling at first. Why do we need to import **React** when 
we don't actually reference it anywhere else in the file?

Let's look at the Card function itself:

```javascript
function Card(props) {
  return (
    <div className="Card"> 
      {props.title}
    </div>
  );
}
```

Notice anything _weird_ about this **Javascript** function? 

If you've brushed up on your HTML/CSS/JS, you might notice that this
function is mixing _Javascript_ syntax with _HTML_ syntax! What's going on here?

### JSX

This file isn't being interpreted as _just_ plain-old Javascript - it's 
actually an extension to Javascript, called [JSX](https://reactjs.org/docs/introducing-jsx.html) - which mashes up the concept
of HTML templating with Javascript. The fundamental thought here is that 
rendering logic is inherently coupled (i.e. _intertwined_) with other UI logic.
Rather than separating the rendering logic into a separate file, [like some 
other frameworks do with HTML templates](), everything is contained in one
place.

### Babel

Under the hood, React is using something called [Babel](https://babeljs.io/) to
_pre-compile_ the Javascript. Ultimately all of the JSX syntax gets turned into
normal Javascript functions ([React.createElement](https://reactjs.org/docs/react-api.html#createelement), specifically), but you don't
need to worry about that process too much at this point. It's good just to know 
that it exists, and how to use JSX.

### Defining Props

As mentioned earlier, all you need to define a React Component is some **properties**
and a **rendering function**. 

```javascript
function Card(props) {
```

The Card function takes in its props as an argument. 

```javascript
  return (
    <div className="Card"> 
      {props.title}
    </div>
  );
```

It then references the **title**, which it assumes has been passed in on the 
**props** object. The curly braces around **props.title** turn it into a JSX
expression, which outputs the value into the rendered HTML. Without the braces,
all of the cards would just say _props.title_, rather than the actual text 
passed into the function!

![app broken](images/app-2-1-broken.png)

### Passing Props

So, our **Card** component knows how to render itself when passed in a **props**
object with a title property. But where is that done, exactly?


The App.js file imports the **Card** component from its own respective file:

```javascript
// App.js
import Card from './Card.js';
```

We also require the Card.js file to *export* it's Card function:

```javascript
// Card.js
export default Card;
```

Without that line, we will run into errors.

From there, it uses JSX syntax to create a handful of cards.

```javascript
function App() {
  return (
    <div className="App">
      <Card title="Learn to code" />
      <Card title="Do a flip" />
      <Card title="Go outside" />
    </div>
  );
}
```

Let's look more closely at a Card-creating line:

```html
<Card title="Learn to code" />
```

This JSX creates a Card component, and passes the **title** string to it.
This is what's referenced by the **props** in the Card function. Simple enough!
We will cover more complicated property passing in later Tutorial Steps.

### Where is the App Itself Created?

You'll notice a pair of files, **index.html** and **index.js**.

**index.html** is simple:

```html
<div id="root"></div>
```

**index.js** is slightly more complicated:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));
```

The basic context is that the html is as simple as possible, and 
just contains a unique ```<div>``` element called ```root```, which
the **index.js** file _injects_ React into (by creating an instance
of the **App**).

You won't need to modify this section, but it's good to understand the
basics of the plumbing!

## All Set!

Good work! This step was fundamental to your understanding of React.
We covered a lot of ground. Take a break, and when you're ready, head
on over to <a href="https://link.lavell.xyz/rapid-react-3" target="_blank">Step 3</a>, where we'll start styling things and making our
little prototype look more like Trello!