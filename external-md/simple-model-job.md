## Le modèle métier

* deux types d'entités
    * User
    * Job



## User

```
 {  "_id"       : "user-57d80fb91db5e79549713ab5"
    "firstName" : "John", "lastName"  : "DOE",
    "location" : {
        "rangeKm" : 10,
        "address" : {
            "street" : "7 allée de la Cristallerie", 
            "zipCode" : "92000", "city" : "Sèvres"
        },
       "city" : "Sèvres",
       "geolocation" {"longitude" : 47.34930, "latitude" : 0.72678},
    }
    //if skills exists, user =  provider
    "skills" : ["babysitting", "garde_enfants"]
}
```

<aside class="notes">
    persisté comme ça dans mongo
</aside>



## Job
```
{
  "_id"         : "job-5551bb001000002e00b5194a",
  "description" : "Garder mes enfants de 17h->19h les vendredi",
  "askerId"     : "user-57d80fb91db5e79549713ab5",
  "skill"       : "babysitting",
  "location" : {
      "longitude" : 47.349308,
      "latitude" : 0.726781
   },
   "status" : "inreview",
   "expirationDate" : "2016-11-30T23:59:59.999Z"
 }
```

<aside class="notes">
    Le statut sera modifé par la suite
    Requêtes geolocalisées (read model)
</aside>

