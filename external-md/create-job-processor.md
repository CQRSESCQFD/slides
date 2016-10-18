### Exemple de processor
 
```scala 
CommandProcessor[UpdateJob, Job] {
  cmd =>
    new CommandProcessor[UpdateJob, Job] {
    
    override def validator =
      StateIsNotNull[Job] |+| StatusIsOneOf(InReview, Pending)
   
    override def events(context: CommandContext) = (state: Job) =>
      JobDescriptionUpdated(
        context,
        FieldUpdate(state.description, cmd.job.description)) :: Nil
        
    }
}
```