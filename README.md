# Planetes_Neo4j

Nous avons créé ce repository ensemble avec Paul L. dans le cadre de la formation Mastère "Big Data Engineer" de l'Université de Technologie de Troyes.  Ce projet a pour but de batir et d'utiliser une base de données graphes Neo4j. Ce cours était assuré par Jérôme B.
La version la plus à jour est v4 Rapport.
Nous avons choisi pour ce projet Neo4j d’utiliser les données publiques de la NASA sur les exoplanètes découvertes (confirmées). Il y en a 5539 officielles à ce jour.


## Le projet comporte plusieurs parties:
1. Recherche et Pré-traitement des données brutes - Planètes_Pré-traitement.ipynb
2. Définition de la structure de la base de données - Page 6 du rapport Projet_Neo4j_LELEGARD_MORAND.pdf
3. Ingestion des données dans Neo4j - Script_Neo4j.txt
4. Requêtes de la base de données  - Requetes_Neo4j.txt
5. Visualisation du résultat des requêtes - Exoplanet_Viz.ipynb  

Pour plus de détail, se rapporter au rapport Projet_Neo4j_LELEGARD_MORAND.pdf, disponible dans ce repository. Le modèle Neo4j comporte 9855 noeuds et 1 635 303 relations.

---

## Ci-dessous un exemple de requête (Requête_1)

« Un concours est lancé, le prochain observatoire qui trouvera une nouvelle planète autour d’une étoile de classe spectrale « K0 » gagnera 1 million de dollars ! Quels sont les systèmes que l’observatoire de Haute-Provence doit surveiller pour avoir une chance de gagner ? »

### Traduction de la requête en code Cypher:  
MATCH (obs:Observatoire{Nom:'Haute-Provence Observatory'})  
WITH obs.Latitude AS Lat_Haute_Provence  
MATCH (obs:Observatoire)-[r1:EST_SITUE_DANS]->(hem:Hemisphere)-[r2:ON_PEUT_VOIR_DEPUIS]->(con:Constellation)<-[r3:APPARTIENT_A]-(st:Systeme_stellaire)-[r4:RAYONNE]->(sp:Classe_spectrale)  
WHERE (obs.Nom = 'Haute-Provence Observatory') AND (sp.Code = 'K') AND (r4.Subdivision = 0.0) AND (r2.Latitude_max > Lat_Haute_Provence)  
RETURN obs,r1,hem,r2,con,r3,st,r4,sp  

### Résultat de la requête
![image](https://github.com/Nimodeyv/Planetes_Neo4j/assets/105541734/1b7bd704-538b-4de2-9043-259e7a55e441)
