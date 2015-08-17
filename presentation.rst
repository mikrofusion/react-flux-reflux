:title: Flux Reflux React
:data-transition-duration: 1000
:css: css/presentation.css

.. raw:: html

  <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">

----

.. raw:: html

  <div class="github-fork-ribbon-wrapper right">
    <div class="github-fork-ribbon">
      <a href="https://github.com/mikrofusion/react-flux-reflux">Fork me on GitHub</a>
    </div>
  </div>

.. image:: images/react.png
    :height: 200px
    :width: 200px
    :align: right

React
=====

Flux
====

RefluxJS
========

Redux
========

Mike Groseclose (@mikrofusion)

----

Overview
========

* Part I:   Some Theory
* Part II:  React
* Part III: Flux / Reflux / Redux
* Part V:   A Bit Of Code

----

:data-rotate: 100
:data-rotate-y: 100

Part I: Some Theory
===================

----

:data-rotate: 0
:data-rotate-y: 0

Impure functions
================

  * Don’t always return the same result given the same input.

  * Can cause side effects.

----

.. code:: javascript

  var count = 0;
  function increment() {
    return ++count;
  }

----

.. code:: javascript

  function debug(str) {
    console.log(str);
  }

.. raw:: html

  <div class='shrink'>
    Note: writing to disk / file is a side effect.
  </div>

----

Expressions made from impure functions are hard to predict.

Expressions made from impure functions are hard to test.

----

Lack of testing and predictability makes applications:
  * harder to reason about.
  * harder to scale.
  * harder to refactor with confidence.

----

Expressions made from impure functions create fragile applications.

----

Pure functions
==============

  * Will always evaluate to the same result given the same input.
  * Stateless.
  * No side effects.

----

Pure expressions
================

  * Expressions that are constructed from pure functions.
  * Pure functions are referentially transparent.
  * An expression which is referentially transparent can be replaced with its value and have no impact on the system.

----

Referencially transparent functions are like black boxes.

----

Black box development
=====================

  * With black boxes implementation details do not matter.
  * When working with a black box the only concern is inputs and outputs.
  * One black box can be replaced with another black box as long as same data in results in same data out.

----

Referential transparency
========================

  * Simplifies the code making it easier to reason about.
  * Makes testing easier (focus on inputs and outputs)
  * Allows for more confident refactors.
  * Less fragile, more scalable code.

----

.. code:: javascript

  function multiply(x, y) {
    result = 0;
    for(var i = 0; i < y; i++) {
      result += x;
    }
    return result;
  }

----

.. code:: javascript

  function multiply(x, y) {
    return x * y;
  }

----

Event Sourcing Pattern
======================

Rather than storing the current state, store the initial state and the events that lead to the current state.

----

.. code:: javascript

  input: 0

.. raw:: html

  <br>

.. code:: javascript

  event: +3

.. raw:: html

  <br>

.. code:: javascript

  event: -1

.. raw:: html

  <br>

.. code:: javascript

  output: 2

----

:data-rotate: 100
:data-rotate-y: 100

Part II: React
==============

----

A JavaScript library for building user interfaces.

----

:data-rotate: 0
:data-rotate-y: 0

React is only a view component.

React is technology stack agnostic.

----

Why React?
==========

  * React focuses on being simple and declarative

  * React is about building reusable components.

  * Similar to black boxes, React components are extremely encapsulated making code reuse, testing, and separation of concerns easy.

----

In order to be stay encapsulated React uses some unfamiliar conventions.

----

React doesn't use templates
===========================

React combines markup and view logic into a single component.

This creates components which are easier to extend and maintain.

React recommends using JSX to give the markup a familiar syntax.

----

.. code:: javascript

  var Bar = require('./foo');
  var Foo = React.createClass({
    function() {
      return (
        <div>
          <Bar name={this.props.name} />
        </div>
      );
    }
  });

----

:data-y: r3000
:data-rotate: 100
:data-rotate-y: 100

Part III:
=========

Flux / RefluxJS / Redux
=======================

----

:data-y: r0
:data-rotate: 0
:data-rotate-y: 0

What is Flux?
=============

Flux is the application architecture that Facebook uses to build client-side web apps.

----

Flux complements React's composable view components by utilizing a unidirectional data flow.

Flux takes a more functional approach to how data is handled in a web application.

Flux is a pattern, not a framework.

.. raw:: html

  <div class='shrink'>
    * There is no requirement to use a Flux architecture when using React.
  </div>

----

RefluxJS & Redux?
=================

  * RefluxJS and Redux are framework implementations of the Flux architecture.
  * RefluxJS strive to be more Functional Reactive Programming (FRP) friendly and simplify Flux.
  * Redux is completely decoupled from React and has live code editing combined with a time traveling debugger.

----

Flux
====

