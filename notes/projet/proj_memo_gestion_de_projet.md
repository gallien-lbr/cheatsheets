# Mémo Gestion de projet - Les documents de conception.



## Cahier des charges 
Document initial du porteur du besoin (client / maîtrise d'ouvrage). 
Objectif => formuler le besoin initial.

## SFG / GFS

- Rédigé par la maîtrise d'oeuvre (réalisateur de la solution).
- Proposition technique de haut niveau sur les fonctionnalités à implémenter.
- Spécifications Fonctionnelles Générales pour décrire les décrire fonctionnalités du client.

SFG = Document orienté client / commerciaux.
pour les petits projet, passer directement au SFD.

Doivent figurer, la reformulation du besoin métier.
* Objectifs à atteindre
* Objectifs stratégiques
* Principaux utilisateurs finaux
* Contraintes internes / externes

### 6 piliers SFG

1) Reformulation du besoin métier (Objectifs stratégiques, périmètre de la solution cible, contraintes internes / externes, end-users)
2) Processus métier (fourni par la MOA) => comment la solution va s'intégrer à l'env. économique des utilisateurs / de l'organisation
3) Vue macro-scopique du SI (intégration du logiciel dans le SI) 
4) Traduction des besoins métiers de haut niveau, décrit de manière synthétique
5) Exigences Non Fonctionnelles (décrire le **comment ?**) - ENF - Performances / maintenabilité etc.
6) Priorisation

Pas de SGF en mode "run".
Pas de SFG en Agile.

## SFD - Spécifications Fonctionnelles Détaillées 

**En résumé :**
- document orienté équipe de dévs / graphistes
- 1 livrable
- schémas / maquettes
- 1 phase du projet
- description des fonctionnalités du projet
- projet géré de manière "traditionnelle" cycle en V ou Watefall (pas en Agilité qui utilise le `product backlog` ou les `user stories`)

Information à mettre : 
- Enumérer les fonctionnalités.
- Code couleurs application, polices.
- Partie maquettage, zoning.
- Scénarios de l'application.
- Etc ...

## STD - Spécifications Techniques Détaillées 

Partie technique: le STD n'est pas systématiquement présenté au client. 
- choix technologique
- outils utilisés pour l'automatisation des tâches, build, déploiement.
- diagrammes (ex: séquences, SADT, UML, schéma base de données etc.)

## Document Gestion de produit  (draft)

possible de mettre des schéma de gestion projet: 
- WBS (Work Breakdown structure), DBS (Deliverable Breakdown Structure)
- GANTT
- PERT (Program evaluation and review technique)
  
## Différence Projet / Produit 

**Produit:**
* uniquement ce qui est développé / livré au client

**Projet:**
* découverte client
* partie adminstrative / juridique
* évaluation chiffrage tâches
* partie conception
* partie livraison
* partie tests

## DAT - Dossier d'Architecture Technique

Le DAT (document d’architecture technique) est un document réalisé par un architecte technique. Il définit et documente tout ce qu’il faut faire et mettre en place pour réussir la mise en œuvre de l’architecture, en vue d’atteindre les objectifs et respecter les différentes contraintes.

## DEX - Dossier d'Exploitation

Le DEX contient les informations dont l'équipe d'exploitation a besoin pour pouvoir assurer une exploitation en règle du système et pouvoir réagir de manière appropriée lorsqu'un problème surgit.


## BAT - Bon à Tirer 

Pour la communication graphique print et utilisé en imprimerie (kakémono, carte de visites etc.) 

## Ressources

* [Video Explicative sur les SFG](https://youtu.be/nP8nymGCfw8)
* [Video Explicative sur les SFD](https://www.youtube.com/watch?v=aWPM-JGR0qI&ab_channel=BestOfBusinessAnalyst)
* [Video sur les documents de conception](https://youtu.be/YpTFkXNzkcU)
* [Slideshare sur le SCRUM](https://www.slideshare.net/LuongMinhHai/mod-6-agile-scrum-in-a-nutshellpdf)
* [Gouvernance projet / Comitologie](https://blog-gestion-de-projet.com/comitologie-projet/)
* [Video Comitologie](https://youtu.be/oy5kGqzuuEc)
