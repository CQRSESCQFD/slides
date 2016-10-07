## Une commande, des events

```
case object CreateJob extends JobCmd
object JobCreated extends EventCompanion[Job,  EntityCreation]

case class UpdateJobDescription extends JobCmd
object JobDescriptionUpdated extends 
        EventCompanion[String, FieldUpdate]

```