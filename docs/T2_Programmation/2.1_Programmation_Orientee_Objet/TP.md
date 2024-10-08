# TP : balles rebondissantes

![image](data/balles1.png){: .center witdh=40%}

## 1. Prise en main de Pygame

```python linenums='1'
import pygame, sys
import time
from pygame.locals import *

LARGEUR = 640
HAUTEUR = 480
RAYON = 20

pygame.display.init()
fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
fenetre.fill([0,0,0])

x = 300
y = 200
dx = 4
dy = -3
couleur = (45, 170, 250)

while True:
    fenetre.fill([0, 0, 0])
    pygame.draw.circle(fenetre, couleur, (x, y), RAYON)

    x += dx
    y += dy

    pygame.display.update()

    # routine pour pouvoir fermer «proprement» la fenêtre Pygame
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.display.quit()
            sys.exit()

    time.sleep(0.1)


```

### 1.1  Rajout d'un rebond sur les parois
Modifiez le code précédent afin que la balle rebondisse sur chaque paroi (il suffit de modifier intelligemment "les variables de vitesse" ```dx``` et ```dy```).

??? tip "Variables de vitesse"
    Il s'agit d'un abus de langage. En effet, la vitesse horizontale de la balle se note $v_x$ pas $dx$ mais $v_x$ est liée à la variation de position horizontale $dx$ par la formule $v_x=\frac{dx}{dt}$ où $dt$ est le temps entre deux rafraîchissement d'image que l'on indique dans `time.sleep(dt)`. Donc, à rafraîchissement d'image constant, c'est bien $dx$ qui permet de fixer la vitesse horizontale de la balle. Il en est de même pour la relation entre la vitesse verticale $v_y$ et `dy`. 


??? info "Correction"
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])

    x = 300
    y = 200
    dx = 4
    dy = -3
    couleur = (45, 170, 250)

    while True:
        fenetre.fill([0, 0, 0])
        pygame.draw.circle(fenetre, couleur, (x, y), RAYON)

        x += dx
        y += dy

        if (y <= RAYON) or (y >= HAUTEUR - RAYON):
            dy = -dy
        if (x <= RAYON) or (x >= LARGEUR - RAYON):
            dx = -dx

        pygame.display.update()

        # routine pour pouvoir fermer «proprement» la fenêtre Pygame
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.02)


    ```



### 1.2 Rajout d'une deuxième balle
Attention au nommage des variables...

??? info "À compléter"
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])

    dxA = 7
    dyA = 4
    dxB = -5
    dyB = 3


    xA = LARGEUR // 3
    yA = HAUTEUR // 2
    xB = LARGEUR // 2
    yB = HAUTEUR // 2


    couleurA = (45, 170, 250)
    couleurB = (155, 17, 250)

    while True:
        ######################
        #        À vous      #
        ######################        
        pygame.display.update()

        # routine pour pouvoir fermer «proprement» la fenêtre Pygame
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.03)
    ```






