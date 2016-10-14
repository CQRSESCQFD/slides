## Facile à tester

```scala
"when job status is finished UpdateJobDescription must be refused" in{
  //given
  val job = generateJob(generateUser)
    .gen(dataFactory).copy(status = Finished)
  val cmd = UpdateJobDescription("Nouvelle description")

   //when
  val eventsOrError = JobProtocol.updateJobProcessor
    .makeProcessor(cmd)
    .prepare(cmdCtxt , job)
    
   //then 
  eventsOrError should beLeft()
}
```

<aside class="notes">
    Pas de mock nécessaire<br/>
    Usage de générateurs type scalacheck pratiques
</aside>

