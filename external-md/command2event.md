## Une commande, un/des events

```
case object CreateJob extends JobCmd
object JobCreated extends EventCompanion[Job,  EntityCreation]

case class UpdateJobDescription extends JobCmd
object JobDescriptionUpdated extends 
        EventCompanion[String, FieldUpdate]

``` 
<aside class="notes">
    Granularité commande / event
    1 / 1 ou 1 -> N
</aside>