??? info "Correction"
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])


    dxA = 7
    dyA = 4
    dxB = -5
    dyB = 3


    xA = LARGEUR // 3
    yA = HAUTEUR // 2
    xB = LARGEUR // 2
    yB = HAUTEUR // 2


    couleurA = (45, 170, 250)
    couleurB = (155, 17, 250)

    while True:
        fenetre.fill([0, 0, 0])
        pygame.draw.circle(fenetre, couleurA, (xA, yA), RAYON)
        pygame.draw.circle(fenetre, couleurB, (xB, yB), RAYON)

        xA += dxA
        yA += dyA

        xB += dxB
        yB += dyB

        # rebond en haut ou en bas
        if (yA < RAYON) or (yA > HAUTEUR - RAYON):
            dyA = -dyA

        # rebond à gauche ou à droite
        if (xA < RAYON) or (xA > LARGEUR - RAYON):
            dxA = -dxA

        # rebond en haut ou en bas
        if (yB < RAYON) or (yB > HAUTEUR - RAYON):
            dyB = -dyB

        # rebond à gauche ou à droite
        if (xB < RAYON) or (xB > LARGEUR - RAYON):
            dxB = -dxB

        pygame.display.update()

        # routine pour pouvoir fermer «proprement» la fenêtre Pygame
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.03)


    ```

### 1.3 Gestion de la collision entre les deux balles
**Q1.** À l'aide d'un schéma (papier-crayon !), mettez en évidence le test devant être réalisé pour détecter une collision.

??? tip "indice"
    ![image](data/TP_dist.png){: .center}
    

**Q2.** Implémentez ce test (en créant pour cela une fonction ```distance``` )  et affichez "collision" en console lorsque les deux balles se touchent.

??? info "Correction"
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])


    dxA = 7
    dyA = 4
    dxB = -5
    dyB = 3


    xA = LARGEUR // 3
    yA = HAUTEUR // 2
    xB = LARGEUR // 2
    yB = HAUTEUR // 2


    couleurA = (45, 170, 250)
    couleurB = (155, 17, 250)


    def distanceAB(xA, yA, xB, yB):
        return ((xA-xB)**2 + (yA-yB)**2)**0.5


    while True:
        fenetre.fill([0, 0, 0])
        pygame.draw.circle(fenetre, couleurA, (xA, yA), RAYON)
        pygame.draw.circle(fenetre, couleurB, (xB, yB), RAYON)

        xA += dxA
        yA += dyA

        xB += dxB
        yB += dyB

        # rebond en haut ou en bas
        if (yA < RAYON) or (yA > HAUTEUR - RAYON):
            dyA = -dyA

        # rebond à gauche ou à droite
        if (xA < RAYON) or (xA > LARGEUR - RAYON):
            dxA = -dxA

        # rebond en haut ou en bas
        if (yB < RAYON) or (yB > HAUTEUR - RAYON):
            dyB = -dyB

        # rebond à gauche ou à droite
        if (xB < RAYON) or (xB > LARGEUR - RAYON):
            dxB = -dxB

        if distanceAB(xA, yA, xB, yB) < 2 * RAYON:
            print("collision")

        pygame.display.update()

        # routine pour pouvoir fermer «proprement» la fenêtre Pygame
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.03)



    ```


**Q3.** Pour donner l'illusion physique du rebond, échangez les valeurs respectives de ```dx``` et ```dy``` pour les deux balles.

