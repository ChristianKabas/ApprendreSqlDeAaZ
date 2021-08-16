# Les Fondamentaux de SQL
## Somaire
``` sql
- Les fondamentaux des requêtes SQL
- Jointures
- SQL Avancé: Fonctions et Sous-requêtes
- Création de bases et de tables
- Vues
```

Nous allons travailler sur la base de donnée SKILA:
page d'installation **[sakila-installation](https://dev.mysql.com/doc/sakila/en/sakila-installation.html)**.
### Structured Query Language
Le **SQL** (Structured Query Language) est un langage permettant de communiquer avec une base de données. Ce langage informatique est notamment très utilisé par les développeurs web pour communiquer avec les données d’un site web. SQL.sh recense des cours de SQL et des explications sur les principales commandes pour lire, insérer, modifier et supprimer des données dans une base.
- #### SELECT
  - Une des tâches les plus récurrentes est d'interroger une base de donnée en utilisant la declaration **SELECT**
  - Elle a beacoup de clauses que vous pouvez combiner pour former une requête puissante
  - Syntaxe :
    ``` sql
    SELECT colonne1,colonne2 FROM table;
    ```
  - Préciser la liste des colonnes de la table qu'on souhaite retourner dans la clause **SELECT**
    - Utiliser une virgule entre deux colonnes
    - Si vous souhaitez retourner toutes les colonnes utilisez un astérisque : *
  - Indiquer le nom de la table après le mot clé **FROM**
  - *Exemple* :
    ``` sql
    SELECT first_name,last_name FROM actor;
    ```
- #### SELECT DISTINCT
  - Dans une table, une colonne peut contenir des valeurs dupliquées.
  - On souhaite avoir la liste des différentes valeurs uniques (sans doublons)
  - **DISTINCT** permet de retourner les valeurs uniques (sans doublons)
  - Syntaxe :
    ``` sql
    SELECT DISTINCT colonne1,colonne2 FROM table;
    ```
  - *Exemple* :
    ``` sql
    SELECT DISTINCT rental_rate FROM film;
    ```
- #### SELECT WHERE
  - Si on souhaite avoir que des lignes spécifiques de notre table
  - **WHERE** permet de spécifier les lignes à retourner
  - Syntaxe :
    ``` sql
    SELECT colonne1,colonne2 FROM table WHERE conditions;
    ```
  - La clause **WHERE** vient après la clause **FROM**
  - Les conditions sont utilisées pour filtrer les lignes à retourner
  - **MySQL** fournit des opérateurs pour construire les conditions
  - #####Les opérateurs de comparaison
    - Arithmétiques
  
      | Opérateur | Description |
      |-----------|-------------|
      |  <  |  inférieur à  |
      |  >  |  supérieur à  |
      |  <=  |  inférieur ou égal à  |
      |  >=  |  supérieur ou égal à  |
      |  =  |  égal à  |
      |  <> ou !=  |  différent de  |

    - Opérateurs logiques

      | Opérateur | Description |
      |-----------|-------------|
      |  AND  |  Opérateur logique ET  |
      |  OR  |  Opérateur logique OU  |

    - Plage de valeurs

      | Opérateur | Description |
      |-----------|-------------|
      |  BETWEEN valeur1 AND valeur2  |  entre valeur1 et valeur2  |
  - *Exemple* : <br />
    *exemple 1* :
    ``` sql
    SELECT first_name,last_name FROM customer WHERE first_name='christian';
    ```
    *exemple 2* :
    ``` sql
    SELECT first_name,last_name FROM customer WHERE first_name='christian' AND last_name='jung';
    ```
    *exemple 3* :
    ``` sql
    SELECT first_name,last_name FROM payment WHERE first_name='christian' OR first_name='david';
    ```
- #### AS (alias)
  - AS est utilisée pour renommer temporairement une colonne ou une table dans une requête.
  - Cette astuce est utile pour faciliter la lecture des requêtes
  - Syntaxe :
    ``` sql
    SELECT colonne1 AS 'Colonne 1',colonne2 AS 'Colonne 2' FROM table;
    ```
  - *Exemple* :
    ``` sql
    SELECT first_name AS 'Prenom du Client',last_name AS 'Nom du Client' FROM customer;
    ```
- #### La fonction COUNT
  - La fonction **COUNT** retourne le nombre de lignes dans une table qui répondent aux conditions de la requêtes
  - Syntaxe :
    ``` sql
    SELECT COUNT(*) FROM table;
    ```
  - On peut aussi spécifier une colonne
  - Syntaxe :
    ``` sql
    SELECT COUNT(colonne1) FROM table;
    ```
  - La fonction **COUNT** ne prend pas en compte les valeurs **NULL**
  - On peut utiliser la fonction **COUNT** avec **DISTINCT**
  - *Exemple* :
    ``` sql
    SELECT COUNT(DISTINCT amount) FROM payment;
    ```
- #### LIMIT
  - **LIMIT** est à utiliser dans une requête SQL pour spécifier le nombre maximum de résultats que l'on souhaite obtenir
  - Pratique quand on souhaite avoir toutes les colonnes, mais toutes les lignes
  - Arrive a la fin de la requête
  - Syntaxe :
    ``` sql
    SELECT colonne1,colonne1 FROM customer LIMIT Nombre;
    ```
  - *Exemple 1* :
    ``` sql
    SELECT first_name,last_name FROM customer LIMIT 10;
    ```
- #### ORDER BY
  - **ORDER BY** permet de trier les lignes dans un résultat d'une requête SQL
  - Trier les données sur une plusieurs colonnes par order ascendant ou descendant
  - Syntaxe :
    ``` sql
    SELECT colonne1,colonne2 FROM table ORDER BY colone1;
    ```
  - Par défaut les résultats sont classés par order ascendant, toutefois il est possible d'inverser l'ordre en utilisant le suffixe ** DESC** après le nom de la colonne
  - Syntaxe :
    ``` sql
    SELECT colonne1,colonne2 FROM table ORDER BY colone1 DESC;
    ```
  - *Exemple* :
    ``` sql
    SELECT * FROM payment ORDER BY amount DESC;
    ```
- #### LIKE
  - **LIKE** est utilisé dans la clause **WHERE**
  - Ce mot-clé permet d'effectuer une recherche sur des valeurs qui :
    - Commencent par une ...
    - Contient ...
    - Se terminent par ...
  - Exemple :
    - On souhaite avoir les clients dont le prénom commence par **J**
    - Syntaxe :
      ``` sql
      SELECT colonne1,colonne2 FROM client WHERE colonne1 LIKE 'J%';
      ```
- #### IN
  - On utilise l'opérateur **IN** dans la clause **WHERE** pour vérifier si une valeur est égale à une des valeurs comprises dans une liste de valeurs déterminées
  - Syntaxe :
    ``` sql
    valeur IN (valeur1,valeur2);
    ```
  - On utilise l'opérateur **NOT IN** dans la clause **WHERE** pour vérifier si une valeur n'est égale à aucune des valeurs comprise dans une liste de valeurs déterminées
  - Syntaxe :
    ``` sql
    valeur NOT IN (valeur1,valeur2);
    ```
- BETWEEN
  - On utilise l'operateur **BETWEEN** dans la clause **WHERE** pour vérifier si une valeur est comprise dans une interval
  - Syntaxe :
    ``` sql
    valeur BETWEEN 3 AND 12;
    ```
  