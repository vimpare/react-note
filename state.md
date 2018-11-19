state:

**delete an item from the array**
To start, we’re going to create a state object.
The object will contain properties for everything you want to store in the state. For us, it’s characters.
 we’re going to create a removeCharacter method on the parent App class.
 必须将该函数传递给组件,向下传递到TableBody从Table
 在TableBody组件中，我们将键/索引作为参数传递，因此过滤器函数知道要删除的项
app.js
```
import React, {Component} from 'react';
import Table from './Table';
class App extends Component {
    state={
        characters:[
            {
                'name': 'Charlie',
                'job': 'Janitor'
            },
            {
                'name': 'Mac',
                'job': 'Bouncer'
            },
            {
                'name': 'Dee',
                'job': 'Aspring actress'
            },
            {
                'name': 'Dennis',
                'job': 'Bartender'
            }
        ]
    }
    removeCharacter = index => {
        const { characters } = this.state;
    
        this.setState({
            characters: characters.filter((character, i) => { 
                return i !== index;
            })
        });
    }
    render() {
        const { characters } = this.state;
        return (
          <div className="container">
              <Table  characterData={characters} removeCharacter={this.removeCharacter}/>
          </div>
        );
    }
}

export default App;
```

table.js
```
import React, {Component} from 'react';
const TableHeader = () => { 
    return (
        <thead>
            <tr>
                <th>Name</th>
                <th>Job</th>
            </tr>
        </thead>
    );
}
const TableBody = props => { 
    const rows = props.characterData.map((row, index) => {
        return (
            <tr key={index}>
                <td>{row.name}</td>
                <td>{row.job}</td>
                <td><button onClick={() => props.removeCharacter(index)}>Delete</button></td>
            </tr>
        );
    });

    return <tbody>{rows}</tbody>;
}
class Table extends Component {
    render() {
        const { characterData,removeCharacter  } = this.props;
        return (
            <table>
                <TableHeader />
                <TableBody characterData={characterData} removeCharacter={removeCharacter}/>
            </table>
        );
    }
}
// 类组件必须包含render()，并且return只能返回一个父元素。
// 注意，如果return包含在一行中，则不需要括号。
export default Table;
```

Submitting Form Data提交表格数据

我们对此表单的目标是每次在表单中更改字段时更新表单的状态，并且当我们提交时，所有数据将传递到App状态，然后将更新表。

app.js
```
import React, {Component} from 'react';
import Table from './Table';
import Form from './Form';
class App extends Component {
    state={
        characters:[]
    }
    removeCharacter = index => {
        const { characters } = this.state;
    
        this.setState({
            characters: characters.filter((character, i) => { 
                return i !== index;
            })
        });
    }
    handleSubmit = character => {
        this.setState({characters: [...this.state.characters, character]});
    }
    render() {
        const { characters } = this.state;
        return (
          <div className="container">
              <Table  characterData={characters} removeCharacter={this.removeCharacter}/>
              <Form handleSubmit={this.handleSubmit}/>
          </div>
        );
    }
}

export default App;
```
form.js

```
import React, { Component } from 'react';

class Form extends Component {
    constructor(props) {
        super(props);

        this.initialState = {
            name: '',
            job: ''
        };

        this.state = this.initialState;
    }
    handleChange = event => {
        const {name, value} = event.target;
    
        this.setState({
            [name] : value
        });
    }
    submitForm = () => {
        this.props.handleSubmit(this.state);
        this.setState(this.initialState);
    }
    render() {
        const { name, job } = this.state; 
    
        return (
            <form>
                <label>Name</label>
                <input 
                    type="text" 
                    name="name" 
                    value={name} 
                    onChange={this.handleChange} />
                <label>Job</label>
                <input 
                    type="text" 
                    name="job" 
                    value={job} 
                    onChange={this.handleChange}/>
                <input 
                    type="button" 
                    value="Submit" 
                    onClick={this.submitForm} />    
            </form>
        );
    }
}
export default Form;
```