??? info "Correction"
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])


    dxA = 7
    dyA = 4
    dxB = -5
    dyB = 3


    xA = LARGEUR // 3
    yA = HAUTEUR // 2
    xB = LARGEUR // 2
    yB = HAUTEUR // 2


    couleurA = (45, 170, 250)
    couleurB = (155, 17, 250)


    def distanceAB(xA, yA, xB, yB):
        return ((xA-xB)**2 + (yA-yB)**2)**0.5


    while True:
        fenetre.fill([0, 0, 0])
        pygame.draw.circle(fenetre, couleurA, (xA, yA), RAYON)
        pygame.draw.circle(fenetre, couleurB, (xB, yB), RAYON)

        xA += dxA
        yA += dyA

        xB += dxB
        yB += dyB

        # rebond en haut ou en bas
        if (yA < RAYON) or (yA > HAUTEUR - RAYON):
            dyA = -dyA

        # rebond à gauche ou à droite
        if (xA < RAYON) or (xA > LARGEUR - RAYON):
            dxA = -dxA

        # rebond en haut ou en bas
        if (yB < RAYON) or (yB > HAUTEUR - RAYON):
            dyB = -dyB

        # rebond à gauche ou à droite
        if (xB < RAYON) or (xB > LARGEUR - RAYON):
            dxB = -dxB

        if distanceAB(xA, yA, xB, yB) < 2 * RAYON:
            dxA, dxB = dxB, dxA
            dyA, dyB = dyB, dyA

        pygame.display.update()

        # routine pour pouvoir fermer «proprement» la fenêtre Pygame
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.03)



    ```






### 1.4 Rajout d'une troisième balle et gestion du rebond avec les deux autres.
... vraiment ? Peut-on continuer comme précédemment ?

![image](data/meme_doubt.png){: .center width=30%}


## 2. La POO à la rescousse : création d'une classe Balle

### 2.1 la classe Balle
L'objectif est que la méthode constructeur dote chaque nouvelle balle de valeurs aléatoires : abscisse, ordonnée, vitesse, couleur...  

- Pour l'aléatoire, on pourra utiliser ```randint(a, b)``` qui renvoie un nombre pseudo-aléatoire entre ```a``` et ```b```.
Il faut pour cela importer la fonction, par ```from random import randint``` 

- Vous pouvez aussi doter votre classe ```Balle``` d'une méthode ```dessine``` (qui affiche la balle), ainsi qu'une méthode ```bouge``` qui la fait bouger. 

Créez cette classe et instanciez une balle.

??? info "À compléter"
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *
    from random import randint

    # randint(0,10) -> nb aléatoire entre 0 et 10

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])


    class Balle:
        def __init__(self):
            # à vous

        def dessine(self):
            # à vous

        def bouge(self):
            # à vous


    ma_balle = Balle()

    while True:
        fenetre.fill([0, 0, 0])

        ma_balle.dessine()
        ma_balle.bouge()

        pygame.display.update()
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.05)


    ```

??? info "Correction"
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *
    from random import randint

    # randint(0,10) -> nb aléatoire entre 0 et 10

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])


    class Balle:
        def __init__(self):
            self.x = randint(0, LARGEUR)
            self.y = randint(0, HAUTEUR)
            self.dx = randint(2, 5)
            self.dy = randint(2, 5)
            self.couleur = (randint(0, 255), randint(0, 255), randint(0, 255))
            self.taille = RAYON

        def dessine(self):
            pygame.draw.circle(fenetre, self.couleur, (self.x, self.y), self.taille)

        def bouge(self):
            self.x += self.dx
            self.y += self.dy

            if self.y < self.taille or self.y > HAUTEUR - self.taille:
                self.dy = -self.dy
            if self.x < self.taille or self.x > LARGEUR - self.taille:
                self.dx = -self.dx


    ma_balle = Balle()

    while True:
        fenetre.fill([0, 0, 0])

        ma_balle.dessine()
        ma_balle.bouge()

        pygame.display.update()
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.05)


    ```
    


### 2.2 Plusieurs balles

L'idée est de stocker dans une liste ```sac_a_balles``` un nombre déterminé de balles... 

??? info "À compléter"
    
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *
    from random import randint

    # randint(0,10) -> nb aléatoire entre 0 et 10

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20
    NB_BALLES = 10

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])


    class Balle:
        def __init__(self):
            self.x = randint(0, LARGEUR)
            self.y = randint(0, HAUTEUR)
            self.dx = randint(2, 5)
            self.dy = randint(2, 5)
            self.couleur = (randint(0, 255), randint(0, 255), randint(0, 255))
            self.taille = RAYON

        def dessine(self):
            pygame.draw.circle(fenetre, self.couleur, (self.x, self.y), self.taille)

        def bouge(self):
            self.x += self.dx
            self.y += self.dy

            if self.y < self.taille or self.y > HAUTEUR - self.taille:
                self.dy = -self.dy
            if self.x < self.taille or self.x > LARGEUR - self.taille:
                self.dx = -self.dx


    mon_sac_a_balles = # à vous 

    while True:
        fenetre.fill([0, 0, 0])

        for balle in mon_sac_a_balles:
            balle.dessine()
            balle.bouge()

        pygame.display.update()
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.05)


    ```


