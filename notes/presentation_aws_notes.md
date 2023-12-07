# Sully Workshop: Le Cloud - 2023

## Introduction
- Comparaison entre OVH et AWS, soulignant la différence d'offre de services.
- AWS a lancé son offre de cloud en 2004.
- Types de Cloud:
  - Cloud Privé
  - Cloud Public: Services mutualisés
  - Cloud Hybride (Combinaison de privé et public)

## Offres Cloud
- On-Prem: Sur site
- IAAS (Infrastructure as a Service): Gestion de l'OS, dominé à 40% par AWS.
- CAAS (Container as a Service): Gestion du runtime, par exemple, Docker + Rancher.
- PAAS (Platform as a Service): Abstraction du runtime (ex: Heroku).
- FAAS (Function as a Service): Lié aux services managés.
- SAAS (Software as a Service).

## AWS Infrastructure
- Propre réseau AWS avec câblage: [Infrastructure AWS](https://infrastructure.aws/)

## Service d'Océrisation
- [Libeo - Factures Océrisation](https://libeo.io/blog/factures/ocerisation)

## Haute Disponibilité et Scalabilité
- Haute disponibilité assurée par les AZ (Availability Zones) ou les régions.
- Scalabilité horizontale et verticale avec autoscaling.

## Offre Amazon
- IAAS: EC2
- PAAS: Elastic Beanstalk
- FAAS: Lambda (AWS inventeur du FAAS)

## Modèle de Tarification
- Pay-as-you-go: Pas de trafic = 0€, [Détails de tarification](https://aws.amazon.com/fr/pricing/)
- Variations de services et prix selon les sites (Paris, Ireland).

## Aspects Juridiques et Souveraineté des Données
- CLOUD ACT: Obligation de fournir des données au gouvernement US sur demande.
- Facturation AWS hébergée aux USA.
- Edge Locations pour la maîtrise du routage des données.
- Offre FAAS non portable entre différents SCP (Service Cloud Provider), par exemple, AWS FAAS non compatible avec FAAS GCP.
- Cloud Souverain: Label SecNumCloud créé par l'ANSSI.

## AWS Services
- RDS: Service de base de données Amazon.
- Services managés en dehors des AZ.
- Gestion des buckets pour le stockage S3 (web static).
- CloudFront pour la mise à disposition mondiale des assets.

## Gestion des Services
- IAAS: Gestion de l'OS, gestion de l'obsolescence du Tomcat/Apache.
- CAAS (en Rancher): Gestion du runtime.

## Infrastructure as Code (IAC)
- CloudFormation (basé sur Terraform sur AWS).
- Exemple: Platform.sh vend de l'IAC.
