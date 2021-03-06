# fis-parser-react

A parser plugin for [fis](https://github.com/fis-dev/fis) to precompile [react](http://facebook.github.io/react/).

##Usage

* install this plugin (make sure you have installed [fis](https://github.com/fis-dev/fis) before).

    ```shell
    npm install -g fis-parser-react
    ```

* create a project

    project
        - foo.jsx
        - fis-conf.js

* vi ``fis-conf.js``

    ```javascript
    fis.config.set('project.fileType.text', 'jsx'); //*.jsx files are text file.
    fis.config.set('modules.parser.jsx', 'react');  //compile *.jsx with fis-parser-react plugin
    fis.config.set('roadmap.ext.jsx', 'js');        //*.jsx are exactly treat as *.js
    ```
* write a jsx file

    ```javascript
    /** @jsx React.DOM */
    var HelloMessage = React.createClass({
      render: function() {
        return <div>Hello {this.props.name}</div>;
      }
    });

    React.renderComponent(
      <HelloMessage name="John" />,
      document.getElementById('container')
    );
    ```

* release your project

    ```shell
    cd project              # get into project
    fis release -d output   # release your project to output dir
    ```

* you will get a compiled js file at ``output/index.js``

    ```javascript
    /** @jsx React.DOM */
    var HelloMessage = React.createClass({displayName: 'HelloMessage',
      render: function() {
        return React.DOM.div(null, "Hello ", this.props.name);
      }
    });

    React.renderComponent(
      HelloMessage( {name:"John"} ),
      document.getElementById('container')
    );
    ```
