# Chapitre 1 - Les bases des bases de donnees relationnelles

**Version 0.1 - Parties 1 et 2**

## Objectifs du chapitre

A l'issue de ce chapitre, vous serez capable de :

- expliquer pourquoi les bases de donnees ont ete creees ;
- distinguer SQL, base de donnees et SGBD ;
- identifier les limites d'un stockage uniquement fonde sur des fichiers ;
- retracer les grandes etapes menant au modele relationnel ;
- expliquer le role d'Edgar F. Codd et la naissance de SQL ;
- reconnaitre les notions susceptibles d'etre evaluees dans une certification Oracle SQL.

---

## Partie 1 - Pourquoi les bases de donnees existent-elles ?

### 1.1 SQL n'est pas une base de donnees

SQL est un langage declaratif utilise pour interroger et manipuler des donnees. Oracle Database est un systeme de gestion de base de donnees relationnelle. Cette distinction est fondamentale : SQL exprime le resultat souhaite, tandis que le SGBD organise l'execution, le stockage, la securite et la coherence.

> **A retenir** - SQL est un langage. Oracle Database est un SGBD.

### 1.2 Avant les bases de donnees relationnelles

Les premieres applications informatiques stockaient leurs informations dans des fichiers propres a chaque programme. Un service commercial, la comptabilite et le service apres-vente pouvaient chacun conserver une copie differente du meme client.

Cette organisation entrainait plusieurs difficultes :

- redondance des donnees ;
- incoherences entre fichiers ;
- dependance forte entre programmes et formats ;
- recherches transversales difficiles ;
- securite et tracabilite limitees ;
- gestion complexe des modifications simultanees.

### 1.3 Exemple : trois fichiers, trois versions d'un client

| Source | Identifiant | Nom | Ville |
|---|---:|---|---|
| Clients.xlsx | 101 | Dupont | Paris |
| Commandes.xlsx | - | DUPONT | Paris 16 |
| Factures.xlsx | - | M. Dupont | PARIS |

Un humain peut supposer qu'il s'agit de la meme personne. Un programme ne peut pas le garantir sans identifiant stable ni regles de coherence.

### 1.4 Ce qu'apporte un SGBD

Un SGBD fournit notamment :

- une organisation centralisee des donnees ;
- des contraintes d'integrite ;
- des mecanismes de transaction ;
- une gestion des utilisateurs et privileges ;
- des mecanismes de sauvegarde et restauration ;
- un langage de requete commun ;
- un acces concurrent controle.

### 1.5 Donnee, information et connaissance

