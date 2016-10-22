## Architecture de prod

* déploiement sur AWS opswork
* toutes les applications sont clusterisées
* déploiement et mises à jour par des recettes Chef   



### Archi réseau

![](images/archi-reseau.png)

<aside class="notes">
Parler  des optimisations en lecture de mongo sur framework d'aggregation : ReadPreference.secondaryPreferred<br/>
La valeur par defaut côté client reactiveMongo = Primary
</aside>



### AWS Opsworks 

![](images/opsworks-layers.png)
