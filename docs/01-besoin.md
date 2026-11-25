# 01 · Le besoin de départ

[← Accueil du dépôt](../README.md) · [Sommaire](README.md) · [02 · Architecture →](02-architecture.md)

## La situation

Un ami a ouvert un barbershop. Il notait les prestations de chaque barber dans une application de notes, puis calculait la part de chacun à la main en fin de mois. J'ai vu un autre barber faire pareil.

## Ce qu'il fallait

| Besoin | Réponse |
|---|---|
| Savoir qui a fait quoi | Un ticket par barber, avec ses prestations |
| Ne pas perdre de passage pendant l'affluence | Un ticket ouvert par barber, gardé quand on passe au suivant |
| Gérer les clients sans réservation | Une liste d'attente du jour, avec rappel par SMS ou WhatsApp |
| Séparer l'équipe et le patron | Deux rôles, vérifiés par la base |
| Calculer les parts | Un pourcentage par barber, avec une date de départ |

## Les limites fixées

- Outil de gestion interne. Le salon garde une vraie caisse à côté.
- Utilisable sur iPad et téléphone, sans rien installer.
- L'équipe ne doit pas avoir besoin d'une formation.
