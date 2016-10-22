## Facile à tester

```scala
"when status is finished UpdateJobDescription must be refused" in {
  //given
  val job = generateJob(generateUser)
    .gen(dataFactory)
    .copy(status = Finished) // interdit d'updater un job Finished
    
  val cmd = UpdateJobDescription("Nouvelle description")

  //when
  val eventsOrError = JobProtocol.updateJobProcessor
    .makeProcessor(cmd)
    .prepare(cmdCtxt , job)
    
  //then 
  eventsOrError should beLeft()
}
```

Note:
* Pas de mock nécessaire
* On aurait pu utiliser scalacheck
* Usage de générateurs type scalacheck pratiques 


