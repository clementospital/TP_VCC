# TP1

## Étape 1

1. Une machine virtuelle est une une machine émulée par un logiciel. Elle dispose de son propre OS et de ses propres caractéristiques. Ces dernières sont prêtées par la machine physique en fonction des besoins de la VM. Elle fonctionne comme une machine physique.

2. Cela sert à mutualiser les ressources physiques mais aussi de disposer d'un environnement isolé du reste de la machine.

3. Aux niveaux des ressources, on est plus limité sur la VM car les ressources qu'elle utilise sont celles prêtées par la machine physique en fonction de son besoin. En revanche, sur une VM, on peut avoir un environnement de travail modulable, démultipliable (image).

## Étape 2 

1. Un conteneur Docker est un environnement minimaliste stable virtualisé pour faire tourner un service précis et ce, sur n'importe quel OS. Il embarque les dépendances et le runtime nécessaire pour faire tourner son service.

2. Une VM virtualise un OS tandis qu'un containeur partage l'OS hôte.

3. Car elles prennent peu de place et sont rapides à déployer et à multiplier (images) en cas de besoin de charge.

## Étape 3

1. Pour la stabilité et la portabilité du conteneur et de ses dépendances. Pour un projet, grâce à un Dockerfile commun tout le monde travaillera avec les mêmes dépendances et blibliothèques.

2. Un conteneur Docker est une instance d'une image Docker, une image peut donc avoir plusieurs conteneurs.

## Étape 4

1. Docker Compose est préférable car plus rapide dans un premier temps et surtout il va assurer à l'aide du docker-compose.yml que chaque micro-service expose les bons ports, ne partagent pas un même port. Il permet aussi de supprimer tous les containers de l'application distribuée en une seule commande (docker compose down).

2. Le docker-compose.yml indique les dépendances entre les containers et les services de l'application distribuée. Il indique ou se situe chaque micro-service. Il indique aussi les ports à exposer pour utiliser les micros-services individuels et/ou le service général (ici nous somme dans le cas d'un port unique pour un service de calculateur reposant sur des micros services composant un calculateur : addition, soustraction etc...).

3. Docker compose pourrait trouver ses limites sur une application distribuée en micros services que l'on voudrait hébergé sur différentes machines. Par ailleurs, si on veut utiliser un seul des micro service, on est obligé de construire l'image de tous les micros services de l'application. Par exemple ici, si je veux uniquement un service de soustraction, docker compose ne me le permet pas, il construira tous les autres micros service conformément au docker-compose.yml.


## Bonus

Afin de supprimer tous les containeurs indépendants (non gérés par un docker-compose.yml) voici une commande fonctionnelle : sudo docker rm -f $(sudo docker ps -aq). Le -f permet de forcer la suppression (si container actif il y a).
