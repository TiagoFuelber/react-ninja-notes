# react-ninja-notes
Notes taken on Fernando Daciuk's React Ninja Course.

[Mindmeister mindmap link](https://www.mindmeister.com/1168818827)

# Forms and inputs

## Controlled components X uncontrolled components
*Controlled component*: A component wich needs to have it's value controlled manually by `setState` and `onChange` props. It needs a variable passed on `value` prop (`checked` if it's checkbox or radio input). Ex.:
```
<input value={myInput} onChange={(e) => this.setState({ myInput: e.target.value })} />
``` 

If the input doesn't have the prop value, it isn't a controlled component and React will handle it's value.

* Give preference to controlled components.

## prop `defaultValue`, `defaultChecked` (radio inputs)
It gives a default value to an uncontrolled component