.. raw:: html

  <div class='container'>
    <br>
    <div class='action'>Action</div>
  </div>

  <div class='container-half'>
    <i class="fa fa-arrow-down"></i>
    <div class='dispatcher'>Dispatcher</div>
  </div>

  <div class='container-half'>
    <i class="fa fa-arrow-down"></i>
    <div class='store'>Store</div>
  </div>

  <div class='container'>
    <i class="fa fa-arrow-down"></i>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <i class="fa fa-arrow-up"></i>
    <div class='view'>View</div>
  </div>

  <div class='container'>
    <i class="fa fa-arrow-down"></i>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <i class="fa fa-arrow-up"></i>
    <div class='user'>User</div>
  </div>
  <span class="footnote"><sup>*</sup> note the unidirectional flow of data</span>

----

:data-z: r1500

  * Actions

    * An object literal containing data and a type property.

  * Dispatcher

    * The dispatcher manages all data flow in Flux (via a registry of callbacks)

  * Stores

    * Stores contain the application state and logic for a particular domain within the application.

  * Views

    * Views listen for changes from the stores and re-render themselves as needed.
    * When using React this is your React component.

----

:data-z: r0

The dispatcher really contains no business logic and is mostly the same between applications using Flux.

It can be argued that the dispatcher is mostly an implementation detail.

----

RefluxJS removes the dispatcher from the flow, by pushing its responsibility into the actions.

----

RefluxJS
========

.. raw:: html

  <div class='container'>
    <br>
    <div class='action'>Action</div>
  </div>

  <div class='container-half'>
    <i class="fa fa-arrow-down"></i>
    <div class='store'>Store</div>
  </div>

  <div class='container'>
    <i class="fa fa-arrow-down"></i>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <i class="fa fa-arrow-up"></i>
    <div class='view'>View</div>
  </div>

  <div class='container'>
    <i class="fa fa-arrow-down"></i>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <i class="fa fa-arrow-up"></i>
    <div class='user'>User</div>
  </div>

----

Redux
=====

Redux uses a single store to store the state of the application.

Redux uses the Event Sourcing Pattern and adds Reducers to mutate the store.

----

Redux Reducers
==============
Pure functions that specify how the application’s state changes in response to an action.

.. code:: javascript

  (previousState, action) => newState

----

Redux
=====

.. raw:: html

  <div class='container'>
    <br>
    <div class='action'>Action</div>
  </div>

  <div class='container-1-3'>
    <i class="fa fa-arrow-down"></i>
    <div class='store'>Store</div>
  </div>

  <div class='container-2-3'>
    <i class="fa fa-arrow-down"></i>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
      &nbsp;&nbsp;&nbsp;
    <i class="fa fa-arrow-down"></i>
    <div class='store'>Reducers</div>
  </div>

  <div class='container'>
    <i class="fa fa-arrow-down"></i>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <i class="fa fa-arrow-up"></i>
    <div class='view'>View</div>
  </div>

  <div class='container'>
    <i class="fa fa-arrow-down"></i>
      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <i class="fa fa-arrow-up"></i>
    <div class='user'>User</div>
  </div>

----

:data-rotate: 100
:data-rotate-y: 100

Part IV: A Bit Of Code
======================

----

:data-rotate: 0
:data-rotate-y: 0

Todo MVC in RefluxJS
====================

Code snippets taken from: https://github.com/spoike/refluxjs-todo

----

Actions
=======

.. code:: javascript

  TodoActions = Reflux.createActions([
        "toggleItem",
        "toggleAllItems",
        "addItem",
        "removeItem",
        "clearCompleted",
        "editItem"
    ]);

----

Stores
======

.. code:: javascript

  Reflux.createStore({
    listenables: [TodoActions], // set up listeners
    onEditItem: function(itemKey, newLabel) {
      ...
    },

    ...

    updateList: function(list){
      // sends the updated list to all listening components
      this.trigger(list);
    },

    ...

  });

----

Components
==========

.. code:: javascript

  var TodoApp = React.createClass({
    // sets state.list when store does trigger(updatedlist)
    mixins: [Reflux.connect(todoListStore,"list")],

    render: function() {
      return (
        <div>
          <TodoHeader />
            <ReactRouter.RouteHandler list={this.state.list} />
          <TodoFooter list={this.state.list} />
        </div>
      );
    }
  });

----

Todo MVC in Redux
=================

Code snippets taken from: https://github.com/rackt/redux/tree/master/examples/todomvc

----

Actions
=======

.. code:: javascript

  export function addTodo(text) {
    return { type: types.ADD_TODO, text };
  }

  export function deleteTodo(id) {
    return { type: types.DELETE_TODO, id };
  }

  ...

----

Reducers
========

.. code:: javascript

  export default function todos(state = initialState, action) {
    switch (action.type) {
    case ADD_TODO:
      return [{
        id: state.length,
        completed: false,
        text: action.text
      }, ...state];

    case DELETE_TODO:
      return state.filter(todo =>
        todo.id !== action.id
      );

    ...

----

Components
==========

.. code:: javascript

  class TodoItem extends Component {
    constructor(props, context) {
      ...
      this.state = { editing: false };
    }

    ...

    render() {
      const {todo, completeTodo, deleteTodo} = this.props;

      ...

      return (
        <li className={classnames({
          completed: todo.completed,
          editing: this.state.editing
        })}>
          {element}
        </li>
      );
    }

----

:data-rotate: 100
:data-rotate-y: 100

Questions?
==========

