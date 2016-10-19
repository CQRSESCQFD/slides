### Chargement des snapshots
```scala
class MongoSnapshotStore extends SnapshotStore   {
 override def loadAsync(persistId: String) Future[Option[Snap]] = {
    persistId.split("-").toList match {
      case "job" :: id :: Nil =>
        jobDao.findById(JobId(id))
      case "user" :: id :: Nil=>
        userDao.findById(UserId(id))
   }
}
```
<aside class="notes">
    Comment réparer des snapshots : recovery<br/>
    Events vs snapshots : aspect backup
    
</aside>