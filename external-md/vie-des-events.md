#### Vie des events


Pipeline

```
def addAccountStatus(json: JsValue): JsValue = json.as[JsObject] 
       + ("accountStatus" -> JsString("active"))
       
object UserCreated extends EventCompanion[User,  EntityCreation] {
    override def readPipeline: ReadPipeline[User] = ReadPipeline(
        3 -> addAccountStatus)}
```

Sérilisation et valeur par défaut

```
(__ \ "accountStatus").readNullable[String].map(_.getOrElse("active"))
```


