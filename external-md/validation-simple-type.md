## Anatomie d'une Action

```scala
def updateDescription(jobId: JobId) = Action.async { req =>
  for {
    payload <- req.body.validate[UpdateDesc]  ?| BadRequest
    command = UpdateJobDescription(jobId, payload)
    job     <- CommandHandler.handle(command) ?| Conflict
  } yield Ok(Json.toJson(job))
}
```

on utilise le DSL de play-monadic-actions



## Validation de la requête
   
<img class="stretch" src="/schemas/1-from-http-to-command-missing-field.png"/>

1er niveau (validation JSON) : Controller

<aside class="notes">
   Chaque requête http (en écriture) à l'API correspond à une commande<br/>
   Et à une query en lecture<br/>
   API REST & CQRS
</aside>


