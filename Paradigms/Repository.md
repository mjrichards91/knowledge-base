# Repository Pattern

The repositiory pattern implements an abstraction of the data access layer from the business logic layer. 

Its benefits include:  
* Minimizes duplicated query logic
* Decouples application from specific data frameworks
* Promotes testability

An example interface should contain the following:

```csharp
class IRepository
{
  Add(object)
  Remove(object)
  Get(id)
  List()
  Find(predicate)
}
```

Notice that an `Update(object)` method is missing. This is because repositories should not be aware of data saving, but rather a Unit of Work should be responsible for that.

### References:

* https://msdn.microsoft.com/en-us/library/ff649690.aspx
* https://blog.falafel.com/implement-step-step-generic-repository-pattern-c/
* https://www.youtube.com/watch?v=rtXpYpZdOzM