??? info "Correction"
    
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *
    from random import randint

    # randint(0,10) -> nb aléatoire entre 0 et 10

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20
    NB_BALLES = 10

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])


    class Balle:
        def __init__(self):
            self.x = randint(0, LARGEUR)
            self.y = randint(0, HAUTEUR)
            self.dx = randint(2, 5)
            self.dy = randint(2, 5)
            self.couleur = (randint(0, 255), randint(0, 255), randint(0, 255))
            self.taille = RAYON

        def dessine(self):
            pygame.draw.circle(fenetre, self.couleur, (self.x, self.y), self.taille)

        def bouge(self):
            self.x += self.dx
            self.y += self.dy

            if self.y < self.taille or self.y > HAUTEUR - self.taille:
                self.dy = -self.dy
            if self.x < self.taille or self.x > LARGEUR - self.taille:
                self.dx = -self.dx


    mon_sac_a_balles = [Balle() for _ in range(NB_BALLES)]

    while True:
        fenetre.fill([0, 0, 0])

        for balle in mon_sac_a_balles:
            balle.dessine()
            balle.bouge()

        pygame.display.update()
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.05)


    ```
    

### 2.3 Collision de toutes les balles

Il «suffit» , dans la méthode constructeur, de tester la collision de la balle ```self``` avec chacune des balles de notre ```sac_a_balles```. 

??? info "Correction"
    
    ```python linenums='1'
    import pygame, sys
    import time
    from pygame.locals import *
    from random import randint

    # randint(0,10) -> nb aléatoire entre 0 et 10

    LARGEUR = 640
    HAUTEUR = 480
    RAYON = 20
    NB_BALLES = 10

    pygame.display.init()
    fenetre = pygame.display.set_mode((LARGEUR, HAUTEUR))
    fenetre.fill([0, 0, 0])


    class Balle:
        def __init__(self):
            self.x = randint(0, LARGEUR)
            self.y = randint(0, HAUTEUR)
            self.dx = randint(2, 5)
            self.dy = randint(2, 5)
            self.couleur = (randint(0, 255), randint(0, 255), randint(0, 255))
            self.taille = RAYON

        def dessine(self):
            pygame.draw.circle(fenetre, self.couleur, (self.x, self.y), self.taille)

        def bouge(self):
            self.x += self.dx
            self.y += self.dy

            if self.y < self.taille or self.y > HAUTEUR - self.taille:
                self.dy = -self.dy
            if self.x < self.taille or self.x > LARGEUR - self.taille:
                self.dx = -self.dx

            for balle in mon_sac_a_balles:
                if (
                    (self.x - balle.x) ** 2 + (self.y - balle.y) ** 2
                ) ** 0.5 < self.taille + balle.taille:
                    self.dx, balle.dx = balle.dx, self.dx
                    self.dy, balle.dy = balle.dy, self.dy


    mon_sac_a_balles = []
    for _ in range(NB_BALLES):
        new_ball = Balle()
        mon_sac_a_balles.append(new_ball)

    # ces 4 dernière lignes peuvent s'écrire par une seule liste en compréhension :
    # mon_sac_a_balles = [Balle() for _ in range(NB_BALLES)]

    while True:
        fenetre.fill([0, 0, 0])

        for balle in mon_sac_a_balles:
            balle.dessine()
            balle.bouge()

        pygame.display.update()
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.display.quit()
                sys.exit()

        time.sleep(0.05)


    ```
    

{#
!!! capytale "Dépôt de projet sur Capytale : [fd7c-59906](https://capytale2.ac-paris.fr/web/c-auth/list?returnto=/web/code/fd7c-59906)"
    Servez-vous de cette feuille de projet pour y déposer les différentes versions de votre travail.
    Je pourrai ainsi le consulter au fur et à mesure de votre progression.

    Ce que je ne veux pas voir :
    ![](data/paste.jpg){: .center width=40%} 

#}