Une **donnee** est une valeur brute, par exemple `450`. Une **information** lui donne un contexte : `montant de la facture = 450 EUR`. Une **connaissance** resulte de l'interpretation : `ce client depasse son montant moyen d'achat`.

> **Piege de l'examen** - Une base de donnees stocke des donnees structurees ; elle ne transforme pas automatiquement toutes les donnees en connaissance metier.

### 1.6 Pourquoi une feuille de calcul ne remplace pas toujours un SGBD

Une feuille de calcul est excellente pour l'analyse personnelle, les calculs rapides et les petits jeux de donnees. Elle devient moins adaptee lorsque plusieurs utilisateurs modifient les memes informations, lorsque les relations sont nombreuses ou lorsque des controles d'integrite stricts sont requis.

| Besoin | Feuille de calcul | SGBD relationnel |
|---|---|---|
| Calcul ad hoc | Tres adapte | Possible |
| Plusieurs utilisateurs | Limite | Concu pour cela |
| Contraintes referentielles | Faibles | Natives |
| Transactions | Limitees | Natives |
| Droits fins | Limites | Avances |
| Requetes complexes | Possibles mais fragiles | SQL |

### 1.7 Resume de la partie 1

Les bases de donnees ont ete creees pour assurer la coherence, la disponibilite, la securite et la recherche efficace des donnees. Elles reduisent les duplications inutiles et permettent a plusieurs applications de partager une source fiable.

---

## Partie 2 - Histoire et naissance du modele relationnel

### 2.1 Les modeles hierarchiques et reseau

Avant le modele relationnel, les donnees etaient souvent organisees comme un arbre ou un reseau de pointeurs. Ces modeles pouvaient etre performants, mais les programmes devaient connaitre les chemins d'acces. Une modification de structure pouvait donc imposer des changements importants dans les applications.

### 2.2 Charles W. Bachman et le modele reseau

Charles W. Bachman a contribue au developpement des premiers systemes de gestion de bases de donnees et a formalise des idees centrales du modele reseau. Les enregistrements etaient relies par des chemins explicites. Le programmeur naviguait de record en record.

### 2.3 Edgar F. Codd et l'article de 1970

En 1970, Edgar F. Codd publie un article fondateur proposant d'organiser les donnees sous forme de relations mathematiques. L'utilisateur n'a plus besoin de connaitre les chemins physiques d'acces. Il indique quelles donnees il souhaite obtenir.

Les principes essentiels sont :

- representation tabulaire logique ;
- independance entre vue logique et stockage physique ;
- operations fondees sur les ensembles ;
- utilisation de cles pour identifier et relier les lignes ;
- langage declaratif plutot que navigation pas a pas.

### 2.4 Relation mathematique et table SQL

Dans la theorie relationnelle, une relation est un ensemble de tuples. En pratique SQL, elle est representee par une table. Les deux notions sont proches mais pas parfaitement identiques : SQL peut autoriser des doublons et des valeurs NULL, alors qu'une relation mathematique est un ensemble sans doublon.

> **A retenir** - Une table SQL est l'implementation pratique du modele relationnel, avec quelques differences importantes par rapport a la theorie mathematique.

### 2.5 IBM System R et SEQUEL

IBM a developpe System R pour demontrer qu'un systeme relationnel pouvait etre utilisable et performant. Le langage SEQUEL, ensuite renomme SQL, a ete concu pour permettre d'exprimer des requetes de facon declarative.

Exemple declaratif :

```sql
SELECT customer_name
FROM customers
WHERE city = 'Paris';
```

La requete indique le resultat attendu, pas le chemin physique a suivre pour le produire.

### 2.6 Oracle et la commercialisation de SQL

Oracle fait partie des premiers editeurs a avoir commercialise un SGBD relationnel utilisant SQL. Au fil des versions, Oracle Database a ajoute de nombreuses fonctions tout en conservant le coeur relationnel et le langage SQL.

### 2.7 La normalisation de SQL

SQL a ensuite ete normalise par des organismes de standardisation. Les produits implementent un socle commun mais conservent des extensions propres. Oracle utilise par exemple `VARCHAR2`, la table `DUAL` dans certains contextes historiques, et diverses fonctions specifiques.

### 2.8 Norme SQL et dialecte Oracle

| Concept | SQL standard | Oracle SQL |
|---|---|---|
| Requete de base | `SELECT` | `SELECT` |
| Chaine variable | `VARCHAR` | `VARCHAR2` recommande |
| Limitation de lignes | Standard moderne | `FETCH FIRST`, `ROWNUM` historique |
| Difference d'ensembles | `EXCEPT` | `MINUS` |

> **Piege de l'examen** - Une syntaxe valide dans PostgreSQL, MySQL ou SQL Server n'est pas automatiquement valide dans Oracle.

### 2.9 Frise chronologique simplifiee

| Periode | Etape |
|---|---|
| Annees 1960 | Modeles hierarchiques et reseau |
| 1970 | Publication du modele relationnel par E. F. Codd |
| Annees 1970 | System R et developpement de SEQUEL/SQL |
| Fin des annees 1970 | Premiers SGBD relationnels commerciaux |
| Annees 1980-1990 | Standardisation et diffusion de SQL |
| Aujourd'hui | SQL reste central dans les systemes transactionnels et analytiques |

### 2.10 Resume de la partie 2

Le modele relationnel a remplace la navigation explicite dans les donnees par une approche declarative et fondee sur les ensembles. SQL est ne de cette evolution. Oracle a participe tres tot a la commercialisation des SGBD relationnels et propose aujourd'hui son propre dialecte du langage.

---

## Exercices de consolidation

1. Expliquez la difference entre SQL et Oracle Database.
2. Donnez trois limites d'une architecture fondee uniquement sur des fichiers.
3. Pourquoi un identifiant stable est-il preferable au nom d'un client ?
4. Quelle difference fondamentale existe entre un langage navigational et un langage declaratif ?
5. Pourquoi une table SQL n'est-elle pas exactement identique a une relation mathematique ?
6. Citez deux exemples de particularites Oracle par rapport a d'autres dialectes SQL.

## Mini-QCM

**1. Quel enonce est correct ?**

A. SQL est un serveur de base de donnees.  
B. Oracle Database est un langage.  
C. SQL est un langage utilise par un SGBD.  
D. Une table est un fichier Excel.

**Reponse : C.**

**2. Quel avantage est typiquement fourni par un SGBD ?**

A. Suppression de tout besoin de sauvegarde.  
B. Gestion des transactions et des acces concurrents.  
C. Garantie qu'aucune erreur humaine ne se produira.  
D. Conversion automatique des donnees en connaissance.

**Reponse : B.**

**3. Le modele relationnel est principalement associe a :**

A. Charles Babbage.  
B. Edgar F. Codd.  
C. Alan Turing.  
D. Larry Page.

**Reponse : B.**

## Prochaines parties prevues

- Partie 3 - Tables, lignes, colonnes et types de donnees.
- Partie 4 - Cles, relations et cardinalites.
- Partie 5 - Contraintes, transactions et proprietes ACID.
- Partie 6 - Exercices, QCM et corriges complets.

## References de travail

- Documentation Oracle Database SQL Language Reference.
- Article fondateur d'Edgar F. Codd, *A Relational Model of Data for Large Shared Data Banks* (1970).
- Standards ISO/IEC 9075 relatifs a SQL.
