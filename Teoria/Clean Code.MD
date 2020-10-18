# Clean Code

[More Info](https://github.com/ryanmcdermott/clean-code-javascript)

### Function arguments (2 or fewer ideally)
Before aplly Clean Code.
```js
  function createMenu(title,body,buttonText, cancellabel){
    // ...
  }
```
After aplly Clean Code.
```js
  const menuOptions={
    title:'foo',
    body:'Bar,
    buttonText:'Baz',
    cancellable:true
  }
  
  function createMenu(menuOptions){
   // ...
  }
```

### Functions should do one thing
Before aplly Clean Code.
```js
  function emailClients(clients){
    clients.forEach((client) => {
      const clientRecord = database.lookup(client);
      if(clientRecord.isActive()){
        email(client);
      }
    });
  }
```
After aplly Clean Code.
```js
  function emailClients(clients){
    clients
      .filter(isClientActive)
      .forEach(email);
  }
  
  function isClientActive(client){
    const clientRecord = database.lookup(client);
    return clientRecord.isActive();
  }
```

### Function names should say what they do
Before aplly Clean Code.
```js
  function addToDate(date,month){
    // ...
  }
  
  const date = new Date();
  addToDate(date,1);
```
After aplly Clean Code.
```js
  function addMonthToDate(month, date){
    // ...
  }
  
  const date = new Date();
  addMonthToDate(1,date);
```

### Functions should only be one level of abstration
Before aplly Clean Code.
```js
  function parseBetterJSAlternative(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach(token => {
    // lex...
  });

  ast.forEach(node => {
    // parse...
  });
}
```
After aplly Clean Code.
```js
  function parseBetterJSAlternative(code) {
  const tokens = tokenize(code);
  const syntaxTree = parse(tokens);
  syntaxTree.forEach(node => {
    // parse...
  });
}

function tokenize(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      tokens.push(/* ... */);
    });
  });

  return tokens;
}

function parse(tokens) {
  const syntaxTree = [];
  tokens.forEach(token => {
    syntaxTree.push(/* ... */);
  });

  return syntaxTree;
}
```

### Remove duplicate code
Before aplly Clean Code.
```js
  function showDeveloperList(developers) {
  developers.forEach(developer => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();
    const data = {
      expectedSalary,
      experience,
      githubLink
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach(manager => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();
    const data = {
      expectedSalary,
      experience,
      portfolio
    };

    render(data);
  });
}
```
After aplly Clean Code.
```js
function showEmployeeList(employees) {
  employees.forEach(employee => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();

    const data = {
      expectedSalary,
      experience
    };

    switch (employee.type) {
      case "manager":
        data.portfolio = employee.getMBAProjects();
        break;
      case "developer":
        data.githubLink = employee.getGithubLink();
        break;
    }

    render(data);
  });
}
```

### Don't use flags as function parameters
Before aplly Clean Code.
```js
  function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```
After aplly Clean Code.
```js
  function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```
