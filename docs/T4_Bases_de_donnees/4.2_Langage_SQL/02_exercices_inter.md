# Exercices SQL interactifs



{{initexo(0)}}



!!! abstract "{{ exercice() }}"
    *Questions interactives à réaliser sur le site sqlzoo.net.*

    **Q1.** Travail sur SELECT, (base de données Nobel) :arrow_right: [ici](https://sqlzoo.net/wiki/SELECT_from_Nobel_Tutorial){. target="_blank"}.

    ??? note "Correction"
        Corrections extraites du dépôt *https://github.com/jisaw/sqlzoo-solutions*.
        ```SQL
        /*
        Third section of sqlzoo, SELECT from Nobel
        */

        --#1
        /*
        Change the query shown so that it displays Nobel prizes for 1950.
        */
        SELECT yr, subject, winner
        FROM nobel
        WHERE yr = 1950

        --#2
        /*
        Show who won the 1962 prize for Literature.
        */
        SELECT winner
        FROM nobel
        WHERE yr = 1962 AND subject = 'Literature'

        --#3
        /*
        Show the year and subject that won 'Albert Einstein' his prize.
        */
        SELECT yr, subject
        FROM nobel
        WHERE winner = 'Albert Einstein'

        --#4
        /*
        Give the name of the 'Peace' winners since the year 2000, including 2000.
        */
        SELECT winner
        FROM nobel
        WHERE subject = 'Peace' AND yr >= 2000

        --#5
        /*
        Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive
        */
        SELECT yr, subject, winner
        FROM nobel
        WHERE (yr >=1980 AND yr <=1989) AND subject = 'Literature'

        --#6
        /*
        Show all details of the presidential winners:

        Theodore Roosevelt
        Woodrow Wilson
        Jimmy Carter
        */
        SELECT *
        FROM nobel
        WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter')

        --#7
        /*
        Show the winners with first name John
        */
        SELECT winner
        FROM nobel
        WHERE winner LIKE 'john%'

        --#8
        /*
        Show the Physics winners for 1980 together with the Chemistry winners for 1984.
        */
        SELECT *
        FROM nobel
        WHERE (subject = "Physics" AND yr = '1980') OR (subject = 'Chemistry' AND yr = 1984)

        --#9
        /*
        Show the winners for 1980 excluding the Chemistry and Medicine
        */
        SELECT *
        FROM nobel
        WHERE yr = 1980 AND subject NOT IN ('Chemistry', 'Medicine')

        --#10
        /*
        Show who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)
        */
        SELECT *
        FROM nobel
        WHERE (subject  = 'Medicine' AND yr < 1910) OR (subject = 'Literature' AND yr >= 2004)

        --#11
        /*
        Find all details of the prize won by PETER GRÜNBERG
        */
        SELECT *
        FROM nobel
        WHERE winner LIKE 'peter gr%nberg'

        --#12
        /*
        Find all details of the prize won by EUGENE O'NEILL
        */
        SELECT *
        FROM nobel
        WHERE winner = 'Eugene O''Neill'

        --#13
        /*
        Knights in order

        List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.
        */
        SELECT winner, yr, subject
        FROM nobel
        WHERE winner LIKE 'sir%'
        ORDER BY yr DESC, winner

        --#14
        /*
        The expression subject IN ('Chemistry','Physics') can be used as a value - it will be 0 or 1.

        Show the 1984 winners ordered by subject and winner name; but list Chemistry and Physics last.
        */
        SELECT winner, subject, subject IN ('Physics','Chemistry')
        FROM nobel
        WHERE yr=1984
        ORDER BY subject IN ('Physics','Chemistry'),subject,winner
        ```

    **Q2.** Travail sur SUM et COUNT, (base de données World) :arrow_right: [ici](https://sqlzoo.net/wiki/SUM_and_COUNT){. target="_blank"}. (jusqu'à la question 5.)

    ??? note "Correction"
        Corrections extraites du dépôt *https://github.com/jisaw/sqlzoo-solutions*.
        ```SQL
        /*
        Fifth section of sqlzoo, SUM and COUNT
        */


        --#1
        /*
        Show the total population of the world.
        */
        SELECT SUM(population)
        FROM world

        --#2
        /*
        List all the continents - just once each.
        */
        SELECT DISTINCT(continent)
        FROM world

        --#3
        /*
        Give the total GDP of Africa
        */
        SELECT SUM(gdp)
        FROM world
        WHERE continent = 'Africa'

        --#4
        /*
        How many countries have an area of at least 1000000
        */
        SELECT COUNT(name)
        FROM world
        WHERE area >= 1000000

        --#5
        /*
        What is the total population of ('France','Germany','Spain')
        */
        SELECT SUM(population)
        FROM world
        WHERE name IN ('France', 'Germany', 'Spain')

        --#6
        /*
        For each continent show the continent and number of countries.
        */
        SELECT continent, COUNT(name)
        FROM world
        GROUP BY continent


        --#7
        /*
        For each continent show the continent and number of countries with populations of at least 10 million.
        */
        SELECT continent, COUNT(name)
        FROM world
        WHERE population >= 10000000
        GROUP BY continent

        --#8
        /*
        List the continents that have a total population of at least 100 million.
        */
        SELECT continent
        FROM world
        GROUP BY continent
        HAVING SUM(population) > 100000000
        ```

    **Q3.** Travail sur JOIN, (base de données Euro2012) :arrow_right: [ici](https://sqlzoo.net/wiki/The_JOIN_operation){. target="_blank"}.

    ??? note "correction"
        ```SQL
        /*
        Sixth section of sqlzoo, Join
        */


        --#1
        /*
        The first example shows the goal scored by 'Bender'.

        Show matchid and player name for all goals scored by Germany.
        */
        SELECT matchid, player FROM goal
        WHERE teamid = 'GER'

        --#2
        /*
        From the previous query you can see that Lars Bender's goal was scored in game 1012. Notice that the column matchid in the goal table corresponds to the id column in the game table.

        Show id, stadium, team1, team2 for game 1012
        */
        SELECT id,stadium,team1,team2
        FROM game
        WHERE id = 1012

        --#3
        /*
        You can combine the two steps into a single query with a JOIN. You will get all the game details and all the goal details if you use

        SELECT *
          FROM game JOIN goal ON (id=matchid)
        Show the player, teamid and mdate and for every German goal. teamid='GER'
        */
        SELECT player, teamid, mdate
        FROM game
          JOIN goal ON (id=matchid AND teamid='GER')

        --#4
        /*
        Use the same JOIN as in the previous question.

        Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'
        */
        SELECT team1, team2, player
        FROM game
          JOIN goal ON (id=matchid AND player LIKE 'Mario%')

        --#5
        /*
        The table eteam gives details of every national team including the coach. You can JOIN goal to eteam using the phrase goal JOIN eteam on teamid=id

        Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10
        */
        SELECT player, teamid, coach, gtime
        FROM goal
          JOIN eteam ON (teamid=id AND gtime<=10)

        --#6
        /*
        To JOIN game with eteam you could use either
        game JOIN eteam ON (team1=eteam.id) or game JOIN eteam ON (team2=eteam.id)

        Notice that because id is a column name in both game and eteam you must specify eteam.id instead of just id

        List the the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
        */
        SELECT mdate, teamname
        FROM game
          JOIN eteam ON (team1=eteam.id AND coach LIKE '%Santos')

        --#7
        /*
        List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
        */
        SELECT player
        FROM goal
          JOIN game ON (id=matchid AND stadium = 'National Stadium, Warsaw')

        --#8
        /*
        The example query shows all goals scored in the Germany-Greece quarterfinal.
        Instead show the name of all players who scored a goal against Germany.
        */
        SELECT DISTINCT(player)
        FROM game
          JOIN goal ON matchid = id
        WHERE ((team1='GER' OR team2='GER') AND teamid != 'GER')

        --#9
        /*
        Show teamname and the total number of goals scored.
        */
        SELECT teamname, COUNT(player)
        FROM eteam
          JOIN goal ON id=teamid
        GROUP BY teamname

        --#10
        /*
        Show the stadium and the number of goals scored in each stadium.
        */
        SELECT stadium, COUNT(player) AS goals
        FROM game
          JOIN goal ON (id=matchid)
        GROUP BY stadium

        --#11
        /*
        For every match involving 'POL', show the matchid, date and the number of goals scored.
        */
        SELECT matchid, mdate, COUNT(player) AS goals
        FROM game
          JOIN goal ON (matchid=id AND (team1 = 'POL' OR team2 = 'POL'))
        GROUP BY matchid, mdate

        --#12
        /*
        For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
        */
        SELECT id, mdate, COUNT(player)
        FROM game
          JOIN goal ON (id=matchid AND (team1 = 'GER' OR team2 = 'GER') AND teamid='GER')
        GROUP BY id, mdate

        --#13
        /*
        List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.
        mdate	team1	score1	team2	score2
        1 July 2012	ESP	4	ITA	0
        10 June 2012	ESP	1	ITA	1
        10 June 2012	IRL	1	CRO	3
        ...
        Notice in the query given every goal is listed. If it was a team1 goal then a 1 appears in score1, otherwise there is a 0.
        You could SUM this column to get a count of the goals scored by team1. Sort your result by mdate, matchid, team1 and team2.
        */
        SELECT mdate,
               team1,
               SUM(CASE WHEN teamid = team1 THEN 1 ELSE 0 END) AS score1,
               team2,
               SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score2 FROM
            game LEFT JOIN goal ON (id = matchid)
            GROUP BY mdate,team1,team2
            ORDER BY mdate, matchid, team1, team2
        ```

!!! abstract "{{ exercice() }}"
    Gestion d'un réseau d'agences de location de voitures.   
    *D'après le travail de J. Le Coupanec (Académie de Rennes)*

    La base de données [locations.db](data/locations.db) contient les tables ```Agences```,```Locations```, ```Vehicules```.
    ![](data/diag_locations.png)

    {!{ sqlide titre="**Requête :**"  base="T4_Bases_de_donnees/4.2_Langage_SQL/data/locations.db" }!}

    ??? note "Questions sur la relation ```Agences```"

        **Q1**. Visualisez toute la relation ```Agences```

        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT * 
            FROM Agences
            ```            
        """
        )
        }}


        **Q2**. Listez uniquement les noms des agences et de leur ville.

        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT nom, ville 
            FROM Agences
            ```           
        """
        )
        }}


        **Q3**. Listez les noms des agences de la ville de Lorient


        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT nom 
            FROM Agences
            WHERE ville = 'Lorient'
            ```            
        """
        )
        }}



        **Q4**. Listez les noms des agences du département du Morbihan (code postal 56***) ainsi que les codes postaux en utilisant par exemple un ```WHERE LIKE```.


        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT nom, code
            FROM Agences
            WHERE code LIKE '56%'
            ```            
        """
        )
        }}



    ??? note "Questions sur la relation ```Vehicules```"

        **Q5**. Déterminez le nombre de voitures que vous possédez. 

        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT COUNT(*) 
            FROM Vehicules
            ```       
        """
        )
        }}



        **Q6**. Déterminez l'âge minimum et maximum de vos véhicules.
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT MAX(age), MIN(age) 
            FROM Vehicules
            ```        
        """
        )
        }}



        **Q7**. Quels sont la marque et le modèle de votre dernière acquisition qui date de trois mois ?
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT nom 
            FROM Vehicules
            WHERE age = 3
            ```           
        """
        )
        }}


        **Q8**.  Quel est le kilométrage maximum des véhicules ?
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT MAX(kilometrage) 
            FROM Vehicules
            ```            
        """
        )
        }}


        **Q9**.  Quel est le kilométrage moyen des véhicules ?
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT AVG(kilometrage) 
            FROM Vehicules
            ```            
        """
        )
        }}



        **Q10**. Afficher toute la flotte de véhicules par ordre décroissant de kilométrage.

        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT * 
            FROM Vehicules
            ORDER BY kilometrage DESC
            ```   
        """
        )
        }}



    ??? note "Questions sur la relation ```Locations```"

        **Q11**. Visualisez toute la relation Locations. 
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT * 
            FROM Locations
            ```            
        """
        )
        }}



        **Q12**. Déterminez le nombre de locations effectuées avec changement d'agence
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT COUNT(*) 
            FROM Locations
            WHERE depart != retour
            ```            
        """
        )
        }}




        **Q13**. Déterminez le nombre total de kilomètres effectués durant les locations
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT SUM(kilometrage) 
            FROM Locations
            ```            
        """
        )
        }}



        **Q14**. Listez toutes les locations en y associant les caractéristiques du véhicule
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT * 
            FROM Locations
            JOIN Vehicules ON Locations.vehicule = Vehicules.immatriculation
            ```            
        """
        )
        }}



        **Q15**. Affichez le nom et l'immatriculation du véhicule ainsi que la date de la location et le kilométrage réalisé pour chacune des locations
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT Vehicules.nom, Vehicules.immatriculation, Locations.date, Locations.kilometrage 
            FROM Locations
            JOIN Vehicules ON Locations.vehicule = Vehicules.immatriculation
            ```            
        """
        )
        }}



        **Q16**. Affichez une seule fois le nom et l'immatriculation des véhicules ayant déjà été loués.
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT DISTINCT nom, immatriculation 
            FROM Locations
            JOIN Vehicules ON Locations.vehicule = Vehicules.immatriculation
            ```            
        """
        )
        }}
 


        **Q17**. Affichez les locations du véhicule immatriculé AB-224-BA en précisant le nom de l'agence de départ ainsi que la ville de départ dans l'ordre chronologique des locations.
        {{
        correction(True,
        """
        ??? success \"Correction\" 
            ```sql
            SELECT Agences.nom, Agences.ville, Locations.* 
            FROM Locations
            JOIN Agences ON Locations.depart = Agences.id
            WHERE vehicule = 'AB-224-BA'
            ORDER BY Locations.date
            ```            
        """
        )
        }}




!!! abstract "{{ exercice() }}"
    Championnat de France de Football 2015-2016

    *D'après le travail de J. Le Coupanec (Académie de Rennes)*
   
    La base de données [soccer.db](data/soccer.db) contient les tables ```Team```,```Match```, ```Event```, ```Player```.  

    ![](data/soccer_diag2.png)

    {!{ sqlide titre="**Requête :**"  base="T4_Bases_de_donnees/4.2_Langage_SQL/data/soccer.db" }!}

    **Q1**. Combien d'équipes ont participé à ce championnat ?

    {{
    correction(True,
    """
    ??? success \"Correction\" 
        ```sql
        SELECT COUNT(*) 
        FROM Team
        ```    
        ou mieux
        ```sql
        SELECT  COUNT( DISTINCT team) from EVENT;
        ```


        
    """
    )
    }}


    **Q2**. Listez les noms des clubs ainsi que leur date de création dans l'ordre chronologique de leur création.

    {{
    correction(True,
    """
    ??? success \"Correction\" 
        ```sql
        SELECT name, birthday 
        FROM Team
        ORDER BY birthday;
        ```           
    """
    )
    }}


    **Q3**. Combien de pénaltys ont été marqués ?


    {{
    correction(True,
    """
    ??? success \"Correction\" 
        ```sql
        SELECT COUNT(*) 
        FROM Event
        WHERE type='penalty';
        ```            
    """
    )
    }}



    **Q4**. Combien de pénaltys ont été sifflés ?


    {{
    correction(True,
    """
    ??? success \"Correction\" 
        ```sql
        SELECT COUNT(*) 
        FROM Event
        WHERE type IN ('penalty','miss')
        ```            
    """
    )
    }}


    **Q5**. Combien de cartons ont été distribués ? 

    {{
    correction(True,
    """
    ??? success \"Correction\" 
        ```sql
        SELECT COUNT(*) 
        FROM Event
        WHERE type IN ('red','yellow2','yellow')
        ```       
    """
    )
    }}



    **Q6**. Combien de buts ont été marqués ?
    {{
    correction(True,
    """
    ??? success \"Correction\" 
        ```sql
        SELECT COUNT(*) 
        FROM Event
        WHERE type IN ('goal','own','penalty')
        ```        
    """
    )
    }}



    **Q7**. Affichez tous les renseignements sur les 10 cartons rouges obtenus le plus rapidement pendant un match.

    {{
    correction(True,
    """
    ??? success \"Correction\" 
        ```sql
        SELECT * FROM Event
        WHERE type = 'red'
        ORDER BY time
        LIMIT 10
        ```           
    """
    )
    }}


    **Q8**.  Donnez le nom du joueur qui a obtenu le carton rouge le plus rapidement.
    {{
    correction(True,
    """
    ??? success \"Correction\" 
        ```sql
        SELECT name  FROM event 
        JOIN player ON player.id=event.player
        WHERE type='red' ORDER BY time LIMIT 1;
        ```            
    """
    )
    }}



!!! abstract "{{ exercice() }}"
    === "Énoncé"
        Cet exercice en ligne est proposé le Knight Lab de l'université américaine Northwerstern University.
    
        ![](data/murdermystery.png){: .center width=50%}
    
        **Le point de départ de l'histoire** : un meurtre a été commis **dans la ville de SQL City le 15 janvier 2018.**
    
        À partir de ce point de départ et d'une base de données dont le diagramme est donné ci-dessous, il s'agit de trouver le meurtrier.
    
        ![](data/schemaMM.png){: .center width=100%}

    === "Zone d'enquête"
        ???+ note "Zone d'enquête :octicons-search-16: (à coups de requêtes)"
            Il est conseillé de travailler avec un Bloc-Notes ouvert à côté afin d'y coller les renseignements obtenus.
    
            {!{ sqlide titre="Tapez votre requête ci-dessous"  base="T4_Bases_de_donnees/4.2_Langage_SQL/data/sql-murder-mystery.db" }!}
    
        ??? question "Vous pensez avoir trouvé le meurtrier ?"
            Copiez la requête 
            ```sql
            INSERT INTO solution VALUES (1, 'nom du meurtrier');
            SELECT value FROM solution;
            ```
            
    
            {!{ sqlide titre="dans le champ ci-dessous :"  base="T4_Bases_de_donnees/4.2_Langage_SQL/data/sql-murder-mystery.db" }!}
    
    
        Sur [la page officielle](https://mystery.knightlab.com/walkthrough.html){:target="_blank"}, vous pouvez être guidés étape par étape jusqu'à la recherche du meurtrier (qui n'est pas la fin de l'énigme !)
    
        - Vous pouvez si vous le souhaitez télécharger la base [sql-murder-mystery.db](data/sql-murder-mystery.db). 
    
    === "Correction"
    {#
        ```sql
        -- Requette:
        SELECT * FROM crime_scene_report 
        
        Résultat:
        -- Affichage de la table complète 
        -- On voit qu'il y a une description qu'il devrait être intéressant de consulter. 
        ___________________________________________________________________________________________
        -- Requette:
        SELECT description FROM crime_scene_report
        WHERE date = 20180115
        AND type = 'murder'
        AND city = 'SQL City';
        
        Résultat:
        -- Security footage shows that there were 2 witnesses. 
        -- The first witness lives at the last house on "Northwestern Dr". 
        -- The  witness, named Annabel, lives somewhere on "Franklin Ave".
        
        Commentaire: 
        -- Le rapport est de toute évidence incomplet.
        -- Mais comme deux localisations sont données, on va tenter de les exploiter.
        ___________________________________________________________________________________________
        -- Requette pour « The first witness lives at the last house on "Northwestern Dr". » :
        SELECT * FROM person
        WHERE address_street_name = 'Northwestern Dr'
        ORDER BY address_number DESC
        LIMIT 1;
        
        Résultat:
        |-------+----------------+------------+----------------+---------------------+-----------|
        |    id | name           | license_id | address_number | address_street_name |       ssn |
        |-------+----------------+------------+----------------+---------------------+-----------|
        | 14887 | Morty Schapiro |     118009 |           4919 | Northwestern Dr     | 111564949 |
        ___________________________________________________________________________________________
        -- Requette pour « The second witness, named Annabel, lives somewhere on "Franklin Ave". »:
        SELECT * FROM person
        WHERE name LIKE '%Annabel%' and address_street_name = 'Franklin Ave';
        
        Résultat:
        |-------+----------------+------------+----------------+---------------------+-----------|
        |    id | name           | license_id | address_number | address_street_name |       ssn |
        |-------+----------------+------------+----------------+---------------------+-----------|
        | 16371 | Annabel Miller |     490173 |            103 | Franklin Ave        | 318771143 |
        |-------+----------------+------------+----------------+---------------------+-----------|
        
        Commentaire: 
        -- On a identifié les deux témoins: Morty Schapiro et Annabel Miller
        -- id de la_table person est une clée primaire liée à la clé étrangère person_id 
        -- de la_table interview  
        ___________________________________________________________________________________________
        -- Requette donnant l'interview d'Annabel Miller : 
        SELECT transcript FROM interview 
        JOIN person ON person.id = interview.person_id
        WHERE person.name = 'Annabel Miller';
        
        Résultat:
        -- I saw the murder happen, and I recognized the killer from my gym when
        -- I was working out last week on January the 9th.
        ___________________________________________________________________________________________
        -- Requette donnant l'interview de Morty Schapiro : 
        SELECT transcript FROM interview 
        JOIN person ON person.id = interview.person_id
        WHERE person.name = 'Morty Schapiro';
        
        Résultat:
        -- I heard a gunshot and then saw a man run out. He had a "Get Fit Now Gym" bag.
        -- The membership number on the bag started with "48Z".
        -- Only gold members have those bags. The man got into a car with a plate that included "H42W".
        
        Commentaire: 
        -- On aurait pu faire la requette suivante pour avoir toutes ces informations en une fois.
        SELECT transcript FROM interview 
        JOIN person ON person.id = interview.person_id
        WHERE person.name in ('Annabel Miller', 'Morty Schapiro');
        
        ___________________________________________________________________________________________
        -- Requette exploitant ces deux interviews:
        SELECT person.name FROM person
        JOIN get_fit_now_member AS member ON person.id = member.person_id
        JOIN drivers_license AS dl ON person.license_id = dl.id
        JOIN get_fit_now_check_in AS ci ON ci.membership_id=member.id
        WHERE member.id LIKE '48Z%' 
        AND member.membership_status = 'gold'
        AND dl.plate_number like '%H42W%'
        AND ci.check_in_date = '20180109';
        
        Résultat:
        /*
        +---------------+
        | name          |
        +---------------+
        | Jeremy Bowers |
        +---------------+
        */
        -- Commentaire: 
        -- Ne pas utiliser la date conduit à la même réponse. 
        -- Mais, il est faux de ne pas vérifier que la date correspond. 
        -- La personne qui a pris la fuite a été trouvée, voyons sa déposition.
        ___________________________________________________________________________________________
        - Requette:
        SELECT transcript FROM interview
        JOIN person ON person.id = interview.person_id
        WHERE person.name = 'Jeremy Bowers';
        
        Résultat:
        -- I was hired by a woman with a lot of money.
        -- I don't know her name but I know she's around 5'5" (65") or 5'7" (67").
        -- She has red hair and she drives a Tesla Model S. 
        -- I know that she attended the SQL Symphony Concert 3 times in December 2017. 
        
        Commentaire :
        -- On a trouvé le meurtrier 
        -- Mais il faut maintenant chercher la femme qui a commandité le crime.
        ___________________________________________________________________________________________
        Requette:
        SELECT name as nom, fb.date as 'date du concert SQL' FROM person
        JOIN drivers_license AS dl ON dl.id = person.license_id
        JOIN facebook_event_checkin AS fb ON fb.person_id = person.id 
        WHERE fb.event_name LIKE "%SQL%"
        AND dl.car_make = 'Tesla' 
        AND dl.car_model = 'Model S'
        AND dl.hair_color = 'red'
        AND (65 <= dl.height <= 67);
        
        Résultat:
        /*
        |-------------------+---------------------|
        | nom               | date du concert SQL |
        |-------------------+---------------------|
        | Miranda  Priestly |            20171206 |
        |-------------------+---------------------|
        | Miranda  Priestly |            20171212 |
        |-------------------+---------------------|
        | Miranda  Priestly |            20171229 |
        |-------------------+---------------------|
        */
        Commentaire:
        -- Même si l'on enlève la couleur des cheveux, il n'y a pas plus de résultats.
        -- La personne qui a commandité le meurtre est donc Miranda Priestly        
        ```
   #} 
