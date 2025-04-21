## Le fichier de configuration 

```
  moodle:
    version: 4.5+
  plugins:
    moodle-tool_redis:
      name: Redis management
      source: https://github.com/moodle-an-hochschulen/moodle-tool_redis
      branch: MOODLE_405_STABLE
    moodle-tool_opcache:
      name: Opcache management
      source: https://github.com/moodle-an-hochschulen/moodle-tool_opcache
      branch: MOODLE_405_STABLE

```
A chaque projet est associée une base de code.
Le fichier de configuration défnit l'état demandé de la base de code .

Le fichier de configuration comporte 2 parties distinctes
- Moodle
- la liste des plugins à installer

Cela commence par définir la version de Moodle :
il est possible de préciser comme version source :

- la dernière version mineure disponible: 4.5 
- la dernière version mineure avec les dernières corrections  : 4.5+
- une version  spécifique : 4.5.1
- une version spécifique définie par un tag : <tag>
- une version spécifique définie par un commit : <commit>

### Liste des plugins à installer

Les commandes suivantes  sont utilisées :
- import d'un plugin
- ajout d'un plugin au projet
- edition du fichier de configuration

#### import d'un plugin
A partir du nom du plugin moodle-<type>_<component name> ou sous forme abéégée <type>_<compnent name>, le script recupere les informations dans le répertoire officiel des plugins maintenu par Moodle pour cloner en local le dépot.

#### Ajout d'un plugin au projet
A partir de la liste des plugins en cache, sélection du plugin à installer
Le script recherche la version du plugin compatible avec la version Moodle du projet

### Edition du fichier de configuration
L'adminstateteur peut editer manuellement lr fichier de configuration
- ajout d'un plugin non officiel
- utilisation d'une version personnalidée d'un plugin








## Moodle

Chaque version de Moodle comporte 3 parties par exemple : 4.5.1 

Une version majeure est définie par les 2 premiers chiffres : 4.5

Le dernier chiffre indiquant les versions mineures.

Moodle suit les concepts [semantic versionnning](versionninnage_semantique.md)

Moodle HQ livre des mises à jour chaque semaine pour les versions mineures maintenues.
Tous les 2 mois, sortie d'une nouvelle version mineure après passage de tests approfondis
voir le détail [ici](https://moodledev.io/general/releases)

Dans le fichier de configuration 

la mise à niveau du dépôt local Moodle se fait en lançant l'option : Mise à jour du cache Moodle

## PLugins

Pour chaque plugins :
- name : description succincte (optionnel)
- source: url du dépôt git du plugin
- version : référence  à utiliser  (doit être compatible avec la version Moodle)

Ces informations sont renseignées automatiquement lors de l'utilisation de la commande **import d'un plugin**
Elles doivent être renseignées manuellement pour un plugin qui ne provient pas de la liste officielle.
