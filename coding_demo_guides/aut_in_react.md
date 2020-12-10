- AUT in React. 
- Outside in 

- Outside parts will be covered by Acceptance test with cypress - which you are hopefully becoming familiar with now.
- If i click on a button and fill in a field this should happen.. bla bla 
- Inside will be covered by unit tests, or component tests - since we are working with components. 
- to make sure our components, modules and services are doing what they are suppose to 

- Write an acceptance test, what we want te application to do, watch it fail
- write a component tests to slowly get to the point where the acceptance test passes, and then go over the cycle again

- We only write code to pass the test that we just wrote, we  need to stop ourselves to implement other features or functionalty, first we write the test

- Today we will build a small app that displays a list of employees, a small simple little HR-application, maybe? 

**show them lo-fi**

```
As a user of the application
In order to be able to work with employee management
I would like to access a list of employees.
```

1. The user access the application using her/his browser
2. The application fetches the list of employees from the company’s internal systems (exposed to the application by a Rest API endpoint)
3. A view with the employee data is rendered and displayed in the users’ browser.

```
$ yarn create react-app employee_management
```
- clean up files, as usual 

```
import React, { Component } from "react";

class App extends Component {
  render() {
    return (
      <>
        <section data-cy="header">
          <h1>Employee list</h1>
        </section>
      </>
    );
  }
}

export default App;
```

```
$ yarn add cypress --dev
```
```
$ ./node_modules/.bin/cypress open
```
- Remove examples 
- "cy:open": "yarn start & cypress open"
```
$ touch cypress/integration/displayEmployeeList.feature.js
```
```
describe('Display list of employees', () => {
  // Our tests will go here
})
```
```
it('when user visits the page', () => {
    cy.visit('http://localhost:3000')
    cy.get('[data-cy="header"]')
      .should('contain', 'Employee list')
})
```
- start server, run cypress - green yey!

```
  it('user can see a list of 5 employees', () => {
     cy.get('[data-cy="main"]').within(() => {
      cy.get('li').should('have.length', 5)
     })
  });
```
- This should fail for us
- So lets stop for a second, 
    - we want to display a list of users, 
    - we want to fetch that data from an external api, and 
    - we want them displayed in an unordered list. 
- Quite a lot going on, so lets extract that to a separate component
- Follow naming standards, EmployeeList
- We need to write tests for the code we wished we had 

- add and import the none existing component to the app
- tests are failing
- Move from outsite to inside and start with component testing. 
```
$ yarn add --dev enzyme enzyme-adapter-react-16
$ touch src/setupTests.js
```
```
import { configure } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';
configure({ adapter: new Adapter() });
```
```
$ mkdir src/__tests__
```
```
import React from 'react';
import { shallow, mount } from 'enzyme';
import EmployeeList from '../EmployeeList'
import axios from 'axios';

describe('<EmployeeList />', () => {
  it('should fetch employees from back-end using Axios', () => {
    const axiosSpy = jest.spyOn(axios, 'get');
    shallow(
      <EmployeeList />
    )
    expect(axiosSpy).toBeCalled();
  })
```
```
$ touch src/EmployeeList.jsx
```

- create a class component (rce)

- now we will se that it fails because axios was never called 
- show them reqres.in - tool for demo purposes, test data/fake data

**https://reqres.in/api/users?per_page=5**

```
$ yarn add axios
```
```
import React, { Component } from 'react'
import axios from 'axios'

class EmployeeList extends Component {
  state = {
    employees: []
  }

  componentDidMount() {
    this.fetchEmployeeData()
  }

  async fetchEmployeeData() {
    let employeeData = await axios.get(
      "https://reqres.in/api/users?per_page=5"
    );
    this.setState({employees: employeeData.data.data})
  }
  render() {
    return (
      <div>
        
      </div>
    )
  }
}

export default EmployeeList
```
- And we are going green, axios is being called when the component mounts
```
it('should render a list of 5 employees', async () => {
    const expectedData = {
      data: [
        {
          id: 1,
          first_name: "George",
          last_name: "Bluth",
          avatar:
            "https://s3.amazonaws.com/uifaces/faces/twitter/calebogden/128.jpg",
        },
        {
          id: 2,
          first_name: "Janet",
          last_name: "Weaver",
          avatar:
            "https://s3.amazonaws.com/uifaces/faces/twitter/josephstein/128.jpg",
        },
        {
          id: 3,
          first_name: "Emma",
          last_name: "Wong",
          avatar:
            "https://s3.amazonaws.com/uifaces/faces/twitter/olegpogodaev/128.jpg",
        },
        {
          id: 4,
          first_name: "Eve",
          last_name: "Holt",
          avatar:
            "https://s3.amazonaws.com/uifaces/faces/twitter/marcoramires/128.jpg",
        },
        {
          id: 5,
          first_name: "Charles",
          last_name: "Morris",
          avatar:
            "https://s3.amazonaws.com/uifaces/faces/twitter/stephenmoon/128.jpg",
        },
      ],
    };
    const describedComponent = mount(<EmployeeList/>)
    await describedComponent.setState({employees: expectedData.data})
    expect(describedComponent.find('li')).toHaveLength(5)
  });
```
- could find any li elements
```
import React, { Component } from "react";
import axios from "axios";

class EmployeeList extends Component {
  state = {
    employees: [],
  };

  componentDidMount() {
    this.fetchEmployeeData();
  }

  async fetchEmployeeData() {
    let employeeData = await axios.get(
      "https://reqres.in/api/users?per_page=5"
    );
    this.setState({ employees: employeeData.data.data });
  }
  render() {
    let employeeList = this.state.employees.map((employee) => {
      return (
        <li
          key={employee.id}
        >{`${employee.first_name} ${employee.last_name}`}</li>
      );
    });
    return (
      <div>
        <ul>{employeeList}</ul>
      </div>
    );
  }
}

export default EmployeeList;
```