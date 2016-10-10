## Akka persistence

```
sealed trait UserEvent
case class LastNameUpdated(lastName: String) extends UserEvent
case class User(userId:String,firstName:String, lastName:String)

class UserPersistenceActor extends PersistentActor {
  var state = User("user-57d80fb91db5e79549713ab5", "John", "DOE")
  
  override def persistenceId = "user-57d80fb91db5e79549713ab5"
  
  override def receiveCommand: Receive = {
    case LastNameUpdated(newLastName) => 
        state = state.copy(lastName = newLastName)
 }
```

<aside class="notes">
    Persistence de l'état d'un acteur<br/>
    Logs d'event<br/>
    Snapshots de l'état de l'acteur<br/>
</aside>
