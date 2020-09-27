# freeCodeCamp calc 
>  A simple calculator using a state transition table and a fsm 

This project is my solution to the [freeCodeCamp project "Build a JavaScript Calculator"](https://www.freecodecamp.org/learn/front-end-libraries/front-end-libraries-projects/build-a-javascript-calculator) .

The diagram is a representation of the `state machine` that controls the logic, a `state transition table` is used to describe the finite state machine.

The `state transition table`  is a string that is passed as input to two scripts (that I'm currently writing). The scripts  outputs are  an   [`edge list`](https://en.wikipedia.org/wiki/Edge_list) (for Dagre-d3) and  a [machine config object](https://xstate.js.org/docs/guides/machines.html#configuration) (for [Xstate](https://xstate.js.org/docs) ). 


## Diagram

You can: 
* Move the diagram (click-and-drag to pan (translate): click (the diagram, keep pressing) plus  mouse  movements
* Zoom in (spin the wheel to zoom (scale), or use touch): double click (the diagram)
* Zoom out (spin the wheel to zoom (scale): shift plus double click (the diagram)

![Finite state machine graph, calculator ](file:img/fcc-calc-v2-bootstrap-graph.gif)


## [User Stories](https://www.freecodecamp.org/learn/front-end-libraries/front-end-libraries-projects/build-a-javascript-calculator)

User Story #1: My calculator should contain a clickable element containing an = (equal sign) with a corresponding id="equals".

User Story #2: My calculator should contain 10 clickable elements containing one number each from 0-9, with the following corresponding IDs: id="zero", id="one", id="two", id="three", id="four", id="five", id="six", id="seven", id="eight", and id="nine".

User Story #3: My calculator should contain 4 clickable elements each containing one of the 4 primary mathematical operators with the following corresponding IDs: id="add", id="subtract", id="multiply", id="divide".

User Story #4: My calculator should contain a clickable element containing a . (decimal point) symbol with a corresponding id="decimal".

User Story #5: My calculator should contain a clickable element with an id="clear".

User Story #6: My calculator should contain an element to display values with a corresponding id="display".

User Story #7: At any time, pressing the clear button clears the input and output values, and returns the calculator to its initialized state; 0 should be shown in the element with the id of display.

User Story #8: As I input numbers, I should be able to see my input in the element with the id of display.

User Story #9: In any order, I should be able to add, subtract, multiply and divide a chain of numbers of any length, and when I hit =, the correct result should be shown in the element with the id of display.

User Story #10: When inputting numbers, my calculator should not allow a number to begin with multiple zeros.

User Story #11: When the decimal element is clicked, a . should append to the currently displayed value; two . in one number should not be accepted.

User Story #12: I should be able to perform any operation (+, -, *, /) on numbers containing decimal points.

User Story #13: If 2 or more operators are entered consecutively, the operation performed should be the last operator entered (excluding the negative (-) sign). For example, if 5 + * 7 = is entered, the result should be 35 (i.e. 5 * 7); if 5 * - 5 = is entered, the result should be -25 (i.e. 5 x (-5)).

User Story #14: Pressing an operator immediately following = should start a new calculation that operates on the result of the previous evaluation.

User Story #15: My calculator should have several decimal places of precision when it comes to rounding (note that there is no exact standard, but you should be able to handle calculations like 2 / 7 with reasonable precision to at least 4 decimal places).

Note On Calculator Logic: It should be noted that there are two main schools of thought on calculator input logic: immediate execution logic and formula logic. Our example utilizes formula logic and observes order of operation precedence, immediate execution does not. Either is acceptable, but please note that depending on which you choose, your calculator may yield different results than ours for certain equations (see below example). As long as your math can be verified by another production calculator, please do not consider this a bug.

EXAMPLE: 3 + 5 x 6 - 2 / 4 =

    Immediate Execution Logic: 11.5
    Formula/Expression Logic: 32.5


## Comments about the code

In order to avoid "too many arrows" I am using a "type" plus "payload" approach. 

The idea is  use only seven events("types") and use "payload" to specify a value:

- number
- oprtr 
- minus
- zero
- equals
- dot
- ce


``` javascript
 const input = {
    seven:    {type: "number",   payload: 7  },
    eight:    {type: "number",   payload: 8  },
    nine :    {type: "number",   payload: 9  },
    add  :    {type: "oprtr",    payload:"+" },
    multiply: {type: "oprtr",    payload:"X" },
    four:     {type: "number",   payload: 4  },
    five:     {type: "number",   payload: 5  },
    six:      {type: "number",   payload: 6  },
    divide:   {type: "oprtr",    payload:"/" },
    one:      {type: "number",   payload: 1  },
    two:      {type: "number",   payload: 2  },
    three:    {type: "number",   payload: 3  },
    minus:    {type: "minus",    payload:"-" },
    zero :    {type: "zero",     payload: 0  },
    equals:   {type: "equals",   payload: "="},
    dot:      {type: "dot",      payload: "."},
    ce:       {type: "ce",                   }
 };
```

The state transition table (string)  is simple and easy to follow: 
   
   
- The calculator has a local state (context): 

``` javascript
const stateTransitionTable =
`
context:
      data: [ 0 ]
     opnd1: []
     oprtr: []
     opnd2: []

...

`
```

- The state transition table describe:
   - The current state 
   - The input that produce a transition (to the next valid state) 
   - The next state 
   - Side effects (actions/function calls) that will take place


``` javascript
const stateTransitionTable =

`
 *START  number  OPND1  entry: displaydata   :setlastdata     :setopnd1  exit: displaydata
... 
`
```

In the above code we have: 

- Initial state:  START (the initial state is marked with a star)

- Input: number

- Next state: OPND1

- Side effects:
 
  - Entry actions:        displaydata
  - Transition actions:   setlastdata , setopnd1 
  - Exit actions:         displaydata


When the state is entered the `entry` action (displaydata) will be executed, when the input (number) is received the `transition` actions (setlastdata , setopnd1) will be executed. When the state is exited the `exit` action (displaydata) will be executed.




## Demo

[Calculator](https://diegoperezm.github.io/freecodecamp-calc/index.html)

## Licensing

"The code in this project is licensed under MIT license."
