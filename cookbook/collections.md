## Collections

  
**Q:  How do I insert an { array | date | boolean | session } into a document record?**  
This example should mostly cover it:

````
Todos.insert({
  text: text,
  gannt.dependency: dependency,
  gannt.parent: parent,
  list_id: Session.get('list_id'),
  done: false,
  timestamp: (new Date()).getTime(),
  tags: tag ? [tag] : []
});
````

**Q:  How do I get the _id of the most recently created document?**  

````
var id = Todos.insert({text: 'foo'});
````


**Q:  Something is funny with arrays in my document.  Help!**  
So, Mongo reactivity is currently limited, in that it's not reactive on arrays of object.  

````js
// the objects in an array are not reactive
{ 
  _id: "xjkhce8wcudx", 
  person: { 
    name:"Jane", 
    age:"22"
  },
  friends: [ 
    personA: { //not reactive 
      name:"Joe", //not reactive
      age:"24"  //not reactive
    }, 
    personB: {  //not reactive
      name:"Julia", //not reactive
      age:"27"  //not reactive
    }, 
  ], 
  highscores: [
     "1068954",
     "56793",
     "34509"
  ]
  score: "20690"
}
````


------------------------------------------------------------------
### Pagination
The pattern seems to be to use $limit on the server, and $slice on the client.  

https://trello.com/card/pattern-for-easy-pagination/508721606e02bb9d570016ae/67  
http://stackoverflow.com/questions/14167394/ideal-way-of-doing-infinite-scroll-and-real-time-updates-in-meteor  
