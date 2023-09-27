
<!-- ![](data/pile_exec.webp){: .center width=30%} -->

### 3.2 Limitation de la taille de la pile
Nous venons de voir que notre appel à ```mystere(5)``` générait une pile de hauteur 6 (on parlera plutôt de *profondeur* 6). Cette profondeur est-elle limitée ?


```python
mystere(2962)
```


    ---------------------------------------------------------------------------

    RecursionError                            Traceback (most recent call last)

    <ipython-input-32-a97c4dde4ef8> in <module>
    ----> 1 mystere(2962)
    

    <ipython-input-1-386660a434f2> in mystere(n)
          3         return 0
          4     else :
    ----> 5         return n + mystere(n-1)
    

    ... last 1 frames repeated, from the frame below ...


    <ipython-input-1-386660a434f2> in mystere(n)
          3         return 0
          4     else :
    ----> 5         return n + mystere(n-1)
    

    RecursionError: maximum recursion depth exceeded in comparison


Vous venons de provoquer un «débordement de pile», le célèbre **stack overflow**. 

De manière générale, les programmes récursifs sont souvent susceptibles de générer un trop grand nombre d'appels à eux-mêmes. Il est parfois possible de les optimiser, comme nous le verrons dans le cours concernant la **programmation dynamique**.  

Nous reparlerons aussi de récursivité lorsque nous l'inscrirons dans un paradigme plus global de programmation, qui est **« diviser pour régner »** (en anglais *divide and conquer*).

## 4. Exemples de récursivité double

### 4.1 La suite de Fibonacci
Considérons la suite numérique ainsi définie :

- $F_0 = 0$
- $F_1 = 1$
- $\forall n \in \mathbb{N}, F_{n+2} = F_{n+1}+F_n$

On a donc $F_2=0+1=1, F_3=F_2+F_1=1+1=2, F_4=F_3+F_2=2+1=3, F_5=F_4+F_3=3+2=5$ ...


!!! example "{{ exercice() }}"
    === "Énoncé"
        Implémenter de façon récursive la suite de Fibonacci.
    === "Correction"
        {#
        ```python linenums='1'
        def fibo(n):
            if n == 0 :
                return 0   
            elif n == 1 :
                return 1
            else :
                return fibo(n-1) + fibo(n-2)
        ```
        #}



**Observation de la pile d'exécution**

Appelons ```F(n)``` la fonction calculant de manière récursive le n-ième terme de la suite. Observons en détail la pile d'exécution lors du calcul de ```F(4)```.


<center>
![](data/pile_fibo.gif)
</center>


!!! aide "Analyse grâce à PythonTutor"
    <iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20fibo%28n%29%3A%0A%20%20%20%20%0A%20%20%20%20if%20n%20%3D%3D%200%20or%20n%20%3D%3D%201%20%3A%0A%20%20%20%20%20%20%20%20return%20n%0A%20%20%20%20else%20%3A%0A%20%20%20%20%20%20%20%20return%20fibo%28n-1%29%20%2B%20fibo%28n-2%29%0A%0Aprint%28fibo%284%29%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

On s'aperçoit notamment que :

- les appels récursifs ne sont PAS simultanés (rappelons que la simultanéité n'existe théoriquement pas en informatique). On pourrait s'imaginer que la relation $F_4=F_3+F_2$ allait déclencher deux «fils» récursifs calculant respectivement $F_3$ et $F_2$. Il n'en est rien, on va jusqu'au bout du calcul de $F_3$ avant de s'intéresser à $F_2$.
- conséquence de la remarque précédente : le calcul de $F_2$ s'effectue 2 fois. Une amélioration future (appelée **mémoïsation**, voir le cours de programmation dynamique) sera de conserver cette valeur de $F_2$ afin d'améliorer les calculs.


Observation sur Capytale (code cca1-1932300) avec ```rcviz``` (Module Python pour visualiser une récursion sous forme d'arbre avec des arguments et des valeurs de retour à chaque nœud.)  

On peut y construire par exemple l'arbre d'appel de ```fibo(6)``` :

![image](data/arbre.png){: .center width=100%}

On y remarque (par exemple) que ```fibo(2)``` est calculé 5 fois... 

### 4.2 Comparaison des performances

!!! example "{{ exercice() }}"
    === "Énoncé"
        Écrire une fonction ```fibo_imperatif(n)``` qui calcule de façon directe (*impérative*) le n-ième terme de la suite de Fibonacci.
    === "Correction"
        {#
        ```python linenums='1'
        def fibo_imperatif(n):
            a = 0
            b = 1
            for k in range(n-1):
                t = b
                b = a + b
                a = t
            return b
        ```
        #}



Observons grâce au module ```timeit``` le temps moyen pris pour calculer $F(20)$ avec les deux fonctions ```fibo_imperatif()``` et ```fibo_recursif()```.


```python
%timeit fibo_imperatif(20)
```

    1.02 µs ± 14 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)



```python
%timeit fibo_recursif(20)
```

    2.35 ms ± 10.8 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)


La programmation récursive apparait donc comme quasiment 1000 fois plus lente que l'impérative.

:warning: **Attention :** cette comparaison des vitesses d'éxécution peut être critiquée car les deux programmes n'ont pas la même _complexité_. Nous étudierons la complexité au moment des algorithmes de tri. 



![image](data/prod.jpg){: .center width=40%}

Peut-on résumer la récursivité à une méthode élégante mais inefficace ? Ce serait réducteur : l'efficacité c'est _aussi_ avoir un code lisible et intuitif. Nous en reparlerons lors du parcours des arbres et des graphes. (cf aussi l'exercice sur les Tours de Hanoï)
## 5. Annexe : dessins récursifs grâce au module ```turtle``` 
Le module ```turtle``` permet de faire des tracés basiques. Mais dès l'instant où on met de la récursivité dans le code, les résultats peuvent devenir très surprenants, et aboutir à des structures [fractales](https://fr.wikipedia.org/wiki/Fractale).

```python linenums='1'
from turtle import *

ang = 40

def trace(n,l):
    
    if n == 0 :
        return None
    else :
        forward(l)
        left(ang)
        trace(n-1,0.7*l)
        right(2*ang)
        trace(n-1,0.7*l)
        left(ang)
        forward(-l)

        
penup()        
goto(0,-80)
pendown()
left(90)
speed(0)

trace(5,100)
```

<center>
![](Https://raoulhatterer.github.io/tnsi/T2_Programmation/2.2_Recursivite/data/arbre.gif)
</center>
