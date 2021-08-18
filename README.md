# Apprendre le SQL
## Somaire
``` sql
- Les fondamentaux des requêtes SQL
- Jointures
- SQL Avancé: Fonctions et Sous-requêtes
- Création de bases et de tables
- Vues
```

Nous allons travailler sur la base de donnée SKILA :
page d'installation **[sakila-installation](https://dev.mysql.com/doc/sakila/en/sakila-installation.html)**.
### Structured Query Language
Le **SQL** (Structured Query Language) est un langage permettant de communiquer avec une base de données. Ce langage informatique est notamment très utilisé par les développeurs web pour communiquer avec les données d’un site web. SQL.sh recense des cours de SQL et des explications sur les principales commandes pour lire, insérer, modifier et supprimer des données dans une base.
### Les Fondamentaux de SQL
- #### SELECT
  - Une des tâches les plus récurrentes est d\'interroger une base de donnée en utilisant la declaration **SELECT**
  - Elle a beaucoup de clauses que vous pouvez combiner pour former une requête puissante
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
  - ##### Les opérateurs de comparaison
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
    SELECT first_name,last_name 
    FROM customer 
    WHERE first_name='christian';
    ```
    *exemple 2* :
    ``` sql
    SELECT first_name,last_name 
    FROM customer 
    WHERE first_name='christian' 
    AND last_name='jung';
    ```
    *exemple 3* :
    ``` sql
    SELECT first_name,last_name 
    FROM payment 
    WHERE first_name='christian' 
    OR first_name='david';
    ```
  - #### Savoir dans quel ordre sont utilisé chacun des commandes au sein d’une requête SELECT
    ``` sql
    SELECT *
    FROM table
    WHERE condition
    GROUP BY expression
    HAVING condition
    { UNION | INTERSECT | EXCEPT }
    ORDER BY expression
    LIMIT count
    OFFSET start
    ```
- #### AS (alias)
  - AS est utilisée pour renommer temporairement une colonne ou une table dans une requête.
  - Cette astuce est utile pour faciliter la lecture des requêtes
  - Syntaxe :
    ``` sql
    SELECT colonne1 AS 'Colonne 1',colonne2 AS 'Colonne 2' 
    FROM table;
    ```
  - *Exemple* :
    ``` sql
    SELECT first_name AS 'Prenom du Client',
        last_name AS 'Nom du Client' 
    FROM customer;
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
  - **ORDER BY** permet de trier les lignes dans un résultat d\'une requête SQL
  - Trier les données sur une plusieurs colonnes par order ascendant ou descendant
  - Syntaxe :
    ``` sql
    SELECT colonne1,colonne2 FROM table ORDER BY colone1;
    ```
  - Par défaut les résultats sont classés par order ascendant, toutefois il est possible d\'inverser l\'ordre en utilisant le suffixe **DESC** après le nom de la colonne
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
  - Ce mot-clé permet d\'effectuer une recherche sur des valeurs qui :
    - Commencent par une ...
    - Contient ...
    - Se terminent par ...
  - Exemple :
    - On souhaite avoir les clients dont le prénom commence par **J**
    - Syntaxe :
      ``` sql
      SELECT colonne1,colonne2 
      FROM client 
      WHERE colonne1 
      LIKE 'J%';
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
  - On utilise l\'opérateur **BETWEEN** dans la clause **WHERE** pour vérifier si une valeur est comprise dans un interval
  - Syntaxe :
    ``` sql
    valeur BETWEEN 3 AND 12;
    ```
  - **BETWEEN** remplace l\'utilisation de >= et <=
  - Syntaxe :
    ``` sql
    valeur >= 3 AND valeur <= 12;
    ```
  - On utilise l\'opérateur **NOT BETWEEN** dans la clause **WHERE** pour vérifier si une valeur n\'est pas comprise dans une interval
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
    SELECT customer_id,amount 
    FROM payment 
    WHERE amount 
    NOT BETWEEN 0 AND 2;
    ```
    Interval par date
    ``` sql
    SELECT DISTINCT customer_id,amount,payment_date 
    FROM payment 
    WHERE payment_date 
    BETWEEN '2005-05-01' AND '2005-06-29';
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
        SELECT customer_id,AVG(amount) 
        FROM payment 
        GROUP BY customer_id 
        ORDER BY 2 DESC;
        ```
      - *Exemple 2* :
        ``` sql
        SELECT staff_id,COUNT(*) 
        FROM payment 
        GROUP BY staff_id 
        ORDER BY 2 DESC;
        ```
      - *Exemple 3* :
        ``` sql
        SELECT rating,COUNT(rating) 
        FROM film 
        GROUP BY rating;
        ```
      - *Exemple 4* :
        ``` sql
        SELECT rating,ROUND(AVG(rental_rate),2) 
        FROM film 
        GROUP BY rating;
        ```
      - *Exemple 5* :
        ``` sql
        SELECT rental_duration,COUNT(rental_duration) 
        FROM film 
        GROUP BY rental_duration;
        ```
