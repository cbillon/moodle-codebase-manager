# Gitops

C’est une implémentation du déploiement automatisé d’application Cloud Native qui consiste à réaliser la construction de l'infrastructure en utilisant les mêmes outils utilisés lors du développement d’applications comme Git ou encore les outils de CI/CD.

Le concept est d’avoir dans un repository Git la description déclarative de l’infrastructure souhaitée en production et un processus automatisé, qui se charge d'appliquer l'état d’infrastructure défini dans le repo git sur vos environnements. Ainsi, pour déployer une nouvelle version d’application ou la mettre à jour, le repository Git doit être mis à jour et le processus automatisé se charge du reste, car c’est la source centrale de vérité pour toute l’infrastructure requise pour faire tourner les applications

Pour arriver à une implémentation complète du GitOps, il faut utiliser un pipeline CI/CD. Les changements d’infrastructures sur Git seront déployés automatiquement dans l'environnement souhaité après chaque commit.

## Pourquoi une organisation doit adopter les pratiques GitOps ?
D’un point de vue stratégique, il y a plusieurs raisons qui peuvent amener une organisation à adopter la pratique du GitOps.

### Déploiements Continus
Les déploiements automatisés impliquent forcément des déploiements plus fréquents et plus rapides. GitOps facilite le processus de déploiement d’infrastructure, car tous les changements se passent sur Git et il n’y a plus besoin de gérer des outils en plus pour mettre à jour votre infrastructure.

### Rollback
Toutes les opérations sont tracées et historisées sur Git. Il est toujours possible de retrouver à partir de quel déploiement (ou commit) un dysfonctionnement est apparu et de retirer la modification correspondante. Ceci réduit énormément le MTTR (Mean-time-to-repair), en particulier sur des architectures microservices.

### Sécurité
GitOps repose sur la sécurisation du repository Git. Tandis que les équipes ont les droits d'écriture et passent par un processus de peer-review via des pull-requests, le processus chargé de déployer sur l’environnement cible nécessite seulement des droits de lecture (et en particulier pour des stratégies de Pull). Le fait d'utiliser des branches bien protégées pour des environnements de production ( accessibles en écriture à des profils restreints) et d’avoir une stratégie de gestion de secrets augmentent le niveau de sécurité des déploiements.  Ceci permettra de ne pas exposer les secrets via la CI/CD (facile  à garantir en mode PULL) et de faciliter les audits du code Git car c’est la seule source de vérité.

### Auto-documentation
Étant donné que l'état d’infrastructure est documenté sur Git, tous les membres de l'équipe peuvent suivre et comprendre l'évolution de l’infrastructure. Ce repository Git représente en lui-même une documentation maintenue enrichie avec les messages des commits.