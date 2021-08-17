# Apprendre le SQL
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
### Les Fondamentaux de SQL
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
- #### BETWEEN
  - On utilise l'operateur **BETWEEN** dans la clause **WHERE** pour vérifier si une valeur est comprise dans un interval
  - Syntaxe :
    ``` sql
    valeur BETWEEN 3 AND 12;
    ```
  - **BETWEEN** remplace l'utilisation de >= et <=
  - Syntaxe :
    ``` sql
    valeur >= 3 AND valeur <= 12;
    ```
  - On utilise l'opérateur ** NOT BETWEEN** dans la clause **WHERE** pour vérifier si une valeur n'est pas comprise dans une interval
  - Syntaxe :
    ``` sql
    valeur NOT BETWEEN 3 AND 12;
    ```
  - *Exemple* :
    ``` sql
    SELECT customer_id,amount FROM payment WHERE amount BETWEEN 0 AND 2;
    ```
    Avec **NOT BETWEEN**
    ``` sql
    SELECT customer_id,amount FROM payment WHERE amount NOT BETWEEN 0 AND 2;
    ```
    Interval par date
    ``` sql
    SELECT DISTINCT customer_id,amount,payment_date FROM payment WHERE payment_date BETWEEN '2005-05-01' AND '2005-06-29';
    ```
- #### Fonctions d'agrégation
  - AVG() = Average
  - MIN() = Minimum
  - MAX() = Maximum
  - SUM() = La somme
  - *Exemple* :
    - Avec **AVG**
      ``` sql
      SELECT ROUND(AVG(amount), 2) FROM payment;
      ```
    - Avec **MIN**
      ``` sql
      SELECT MIN(amount) FROM payment;
      ```
    - Avec **MAX**
      ``` sql
      SELECT MAX(amount) FROM payment;
      ```
    - Avec **SUM**
      ``` sql
      SELECT SUM(amount) FROM payment;
      ```
  - #### GROUP BY
    - Un des outils les plus importants dans SQL
    - La clause **GROUP BY** permet de regrouper plusieurs résultats
    - Pour chaque groupe, on peut appliquer une fonction d'agrégation
    - *Exemple* :
      - Calculer la somme
      - compter le nombre d'éléments dans chaque groupe
    - Syntaxe :
      ``` sql
      SELECT colonne1,fonction_agregation(colonne2) FROM table GROUP BY colonne1;
      ```
    - *Exemple* :
      - *Exemple 1* :
        ``` sql
        SELECT customer_id,AVG(amount) FROM payment GROUP BY customer_id ORDER BY 2 DESC;
        ```
      - *Exemple 2* :
        ``` sql
        SELECT staff_id,COUNT(*) FROM payment GROUP BY staff_id ORDER BY 2 DESC;
        ```
      - *Exemple 3* :
        ``` sql
        SELECT rating,COUNT(rating) FROM film GROUP BY rating;
        ```
      - *Exemple 4* :
        ``` sql
        SELECT rating,ROUND(AVG(rental_rate),2) FROM film GROUP BY rating;
        ```
      - *Exemple 5* :
        ``` sql
        SELECT rental_duration,COUNT(rental_duration) FROM film GROUP BY rental_duration;
        ```
- HAVING
  - On utilise souvent la clause **HAVING** avec la clause **GROUP BY** pour filtrer les groupes de résultats qui ne satisfassent pas une condition précise
  - Syntaxe :
    ``` sql
    SELECT colonne1,fontion_agregation(colonne2) FROM table GROUP BY colonne1 HAVING condition;
    ```
  - **HAVING** est different de **WHERE**
  - **HAVING** appliquent des conditions sur les groupes de résultat créés par **GROUP BY** alors que **WHERE** appliquent des conditions sur les lignes individuelles
  - *Exemple* :
    - *Exemple 1* :
    ``` sql
    SELECT customer_id,SUM(amount) FROM payment GROUP BY customer_id HAVING SUM(amount) > 200;
    ```
    - *Exemple 2* :
    ``` sql
    SELECT store_id,COUNT(customer_id) AS 'Nombre de client' FROM customer GROUP BY store_id HAVING COUNT(customer_id) > 300;
    ```
    - *Exemple 3* :
    ``` sql
    SELECT rating, AVG(rental_rate) FROM film WHERE rating IN('PG','R','G') GROUP BY rating HAVING AVG(rental_rate)<3;
    ```