- HAVING
  - On utilise souvent la clause **HAVING** avec la clause **GROUP BY** pour filtrer les groupes de résultats qui ne satisfassent pas une condition précise
  - Syntaxe :
    ``` sql
    SELECT colonne1,fontion_agregation(colonne2) 
    FROM table 
    GROUP BY colonne1 
    HAVING condition;
    ```
  - **HAVING** est different de **WHERE**
  - **HAVING** appliquent des conditions sur les groupes de résultat créés par **GROUP BY** alors que **WHERE** appliquent des conditions sur les lignes individuelles
  - *Exemple* :
    - *Exemple 1* :
    ``` sql
    SELECT customer_id,SUM(amount) 
    FROM payment 
    GROUP BY customer_id 
    HAVING SUM(amount) > 200;
    ```
    - *Exemple 2* :
    ``` sql
    SELECT store_id,COUNT(customer_id) AS 'Nombre de client' 
    FROM customer 
    GROUP BY store_id 
    HAVING COUNT(customer_id) > 300;
    ```
    - *Exemple 3* :
    ``` sql
    SELECT rating, AVG(rental_rate) 
    FROM film 
    WHERE rating IN('PG','R','G') 
    GROUP BY rating 
    HAVING AVG(rental_rate)<3;
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
    SELECT * 
    FROM tabl1 
    RIGHT JOIN table2 
    ON table1.id=table2.id;
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
    SELECT * 
    FROM table1 
    INNER JOIN table2 
    ON table1.id=table2.id;
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
    SELECT * 
    FROM table1 
    LEFT JOIN table2 
    ON table1.id=table2.id;
    ```
  - *Exemple* :
    - *Exemple 1* :
      ``` sql
      SELECT f.film_id,f.title,i.inventory_id 
      FROM film f 
      LEFT JOIN inventory i 
      ON i.film_id = f.film_id;
      ```
    - *Exemple 2* :
      ``` sql
      SELECT f.film_id,f.title,i.inventory_id
      FROM film f 
      LEFT JOIN inventory i 
      ON i.film_id = f.film_id
      WHERE i.film_id IS NULL
      ORDER BY f.title;
      ```
    - *Exemple 3* :
      ``` sql
      SELECT f.film_id,f.title,i.inventory_id
      FROM film f 
      LEFT JOIN inventory i 
      ON i.film_id = f.film_id
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
### Sous-requêtes
  - Consiste à exécuter une requête à l\'intérieur d\'une autre requête
  - Souvent utilisée au sein d\'une clause **WHERE** ou de **HAVING** pour remplacer une ou plusieurs constantes
  - Supposons que nous voulions trouver les films dont le tarif de location est supérieur au taux de location moyen
  - Nous pouvons le faire en deux étapes :
    - Rechercher le tarif de location moyenne (AVG)
    - Utiliser le résultat de la première requete dans la deuxième instruction **SELECT** pour trouver les films que vous souhaitez
  - Pour contruire une sous-requête, nous plaçons la seconde requête entre paranthèses et nous l\'utilisons dans la clause **WHERE** en tant qu\'expression
  - Syntaxe :
    ``` sql
    SELECT colonne1,colonne2,colonne3 
    FROM table
    WHERE rental_rate > (SELECT AVG(colonne3) FROM table);
    ```
  - *Exemple* :
    ``` sql
    SELECT film_id,title,rental_rate
    FROM film
    WHERE rental_rate > (SELECT AVG(rental_rate) FROM film);
    ```
### Création et modification des tables
  - Objectifs de cette section :
  ``` sql
  - Types de données
  - Clé primaire (PRIMARY KEY) et clé étrangère (FOREIGN KEY)
  - CREATE TABLE
  - INSERT - UPDATE - DELETE
  - ALTER TABLE - DROP TABLE
  - Contraintes
  ```
  - ### TYPES DE DONNÉES
  - MySQL supporte principalement les types de données suivants :
    - Boolean
    - Caractère
    - Nombre
    - Date
  - ### Types de données : Boolean
    - Un boolean peut contenir une des deux valeurs possible : **TRUE** ou **FALSE**. Dans le cas ou la valeur n\est pas connue, la valeur **NULL** est utilisée
    - Quand on déclare une colonne qui contient des boolean, on utilise le mot-clé **boolean**
    - Quand on insert une donnée dans une colonne de type **Boolean**, MySQL va la convertir en valeur Boolean
    - *Exemple* :
      - > 1, yes, y, t, true vont être convertis en true
      - > O, no, n, false vont être convertis en false
    - Quand on sélectionne une donnée d\'une colonne **BOOLEAN**, MySQL affiche t pour true et f pour false et espace pour **NULL**
  - ### Types de données : Caractère
    - Un seul caractère : **char**
    - Une chaîne de caractère de longueur fixe : **char(n)**. Si on insère une donnée de longueur inférieure a n, MySQL va compléter avec des espaces. Si la longueur est superieur a n, MySQL renvoie une erreur
    - Une chaîne de caractère de longueur variable : **varchar(n)**. On peut y stocker des données jusqu\'a n caractère. MySQL ne complètera pas avec des espaces si la longueur est inférieur a n
  - ### Types de données : Nombre
    - **Small Integer** : entier de 2-byte qui peut contenir des valeurs de **-32768** a **32767**
    - **Integer** (**int**) : entier de 4-byte qui peut contenir des valeurs de **-214783648** a **214783648**
    - **float(n)** : Un petit nombre avec un point decimal flottant. Le nombre maximum de chiffres peut être spécifié dans le paramètre **n**
    - **double(n)** : Un grand nombre avec un point décimal flottant. Le nombre maximum de chiffres peut être spécifié dans le paramètre **n**
  - ### Clé Primaire et Clé Étrangère
  - #### La clé primaire
    - Une clé primaire est une colonne utilisée pour identifier une ligne unique dans la table
    - On définit les clés primaires par le biais de contraintes de clé primaire
    - Une table peut avoir une seule clé primaire
    - C'est une bonne pratique de mettre une clé primaire a chaque table
    - Quand on ajoute une clé primaire, MySQL crée un index unique sur la colonne utilisée pour définir la clé primaire
  - On ajoute la clé primaire a une table pendant la création de cette table en utilisant la clause **CREATE TABLE**
  - Syntaxe :
    ``` sql
    CREATE TABLE nom_de_la_table(
        nom_colonne1 type_donnees PRIMARY KEY,
        nom_colonne2 type_donnees,
        nom_colonne3 type_donnees
    );
    ```
  - #### La clé étrangère
    - Une clé étrangère identifie une colonne ou un ensemble de colonnes d\'une table comme référençant une colonne ou un ensemble de colonnes d\'une autre table (la table référencée ou la table parent)
    - En d\'autre mot, une clé étrangère est définie dans une table pour faire référence a une clé primaire dans une autre table
    - Une table peut avoir plusieurs clés étrangères dans sa relation avec d\'autres tables
    - Dans MySQL, on définit une clé étrangère par le biais d\'une contrainte **Clé Étrangère**
    - Une **Clé Étrangère indique que les valeurs d\'une colonne dans la table référencée sont les mêmes que dans la table référencent
    - Pour créer une nouvelle table dans MySQL, on utilise la clause **CREATE TABLE**
    - Syntaxe :
      ``` sql
      CREATE TABLE nom_table(
      nom_colonne TYPE contraint_colonne,
      contraint_table)
      INHERITS nom_table_existante;
      ```
      > *INHERITS clause optionnelle*
    #### Contrainte de Colonne
    - **NOT NULL** : la valeur de la colonne ne peut pas être **NULL**
    - **UNIQUE** : la valeur de la colonne doit être unique dans toute la table
    - **PRIMARY KEY** : cette contrainte est une combinaison de **UNIQUE** et **NOT NULL**
    - Vous pouvez définir une colonne en tant que clé primaire en utilisant une contrainte au niveau de la colonne. Si la clé primaire contient plusieurs colonnes, vou devez utiliser la contrainte au niveau de la table
    - **CHECK** : permet de vérifier une condition quand on insère ou met à jour une donnée
    - *Exemple* : 
      - Les valeurs de la colonne prix de table produit doivent être positives
    - **REFERENCES** : contraint la valeur de la colonne qui existe dans une colonne d\'une autre table
    #### Contrainte de Table
    - **UNIQUE(list_colonne)** : forcer les valeurs de la liste des colonnes entre parenthèses d'\être uniques
    - **PRIMARY KEY(list_colonne)** : définir la clé primaire composée de plusieurs colonnes
    - **CHECK(condition)** : vérifier une condition lors de l\'insertion ou de la mise à jour de données
    - **REFERENCES** : contraint la valeur de la colonne qui existe dans une colonne d\'une autre table
    - *Exemple* :
      - Création de la table **account**
        ``` sql
        CREATE TABLE account(
        user_id INT PRIMARY KEY,
        username VARCHAR(50) UNIQUE NOT NULL,
        password VARCHAR(50) NOT NULL,
        email VARCHAR(355) UNIQUE NOT NULL,
        created_at TIMESTAMP NOT NULL,
        last_login TIMESTAMP
        );
        ```
      - Création de la table **role**
        ``` sql
        CREATE TABLE role(
        role_id INT PRIMARY KEY,
        role_name VARCHAR(255) UNIQUE NOT NULL
        );
        ```
      - Création de la table **account_role**
        ``` sql
        CREATE TABLE account_role(
        user_id INT NOT NULL,
        role_id INT NOT NULL,
        grant_date TIMESTAMP,
        PRIMARY KEY (user_id,role_id)
        );
        ```
  ### INSERT
  - Quand on crée une table, elle est vide
  - La première chose à faire est d\'insérer des données dans cette table
  - On utilise la clause **INSERT** pour insérer des données dans la table
  - On peut insérer une ligne ou plusieurs lignes d\'un coup
  - Syntaxe :
    ``` sql
    INSERT INTO table(colonne1,colonne2,...)
    VALUES(valeur1,valeur2,...);
    ```
  - On spécifie le nom de la table dans laquelle on souhaite insérer des données. Entre parenthèse, on indique la liste des colonnes
  - On indique la liste des valeurs entre parenthèses précédée par **VALUES**
  - Pour ajouter plusieurs lignes à la fois
  - Syntaxe :
    ``` sql
    INSERT INTO table(colonne1,colonne2,...)
    VALUES(valeur1,valeur2,...),
          (valeur1,valeur2),...;
    ```
  - *Exemple* :
    - Insérer qu\'une ligne
      ``` sql
      INSERT INTO lien(url, name, description)
      VALUES ('www.jobkids.com','Job Kids','Job Kids met en relation les entreprises est les particulier.');
      ```
    - Insérer plusieurs lignes
      ``` sql
      INSERT INTO lien(url, name, description)
      VALUES ('www.amazon.fr','Amazon','Amazon est un site e-commerce.'),
             ('www.google.com','Google','Google moteur de recherche.');
      ```
  - Pour copier la structure d\'une table
  - Syntaxe :
    ``` sql
    CREATE TABLE nouvelle_table LIKE ancienne_table;
    ```
  - Exemple :
    ``` sql
    CREATE TABLE lien_copy LIKE lien;
    ```
  - Insérer une donnée de l\'ancienne table
  - *Exemple* :
    ``` sql
    INSERT INTO lien_copy
    SELECT * FROM lien WHERE name='Be Secured';
    ```
  ### UPDATE
  - Pour changer la valeur d\'une colonne, on utilise la clause **UPDATE**
  - Syntaxe :
    ``` sql
    UPDATE table SET colonne1=valeur1,colonne2=valeur2 WHERE condition;
    ```
  - *Exemple* :
    ``` sql
    UPDATE lien SET description='BeSecured est une société des prestations informatique.'
    WHERE name='Be Secured';
    ```
  ### DELETE
  - Pour supprimer des lignes d\'une table, on utilise la clause **DELETE**
  - Syntaxe :
    ``` sql
    DELETE FROM table WHERE condition;
    ```
  - La clause **DELETE** retourne le nombre de lignes supprimées
  - Si aucune ligne n\'est supprimé, clause **DELETE** retourne 0
  - *Exemple* :
    ``` sql
    DELETE FROM lien WHERE lien.ID<>1;
    ```
  ### ALTER TABLE
  - Pour changer la structure d\'une table existante, on utilise la clause **ALTER TABLE**
  - Syntaxe :
    ``` sql
    ALTER TABLE nom_table action;
    ```
  - **MySQL** fournit plusieurs actions qui permettent de :
    - **Ajouter**, **supprimer** ou **renommer** une colonne
    - Mettre une valeur par défaut our une colonne
    - Ajouter une contrainte **CHECK** à une colonne
    - Renommer une table
  - Les mots-clés à utiliser sont :
    > - **ADD COLUMN**
    > - **DROP COLUMN**
    > - **RENAME COLUMN**
    > - **ADD CONSTRAINT**
    > - **RENAME TO**
  - *Exemple* :
    ``` sql
    SELECT * FROM lien;
    ALTER TABLE lien ADD COLUMN active boolean;
    DESCRIBE lien;
    ALTER TABLE lien DROP COLUMN active;
    DESCRIBE lien;
    ALTER TABLE lien RENAME COLUMN name TO nom;
    ALTER TABLE lien RENAME TO table_des_websites;
    SELECT * FROM table_des_websites;
    ```
  ### DROP TABLE
  - Pour supprimer une table existante de la base de données, on utilise la clause **DROP TABLE**
  - Syntaxe :
    ``` sql
    DROP TABLE [IF EXISTS] nom_table;
    ```
  - **IF EXISTS** est optionnelle, elle permet de vérifier si la table existe avant de la supprimer. Cela permet d\'éviter des erreurs
  - *Exemple* :
    ``` sql
    DROP TABLE table_des_websites;
    ```
    ou
    ``` sql
    DROP TABLE IF EXISTS table_des_websites;
    ```
    ou
    ``` sql
    DROP TABLE IF EXISTS table_des_websites CASCADE;
    ```
### VUE
  - Une **VUE** est un objet stocké de base de données
  - Une **VUE** est table virtuelle dans **MySQL**
  - Une **VUE** est une représentation des données d\'une ou plusieurs tables sous-jacentes
  - Une **VUE** est un objet stocké de base de données représentant une requête
  - Une **VUE** simplifie la complexité d\'une requête
  - Comme pour les tables, on peut donner des droits aux utilisateurs sur la VUE
  - La **VUE** montre simplement le résultat d\'une requête SQL spécifique
  - Syntaxe :
    ``` sql
    CREATE VIEW nom_de_la_vue AS (SELECT ...);
    ```
  - *Exemple* :
    ``` sql
    CREATE VIEW info_client AS (
        SELECT first_name,last_name,email,address,phone
        FROM customer c
        JOIN address a
        ON c.address_id = a.address_id
    );
    
    SELECT * FROM info_client;
    ```
    - #### Renommer une **VUE**
      - Syntaxe :
        ``` sql
        RENAME TABLE ancien_nom TO nouveau_nom;
        ```
      - *exemple* :
        ``` sql
        RENAME TABLE info_client TO clients;
        ```
      - #### Supprimer une **VUE**
        - Syntaxe :
        ``` sql
        RENAME TABLE ancien_nom TO nouveau_nom;
        ```
        - *exemple* :
        ``` sql
        RENAME TABLE info_client TO clients;
        ```
## License

GNU

**Christian KABASELE, SQL**