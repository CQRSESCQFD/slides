### Chargement des snapshots
```
class MongoSnapshotStore extends SnapshotStore   {
  override def loadAsync(persistenceId: String): Future[Option[Snap]] = {
      persistenceId.split("-").toList match {
            case "job" :: id :: Nil =>
               jobOpt <- jobDao.findById(JobId(id))
            case "user" :: id :: Nil=> 
               userOpt <- userDao.findById(UserId(id))

   }
}
```
<aside class="notes">
    Comment réparer des snapshots<br/>
    Events vs snapshots : aspect backup
    
</aside>