### Les Jointures
  ``` sql
  - Combiner plusieurs tables utilisants JOIN
  - Type de jointures
  - Union
  ```
- Sélectionner les données se trouvant dans plusieurs tables
    - Principe : Une jointure a lieu entre deux tables. Elle exprime une correspondance entre deux clés par un critère d'égalité
      - *Exemple* :
        - Pour lire l'adresse correspondant à chaque personne, il faut faire une jointure entre la table Personne et Adresse
        
        | Personne |
        |----------|
        |ID  int   |
        |Nom  varchar(30)   |
        |Prenom  varchar(30)   |
        |Adress#  int   |

        | Adresse |
        |----------|
        |ID  int   |
        |Voie  varchar(200)   |
        |CP  int   |
        |Ville  varchar(50)   |
- #### OUTER JOIN / RIGHT JOIN
  - Permet de retourner tous les enregistrements de la table de droite (right = droite) même s'il n'y a pas de correspondance avec la table de gauche
  - Syntaxe :
    ``` sql
    SELECT * FROM tabl1 RIGHT JOIN table2 ON table1.id=table2.id;
    ```
  - *Exemple* :
    ``` sql
    SELECT
       c.customer_id,
       c.first_name,
       c.last_name,
       a.actor_id,
       a.first_name,
       a.last_name 
    FROM customer c
    RIGHT JOIN actor a
    ON c.last_name = a.last_name;
    ```
- #### INNER JOIN
  - Permets de lier plusieurs tables entre-elles
  - Retourne les enregistrements lorsqu'il y a au moins une ligne dans chaque colonne qui correspond à la condition
  - Syntaxe :
    ``` sql
    SELECT * FROM table1 INNER JOIN table2 ON table1.id=table2.id;
    ```
  - *Exemple* :
    ``` sql
    SELECT
       c.customer_id,
       c.first_name,
       c.last_name,
       c.email,
       p.amount,
       p.payment_date
    FROM customer c
    INNER JOIN payment p ON c.customer_id = p.customer_id
    WHERE first_name LIKE 'H%';
    ```
- #### OUTER JOIN / LEFT JOIN
  - Permet de lister tous les résultats de la table de gauche (left = gauche) même s'il n'y a pas de correspondance dans la deuxième tables
  - Syntaxe :
    ``` sql
    SELECT * FROM table1 LEFT JOIN table2 ON table1.id=table2.id;
    ```
  - *Exemple* :
    - *Exemple 1* :
      ``` sql
      SELECT f.film_id,f.title,i.inventory_id FROM film f LEFT JOIN inventory i ON i.film_id = f.film_id;
      ```
    - *Exemple 2* :
      ``` sql
      SELECT f.film_id,f.title,i.inventory_id
      FROM film f LEFT JOIN inventory i ON i.film_id = f.film_id
      WHERE i.film_id IS NULL
      ORDER BY f.title;
      ```
    - *Exemple 3* :
      ``` sql
      SELECT f.film_id,f.title,i.inventory_id
      FROM film f LEFT JOIN inventory i ON i.film_id = f.film_id
      WHERE i.inventory_id IS NULL
      ORDER BY f.title;
      ```
### Types de jointures
  - INNER JOIN
  - RIGHT JOIN
  - FULL JOIN
  - LEFT JOIN
  - #### UNION
    - Permet de mettre bout-à-bout les résultats de plusieurs requêtes utilisant elles-même la commande SELECT
    - Permet de concaténer les résultats de deux requêtes ou plus
    - `Condition` : chacune des requêtes à concaténer retournes le même nombre de colonnes, avec les mêmes types de données et dans le même ordre
    - Syntaxe :
      ``` sql
      SELECT * FROM table1 UNION SELECT * FROM table2:
      ```
## SQL Avancés 
  ``` sql
  - Fonctions mathématiques
  - Fonctions de dates et heure
  - Fonctions et opérateurs de chaîne de caractère
  - Sous-requêtes
  ```
