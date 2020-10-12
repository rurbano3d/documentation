```js

    fellowshipMember.id = uuid();
    fellowshipMember.name = 'Sam';
    fellowshipMember.jobFunction = 'Master of Focus';
    
    //Pode ser substituído por
    
    Object.assign(fellowshipMember, { id: uuid(), name:'Sam', jobFunction:'Master of Focus' });
    
```
