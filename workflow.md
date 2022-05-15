# Workflow Basic Structure
Filename format: `"short-desc.workflow.pu"`
```pu
@startuml
title short desc
start
'some codes here...
end
@enduml
```
# Workflow Control
## Basics
### Reserve Expression or States
- `currentFlow` 

    is an object use to prevent multiple instance of workflow
- `return`

    used to store resulting value (state) of the workflow. 
- `defined` 

    is used to determine whether a state is defined or not 
- `null` 

    is used to set a state to null or determine whether a state is null or not
- `or` 

    an operator in conditional expression  
- `and`

    an operator in conditional expression  
- `not`

    an operator in conditional expression  
- `of`

    used to access member of an object state
- `is`

    used to compare two information (states or constants) 
- `greater than`

    a conditional operator
- `less than`

    a conditional operator
- `splitResult`
- `forkResult`
### Comments
```pu
'this is a comment

/'This is 
multi-line comments'/
```
### If/ElseIf/Else statement
```pu
if (condition) then
    :execute some action task;
elseif (otherCondition) then
    :execute some action UI task;
endif
```
### Declaring/Setting States
```pu
'using set statement
:set someState = expression; 

'using UI task
:someState = execute some action UI task;
'shorthand with UI task
#UI:someState = some action;

'using service task
:someState = execute some action task;
'shorthand with service task
:someState = some action;

'store as local state with ";" semicolon
:set someState = expression;

'store as module (Owner Module) state with "|"
:set someState = expression|

'store as module (Owner Module or Anscestor) state with "]"
:set someState = expression]
```
### Access (first, second, third) arguments 
```pu
@startuml
title some work
start
:someState = first argument;
:anotherState = second argument;
:someOtherState = third argument;
'some code here
stop
@enduml
```
### Passing Parameter to Task or Workflows using Note
```pu
'single param
:execute some task;
note: state

'multi or name params
:execute some task;
note left
    param1 : "some value"
    param2 : someState
end note 

:execute some task;
note right
    paramDesc : "some value"
end note 

'With literal JSON 
:execute some task;
note left
    param1 : {
        prop1: state,
        prop2: "some"
    }
    pram2 : "string"
endnote
```

### Singleton Workflow Management
```pu
@startuml
title some work
    start
    if (someWork is defined) then
        :set return = promise of someWork;
        stop;
    endif
    :set someWork = currentFlow|
    
    'some code here...

    :unset someWork;
    stop
@enduml
```
## Loopings
### while statement
```pu
while (condition)
    'some codes here....
endwhile
```
### repeat while statement
```pu
repeat
    'some code here..
repeat while(condition)
```
## Multi-Tasking
### Split Statement
```pu
split
    'first task here...
    /'return of last executing activity
     is the result of the branch'/
split again
    'another task here...
    /'return of last executing activity
     is the result of the branch'/
endsplit
:set result = splitResult;'value of winning branch
'will not proceed if exeception has occured
```
### Fork Statement
```pu
fork
    'first task here..
    /'return of last executing activity
     is the result of the branch'/
fork again
    'another task here
    /'return of last executing activity
     is the result of the branch'/
endfork
:set result = forkResult; 'Array or results
'will not proceed if exeception has occured
```
# Activity Statements
## Set Statement
Format:

`:set {target state} = {exression}(;|])`

Example:
```pu
:set localState = expression;
:set moduleState = expression|
:set ancestorOrOwnerState = expression]
```

## Unset Statement
Format:

`:unset {target state};`

Example:
```pu
:unset someState;
```
Will try to unset local state first, module, then ancestors.
## Activate/Run Module
Format:

`:{?state = }run {module name} module(;|])`

Examples:
```pu
:run some module;
:someState = run some module;
:someState = run some module|
:someState = run some module]
```
## Execute Service Task
Format:

`:{?state = }execute {task name} task(;|])`

Shorthand: 
`:{?state = }{task name}(;|])`

Examples:
```pu
:execute some task;
:someState = execcute some task;
:someState = execcute some task|
:someState = execcute some task]

'short-hand
:someState = some;
```

## Execute UI Task
Format:

`:{?state = }execute {task name} UI task(;|])`

Shorthand: 
`#UI:{?state = }{task name}(;|])`

Examples:
```pu
:execute some task;
:someState = execcute some UI task;
:someState = execcute some UI task|
:someState = execcute some UI task]

'short-hand
#UI:someState = some;
```

## Execute Workflow
Format:

`:{target state} = execute {workflow name} workflow {?of ownerModule}(;|])`

Examples:
```pu
:execute some workflow;
:execute some workflow of someModule;
:someState = execcute some workflow;
:someState = execcute some workflow|
:someState = execcute some workflow]
```

## Debug/Breakpoint Statement
Format:

`:debugger;`

## Not Recommended to Use
### Execute Controller Method
Format: 

`:invoke {method expression}(;|])`
### Fire Module Event
Format: 

`:{event name}<`
### Pause Workflow from Running
Format: 

`:pause {expression};`
### Resume Workflow in Running
Format: 

`:resume {expression};`