- ### Fonctions de dates et heures
  - SQL permet d\'utiliser des données de type *Date* et *Heure*
  - Plus tard, nous allons voir comment créer ce type de données
  - Ici, on va se focaliser sur l\'extraction des informations de ces données
  - La fonction **EXTRACT()** extrait une partie d\'une date donnée
  - On peut extraire tout type d\'information
  - *Exemple* :
    ``` sql
    SELECT EXTRACT(MONTH FROM '2017-06-15');
    ```
  - Syntaxe :
    ``` sql
    EXTRACT(part FROM date);
    ```
    - #### PART :
      > -  MICROSECOND
      > -  SECOND
      > -  MINUTE
      > -  HOUR
      > -  DAY
      > -  WEEK
      > -  MONTH
      > -  QUARTER
      > -  YEAR
      > -  SECOND-MICROSECOND
      > -  MINUTE-MICROSECOND
      > -  MINUTE-SECOND
      > -  HOUR-MICROSECOND
      > -  HOUR-SECOND
      > -  HOUR-MINUTE
      > -  DAY-MICROSECOND
      > -  DAY-SECOND
      > -  DAY-MINUTE
      > -  DAY-HOUR
      > -  YEAR_MONTH
    - Se référer a : <br />
      **[Function MySQL Extract](https://www.w3schools.com/mysql/func_mysql_extract.asp)**
    - *Exemple* :
      - *Exemple 1* :
        ``` sql
        SELECT EXTRACT(day FROM payment_date) FROM payment;
        ```
      - *Exemple 2* :
        ``` sql
        SELECT EXTRACT(month FROM payment_date) FROM payment;
        ```
      - *Exemple 3* :
        ``` sql
        SELECT EXTRACT(year FROM payment_date) FROM payment;
        ```
      - *Exemple 4* :
        ``` sql
        SELECT DISTINCT EXTRACT(year FROM payment_date) AS 'Année' FROM payment;
        ```
      - *Exemple 5* :
        ``` sql
        SELECT EXTRACT(month FROM payment_date) AS 'Mois',
        SUM(amount)
        FROM payment
        GROUP BY EXTRACT(month FROM payment_date)
        ORDER BY 1 ASC;
        ```
      - *Exemple 6* :
        ``` sql
        SELECT EXTRACT(month FROM payment_date) AS 'Mois',
        SUM(amount)
        FROM payment
        GROUP BY Mois
        ORDER BY 1 ASC;
        ```
### Fonctions Mathématique
  - SQL fournit plusieurs opérateurs mathématiques permettant de manipuler les colonnes de type numérique
  - Pour avoir la liste de ces opérateurs :
    **[Mathematical functions](https://dev.mysql.com/doc/refman/8.0/en/numeric-functions.html)**
  - ### Opérateurs arithmétiques
  
  |Nom|Description|
  |----|----|
  |%, MOD|Modulo operator|
  |*|Multiplication operator|
  |+|Addition operator|
  |-|Minus operator|
  |-|Change the sign of the argument|
  |/|Division operator|
  |DIV|Integer division|
  - *Exemple* :
    - *Exemple 1* :
      ``` sql
      SELECT EXTRACT(month FROM payment_date) AS 'Mois',
       SUM(amount/100)
      FROM payment
      GROUP BY Mois
      ORDER BY 1 ASC;
      ```
    - *Exemple 2* :
      ``` sql
      SELECT EXTRACT(month FROM payment_date) AS 'Mois',
       SUM(amount*2)
      FROM payment
      GROUP BY Mois
      ORDER BY 1 ASC;
      ```
    - *Exemple 3* :
      ``` sql
      SELECT EXTRACT(month FROM payment_date) AS 'Mois',
       SUM(amount+20)
      FROM payment
      GROUP BY Mois
      ORDER BY 1 ASC;
      ```
    - *Exemple 4* :
      ``` sql
      SELECT ROUND(AVG(amount)) FROM payment;
      ```
### Fonctions de chaînes de caractères
  - SQL fournit plusieurs opérateurs permettant de manipuler les colonnes de type chaînes de caractères
  - Pour avoir la liste de ces opérateurs :
  **[String functions](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)**
  - 