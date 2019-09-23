# ROSSI Thomas TP3

# Exercice 1. Commandes de base

**1.Quels sont les 5 derniers paquets installés sur votre machine?**

```
thomas@ubuntu-server:~/script/TP3$ grep installed /var/log/dpkg.log | tail -5
2019-09-23 12:34:44 status installed sosreport:amd64 3.6-1ubuntu2.1
2019-09-23 12:34:44 status installed apt-utils:amd64 1.8.3
2019-09-23 12:34:44 status installed rsyslog:amd64 8.32.0-1ubuntu7
2019-09-23 12:34:46 status installed man-db:amd64 2.8.5-2
2019-09-23 12:34:46 status installed libc-bin:amd64 2.29-0ubuntu2
```

**2.Utiliser dpkg et apt pour compter le nombre de paquets installés (ne pas hésiter à consulter le manuel!).Comment explique-t-on la (petite) différence de comptage?**

```
thomas@ubuntu-server:~/script/TP3$ apt list --installed | wc -l

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

521
thomas@ubuntu-server:~/script/TP3$ dpkg -l | wc -l
525
```

Il y a une différence de 4 lignes car avec la commande car avec dpkg -l il y a 5 lignes en plus au dessus qui ne sont pas des packets et avec apt list il y a 1 ligne en plus qui ne correspond pas à un packet.

**3.Combien de paquets sont disponibles en téléchargement ?**

```apt list | wc -l```

**4.Créer un alias “maj” qui met à jour le système**

```alias maj='sudo apt-get update ; sudo apt-get upgrade'```

**5.A quoi sert le paquet fortunes? Installez-le.**

```sudo apt install fortune-mod```

Il permet d'afficher des petits messages, des citations, des proverbes, etc.. à la connexion de l'utilisateur.

**6.Quels paquets proposent de jouer au sudoku?**

```
thomas@ubuntu-server:/var/lib/apt/lists$ apt search sudoku
En train de trier... Fait
Recherche en texte intégral... Fait
fltk1.1-games/disco 1.1.10-26ubuntu1 amd64
  Boîte à outils Fast Light - exemples de jeux : jeux de dames, sudoku

fltk1.3-games/disco 1.3.4-9ubuntu1 amd64
  Boîte à outils Fast Light - exemples de jeux : jeux de dames, sudoku

gnome-sudoku/disco 1:3.32.0-1 amd64
  Casse-tête Sudoku pour GNOME

hitori/disco 3.31.0-1 amd64
  Jeu de puzzle logique similaire au sudoku

ksudoku/disco 4:18.12.3-0ubuntu1 amd64
  Jeu et Solveur de Sudoku

libqqwing-dev/disco 1.3.4-1.1 amd64
  outil pour générer et résoudre des casse-tête Sudoku (développement)

libqqwing2v5/disco 1.3.4-1.1 amd64
  outil pour générer et résoudre des casse-tête Sudoku (bibliothèque)

nudoku/disco 1.0.0-1 amd64
  ncurses based sudoku games

qqwing/disco 1.3.4-1.1 amd64
  tool for generating and solving Sudoku puzzles (application)

sudoku/disco,now 1.0.5-2build3 amd64  [installé]
  Sudoku en mode console

texlive-games/disco 2018.20190227-1 all
  TeX Live : Composition de jeux
  ```

Les packets gnome-sudoku, hitori, ksudoku, libqqwing-dev, libqqwing2v5, nudoku, qqwing, sudoku, texlive-games.

**7.Lister les derniers paquets installés explicitement avec la commande apt install**

```cat /var/log/apt/history.log```

# Exercice 2

**A partir de quel paquet est installée la commande ls? Comment obtenir cette information en une seule commande, pour n’importe quel programme (indice : la réponse est dans le poly de cours 2, dans la liste descommandes utiles)? Utilisez la réponse à pour écrire un script appelé origine-commande(sans l’extension.sh) prenant en argument le nom d’une commande, et indiquant quel paquet l’a installée.**

```
which -a $1 | xargs dpkg -S 2> /dev/null
```

# Exercice 3

**Ecrire une commande qui aﬀiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du packagespécifié dans cette commande.**

```
if [ $(apt list --installed 2>/dev/null | grep -c "$1") = "1" ]; then
        echo "Le packet $1 est installé"
else
        echo "Le packet $1 n'est pas installé"
fi
```

```
dpkg -l "nom_package" | grep "^ii") && echo "Installé" || echo "Non installé"
```

# Exercice 4

**Lister les programmes livrés avec coreutils. A quoi sert la commande ’[’ et comment aﬀicher ce qu’elle retourne ?**

```
apt show coreutils
```

D'après le manuel, [ est un test - check file types and compare values

```
thomas@ubuntu-server:~/script/TP3$ [
-bash: [: missing `]'
thomas@ubuntu-server:~/script/TP3$ echo $?
2
```

Elle retourne 2

# Exercice 5

**Installez le paquet emacs à l’aide de la version graphique d’aptitude**

```
aptitude
/emacs
/emacs
/emacs
Entrer
+
g
g
```

# Exercice 6. Installation d’un paquet par PPA

**2.Vérifiez qu’un nouveau fichier a été créé dans/etc/apt/sources.list.d. Que contient-il?**


# Exercice 7

