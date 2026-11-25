# 03 · Rôles et accès

[← Accueil du dépôt](../README.md) · [Sommaire](README.md) · [04 · Corriger sans effacer →](04-corriger-sans-effacer.md)

Au début, un seul compte pour tout le monde : toute personne connectée voyait tout. Les gérants ont demandé que l'équipe encaisse sans voir les chiffres.

| Action | Salon | Patron |
|---|:-:|:-:|
| Enregistrer une vente aujourd'hui | ✅ | ✅ |
| Lire les ventes | ❌ | ✅ |
| Voir les passages du jour | selon le réglage | ✅ |
| Voir le bilan et les parts | ❌ | ✅ |
| Changer les prix et les réglages | ❌ | ✅ |

## La règle est dans la base

Cacher un bouton ne protège rien : la clé publique de l'appli est lisible par n'importe qui. Chaque table a donc une *Row Level Security* (PostgreSQL vérifie chaque ligne selon le compte connecté). Exemple simplifié :

```sql
create policy ventes_patron on sales for select to authenticated
  using (salon_id in (select salons_avec_role(array['patron'])));
```

Le salon peut ajouter une vente mais pas la relire. Pour afficher les passages, il appelle une fonction qui ne renvoie que les colonnes permises.

## Vérifié

Chaque règle est essayée avec un compte du mauvais rôle : lire, ajouter, modifier, supprimer, se donner le rôle patron, écrire dans un autre salon.
