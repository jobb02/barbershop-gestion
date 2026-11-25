# 06 · Mettre à jour un salon en service

[← Accueil du dépôt](../README.md) · [Sommaire](README.md) · [07 · Les versions →](07-versions.md)

Le salon travaille pendant que je développe. La règle : le patron ne perd aucune donnée.

## La méthode

1. **Base de test séparée**, jamais d'essai sur la vraie base.
2. **Sauvegarde neuve**, puis restauration sur mon PC pour vérifier qu'elle est utilisable.
3. **Script en une transaction** : tout réussit, ou rien n'est gardé. Il s'arrête s'il n'est pas sur la bonne base ou s'il a déjà été lancé.
4. **Empreintes avant et après** : un code calculé sur toutes les lignes. S'il change, le script annule tout.
5. **L'appli après le script**, pour qu'elle trouve toujours la base attendue.
6. **Retour arrière écrit d'avance.**

```sql
begin;
set local lock_timeout = '3s';            -- base occupée : on abandonne
-- empreinte avant, changement, empreinte après
do $$ begin
  if (select v from avant) <> (select md5(string_agg(to_jsonb(s)::text, '#' order by id)) from sales s)
    then raise exception 'STOP : une donnée a changé. Tout est annulé.'; end if;
end $$;
commit;
```

## Ce qui a coincé

- Fausse alerte de l'outil de restauration : un droit retiré par Supabase n'était pas recréé sur mon PC. Outil corrigé puis réessayé sur une vraie sauvegarde.
- Des noms de colonnes identiques à des alias dans mon garde-fou : il s'arrêtait à tort. Il a bloqué sans rien modifier, dans le bon sens.
- Sur téléphone, le tableau des parts débordait : l'accord est passé sous le nom du barber.
