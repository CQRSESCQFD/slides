## Validation simple par les types

```scala
case class Job(description: Option[String] = None, 
    askerId : UserId, 
    skill: Skill)
    
sealed trait Skill
case objet Babysitting extends Skill

//formatters par défaut
implicit val skillFormat = Json.format[Skill]
implicit val jobFormat = Json.format[Job]
```