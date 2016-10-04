## Akka persistence

```
sealed trait UserEvent
case class LastNameUpdatedEvent(lastName: String) extends UserEvent

class UserPersistenceActor extends PersistentActor {
  
  var state = User("user-57d80fb91db5e79549713ab5", "John", "DOE")
  
  override def persistenceId = "user-57d80fb91db5e79549713ab5"
  
  override def receiveCommand: Receive = {
    case LastNameUpdatedEvent(newLastName) => 
        state = state.copy(lastName = newLastName)
 }
```
