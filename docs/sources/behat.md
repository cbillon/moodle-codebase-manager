### Behat

Behat est un framework de développement piloté par le comportement (BDD) qui permet de spécifier les fonctionnalités de Moodle (ou features) sous forme d'une liste d'étapes lisibles par l'utilisateur. Il analyse ces étapes en actions exécutables pour simuler l'interaction utilisateur avec des navigateurs headless (sans prise en charge de JavaScript, uniquement des requêtes de type curl) ou des outils de simulation utilisateur comme Selenium, qui interagit avec les navigateurs et permet la simulation d'événements JavaScript.
#### Objectif
L'objectif de cette intégration est de permettre aux composants Moodle 
d'avoir leurs propres fonctionnalités et définitions d'étapes. Cela nous permet d'exécuter périodiquement des séries de tests pour détecter les régressions et les fonctionnalités de Moodle dans différents environnements (navigateurs, moteurs de bases de données, serveurs web...). Les tests d'assurance qualité de Moodle seront progressivement réécrits selon ce format pour s'exécuter automatiquement.
