## Akka persistence

```
class UserPersistenceActor extends PersistentActor {
  var state = User("user-57d80fb91db5e79549713ab5", "John", "DOE")
  
  override def persistenceId = "user-57d80fb91db5e79549713ab5"
  
  override def receiveCommand: Receive = {
    // validation de commande
    // appel à persist
    // update du state après persist
  }
        
  override def receiveRecover: Receive = {
    // update du state     
  }      
  
 }
```

<aside class="notes">
    Persistence de l'état d'un acteur<br/>
    Logs d'event<br/>
    Snapshots de l'état de l'acteur<br/>
</aside>
