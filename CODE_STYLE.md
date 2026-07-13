# Conventions SQL et éditoriales

## SQL

- mots-clés SQL en majuscules ;
- noms de tables et colonnes en minuscules dans les exemples ;
- une clause principale par ligne ;
- indentation de quatre espaces ;
- point-virgule en fin d'instruction ;
- alias explicites et courts ;
- éviter `SELECT *` sauf démonstration pédagogique.

Exemple :

```sql
SELECT c.customer_id,
       c.customer_name,
       COUNT(o.order_id) AS order_count
FROM customers c
LEFT JOIN orders o
    ON o.customer_id = c.customer_id
GROUP BY c.customer_id,
         c.customer_name
ORDER BY order_count DESC;
```

## Rédaction

- phrases courtes ;
- expliquer chaque terme à sa première occurrence ;
- distinguer la norme SQL du comportement propre à Oracle ;
- utiliser des exemples métier simples ;
- annoncer les prérequis ;
- terminer chaque section par une synthèse.

## Encadrés

- **À retenir** : synthèse essentielle ;
- **Piège de l'examen** : ambiguïté ou erreur fréquente ;
- **En entreprise** : usage professionnel ;
- **Conseil** : méthode pratique ;
- **À tester** : manipulation reproductible.
