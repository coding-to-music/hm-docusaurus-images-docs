---
id: 5-10-2-auto-generated-class-names
title: 5.10.2 Auto Generated Class Names
date: 2021-04-05 11:11:12
---


Make properties:

```css title="App.css" {13-33}
.App {
  text-align: center;
}

.red {
  color: red;
}

.bold {
  font-weight: bold;
}

.Button {
  background-color: green;
  color: white;
  font: inherit;
  border: 1px solid blue;
  padding: 8px;
  cursor: pointer;
}

.Button:hover {
  background-color: lightgreen;
  color: #333;
}

.Button.Red {
  background-color: red;
}

.Button.Red:hover {
  background-color: salmon;
}
```

```jsx title="App.js" {2,9,28,31,33,36,42,44}
import React, { Component } from "react";
import classes from "./App.css";
import Person from "./Person/Person";

...

  render() {
    let persons = null;
    let btnClass = [classes.Button];

    if (this.state.showPersons) {
      persons = (
        <div>
          {this.state.persons.map((person, index) => {
            return (
              <Person
                click={() => this.deletePersonHandler(index)}
                name={person.name}
                age={person.age}
                key={person.id}
                changed={(event) => this.nameChangedHandler(event, person.id)}
              />
            );
          })}
        </div>
      );

      btnClass.push(classes.Red);
    }

    const assignedClasses = [];
    if (this.state.persons.length <= 2) {
      assignedClasses.push(classes.red); // classes = ['red']
    }
    if (this.state.persons.length <= 1) {
      assignedClasses.push(classes.bold); // classes = ['red', 'bold']
    }

    return (
      <div className={classes.App}>
        <h1>Hi, I'm a React app!</h1>
        <p className={assignedClasses.join(" ")}>This is really working!</p>
        <button
          className={btnClass.join(" ")}
          onClick={this.togglePersonsHandler}
        >
          Toggle Persons
        </button>
        {persons}
      </div>
    );
  }
}

export default App;
```

## How this work

Make a pointer to unique class name, which is generated by the `CSS modules` package:

```jsx
let btnClass = [classes.Button];
```

So because we have an array here, I want to join all the classes that are in there together with a white space in between:

```jsx
 className={btnClass.join(" ")}
```

And now here in this place, where we need to change styles dynamically:

```jsx
btnClass.push(classes.Red);
```

When you run app:

```jsx
btnClass.join(" ") = 'App__Button__2_NDl'
```

When click the button:

```jsx
btnClass.join(" ") = 'App__Button__2_NDl App__Red__2T8IA'
```

This is class name, generated by CSS module package:

```jsx title="Final file" {28}
<style type="text/css">
.App__App__1o-Fp {
  text-align: center;
}

.App__red__lKdi_ {
  color: red;
}

.App__bold__1Ylab {
  font-weight: bold;
}

.App__Button__2_NDl {
  background-color: green;
  color: white;
  font: inherit;
  border: 1px solid blue;
  padding: 8px;
  cursor: pointer;
}

.App__Button__2_NDl:hover {
  background-color: lightgreen;
  color: #333;
}

.App__Button__2_NDl.App__Red__2T8IA {
  background-color: red;
}

.App__Button__2_NDl.App__Red__2T8IA:hover {
  background-color: salmon;
}
</style>
```
