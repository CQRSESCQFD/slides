### Sauvegarde des snapshots
```scala
class MongoSnapshotStore extends SnapshotStore   {
  override def saveAsync(meta: SnapshotMetadata, 
                         snap: Any): Future[Unit] =
    snap match {
      case u: User =>
        userDao.save(u.copy(snapshotMetadata = Some(meta)))
      case j: Job =>
        jobDao.save(j.copy(snapshotMetadata = Some(meta)))
   }
}
```
<aside class="notes">
    Nécessité d'écrire un store custom, car impossible de gérer plusieurs types d'états<br/>
    Quel format de serialisation des events : play-json (connaissance de la lib, plus facile de gérer les versions events)<br/>
    Comment réparer des snapshots<br/>
    Events vs snapshots : aspect backup
    Contenu des métadatas : persistenceId, sequenceNr, timestamp
</aside>