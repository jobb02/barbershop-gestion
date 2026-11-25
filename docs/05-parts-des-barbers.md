# 05 · Parts des barbers

[← Accueil du dépôt](../README.md) · [Sommaire](README.md) · [06 · Mettre à jour un salon en service →](06-mise-en-production.md)

## Le principe

Le patron règle, pour chaque barber, un pourcentage (ou « salarié au mois ») et la date à partir de laquelle il compte. Le bilan affiche le total des prestations, la part du barber et ce qui reste au salon.

## Les choix

| Cas | Choix | Pourquoi |
|---|---|---|
| Le pourcentage change | L'accord en vigueur le jour de la vente s'applique | Un ancien bilan ne change pas tout seul |
| Centimes | Calcul en centimes, le salon prend le reste | Part + salon = total, exactement |
| Erreur de saisie | On ajoute une ligne, la dernière compte | L'historique reste dans la base |
| Saisie douteuse (`6O`, `60 %`, `101`) | Refusée | Un « O » à la place d'un zéro donnait 6 % |
| Copie pour un barber | Seulement sa ligne | Il n'a pas à voir les autres |

Table en ajout seul, lue et complétée par le patron uniquement. Un essai tire 4 000 cas au hasard et vérifie la somme à chaque fois.

C'est une aide au calcul, pas une fiche de paie.
