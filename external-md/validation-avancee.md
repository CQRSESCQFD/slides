## Validations à la carte
```
//company
(__ \ "name").readNullable[String] and
(__ \ "siren").readNullable[String](length(8)) and
(__ \ "siret").readNullable[String](length(14)) and
(__ \ "phoneNumber").readNullable[String] and
(__ \ "tvaNumber").readNullable[String](length(13)) and
(__ \ "capital").readNullable[BigDecimal]
  
```
<aside class="notes">
    Découpage de ses classes de validation/serialisation en package (controller, shared, persistance, events)<br/>
    Notions de DTO avec conversions implicites ???
</aside>