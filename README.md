# React Ninja Notes
Notes taken on Fernando Daciuk's React Ninja Course.

[Mindmeister mindmap link](https://www.mindmeister.com/1168818827)

# Forms and inputs

## Controlled components X uncontrolled components
*Controlled component*: A component wich needs to have it's value controlled manually by `setState` and `onChange` props. It needs a variable passed on `value` prop (`checked` if it's checkbox or radio input). Ex.:
```
<input value={myInput} onChange={(e) => this.setState({ myInput: e.target.value })} />
``` 

If the input doesn't have the prop value, it isn't a controlled component and React will handle it's value.

* Always give preference to controlled components.

## Prop `defaultValue`, `defaultChecked` (radio inputs)
* It gives a default value to an uncontrolled component

## Native `<input />`
* Behaves like React components that renders native inputs.

## `<select></select>`
* The `value` and `defaultValue` props will set the default value of the component.
* The `multiple` prop enable the select to have multiple options selected at once.

## `<textarea />`
* Use `value` and `defaultValue` to set the content instead of using children. Using children content is an anti-pattern.

## `<form></form>`
* The `onChange` prop watches all form inputs.

# Webpack
* [webpack-dashboard](https://github.com/FormidableLabs/webpack-dashboard). A CLI dashboard for webpack. 

# Performance - Critical Rendering Path
* Create variables with the styles
```webpack.config
var criticalrenderingPath = new ExtractTextPlugin('critical-rendering-path.css');
var styles = new ExtractTextPlugin('[name]-[hash].css');
```

* Add the variables to the `plugins` property:
```webpack.config
module.exports = {
  plugins: [
    criticalrenderingPath,
    styles
  ]
}
```

* Set the css loader
```webpack.config
module.exports = {
  loaders: [{
    test: /\.css$/;
    // search and style are the files we want to render inline
    exclude: /node_modules|(search|style)\.css/,
    include: /src/,
    loader: styles.extract('style', 'css')
  }, {
    test: /(search|style)\.css/;
    exclude: /node_modules/;
    include: /src/;
    loader: criticalRenderingPath.extract('style', 'css')
  }]
}
```

*  Insert the style inline on the `<head>` on the html using html-webpack-plugin and extract-text-plugin
```template.html
<head>
  <style>
    <%= compilation.assets['critical-rendering-path.css'].source() %>
  </style>
  <body>
    <% htmlWebpackPlugin.files.js.forEach((jsFile) => { %>
      <script async src="<%= jsFile %>"></script
    <% }) %>
    <% htmlWebpackPlugin.files.css.forEach((cssFile) => { %>
       <% if (cssFile !== 'critical-rendering-path.css') {%>
          <link rel="stylesheet" href="<%= cssFile %>"> 
       <% } %>
    <% }) %>
  </body>
</head>
```
