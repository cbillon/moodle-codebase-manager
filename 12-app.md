
Le “12 Factor app” est un manifeste proposant 12 bonnes pratiques concernant le développement d’applications Cloud. Il a été écrit en 2012, par Adam Wiggins, co-fondateur d’Heroku, un éditeur d’outils permettant le déploiement applicatif web en mode PaaS.

Ces directives sont importantes et pertinentes pour concevoir une architecture d’application évolutive pouvant être publiée de manière fiable, mise à l’échelle rapidement et maintenue de manière cohérente et prévisible. Le « 12 factor app » identifie les erreurs courantes et les points de vigilance concernant l’architecture, le déploiement et l’exploitation d’une application

le document de référence [ici](https://12factor.net/fr/)

## 1. 12-Factor app : Base de code (Codebase)

Une “application” = une seule base de code

Cette base de code peut être déployée à plusieurs endroits, qu’on appelle “environnements” de développements, de tests,  de production, 
avec un système de contrôle de versions tel que Git et possibilité d’effectuer un rollback du code vers une version précédente à tout moment. 

Le principe d’une base de code définit qu’une application ne peut être archivée et versionnée dans plusieurs dépôts de code source et inversement.

Ainsi, un dépôt de code source ne peut contenir qu’une seule application à la fois. Chaque commit vers ce dépôt unique pourra faire l’objet d’une génération d’artefacts qui seront déployés vers un ou plusieurs environnements d’exécution de l’application (test, recette ou production)

Si plusieurs applications partagent la même base de code, il sera préférable de factoriser la partie de code en question qui sera publiée depuis un autre dépôt comme une dépendance externe.

## 2. 12-Factor App : Dépendances (Dependencies)

Les dépendances (plugins ,librairies, outils, …) doivent être décrites explicitement, de manière exhaustive, et doivent être installées lors de l’étape de “build” de l’application. Les plugins peuvent être mis à jour, étendus et déployés plus rapidement, indépendamment les uns des autres et en limitant le risque d’une mise en péril de l’ensemble de l’applicatif.

## 3. 12-Factor App : Configuration (Config)


La configuration ne doit pas faire partie du code mais doit être injectée . 
Pour Moodle cela concerne le fichier config.php


Aujourd’hui, la pratique la plus courante consiste à utiliser des variables d’environnement pour définir le contexte d’exécution d’une application. Ainsi la configuration (connexion à la base de données, identifiants, paramètres spécifiques…) est injectée dans les applications en fonctions du contexte. Le but est de ne packager l’application qu’une seule fois et de la déployer de multiple fois
   


## 4. 12-Factor App : Services de stockage externes (Backing Services)

Une application web utilise très souvent des services externes : serveur web (apache; nginx),base de données (mysql, postgres,...), service de cache (redis), stockage de fichier, envoi d’emails/sms, …Ces services doivent être traités comme externes, découplés de l’application, et utilisés indépendamment de leur méthode de déploiement (service managé par un fournisseur cloud, hébergé par un tiers, installé en local sur la machine). Les ressources auxiliaires (magasins de données, caches, courtiers de messages) doivent être exposées via une URL adressable. La ressource étant ainsi découplée de l’application, elle est interchangeable. On peut ainsi mettre à jour ou modifier ces services à tout moment, sans perturber le fonctionnement de l’application grâce à un détachement/attachement dynamique.

## 5. 12-Factor app : Build, release, run (CI/CD)

Il est recommandé de séparer le déploiement d’une application sur un nouvel environnement en trois phases :

    - L’étape « build » utilise le code et ses dépendances pour produire un artefact
    - L’étape « release » met cet artefact et la configuration associée à disposition sur l’environnement cible
    - L’étape « run » exécute une ou plusieurs instances de la version

Ce découpage en 3 phases réduit le temps d’indisponibilité de l’applicatif car la phase de build peut se faire en parallèle de l’exécution de l’ancienne application sur l’environnement cible. Chaque version doit appliquer une séparation stricte entre les étapes de génération, de mise en œuvre et d’exécution et doit être marquée d’un ID unique avec la possibilité d’effectuer une restauration à tout moment.

Une base de code est transformée en un déploiement (non-développement) à travers les étapes suivantes :

    - L’étape d’assemblage (ou “build”) est une transformation qui convertit un dépôt de code en un paquet autonome exécutable appelé l’assemblage (ou “build”). En utilisant une version du code référencée par un commit spécifié lors du processus de déploiement, l’étape d’assemblage va chercher toutes les dépendances externes et compile les fichiers binaires et les ressources.
    - L’étape de publication (ou “release”) prend l’assemblage produit à l’étape précédente et le combine avec la configuration de déploiement courante. La release résultante contient à la fois l’assemblage et la configuration, et elle est prête pour une exécution immédiate dans l’environnement d’exécution.
    - L’étape d’exécution (ou “runtime”) fait fonctionner l’application dans l’environnement d’exécution, en lançant un ensemble de processus de l’application associée à la release considéré
La configuration ne doit pas faire partie du code mais doit être injectée. 
Pour Moodle cela concerne le fichier config.php
Par ce moyen, l’ensemble des acteurs et outils au sein de la chaine de production applicative peut cibler une configuration spécifique à un environnement en fonction de ses besoins.



    