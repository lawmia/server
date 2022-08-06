# Serveur Lawmia 🧑‍⚖️

**Le meuilleur outils pour les avocats.**

## Fonctionalités principales 😎

* 📁 **Stockez et organisez vos données** | Vous pouvez stocker vos fichiers, dossiers clients, calendriers et plus.
* 🔧 **Trousse à outils** | Planificateur de tâches, signature électronique, gestionnaire de PDF, chronomètres multiples, dictaphone et bien plus encore.
* 🙌 **Collaborez avec les autres** | …en donnant aux autres avocats l'accès aux fichiers et dossiers dont vous autorisez le visionnage ou la modification dans vos dossiers client.
* 🔒 **Sécurité** | Avec des systèmes de chiffrement, [HackerOne bounty program](https://hackerone.com/nextcloud) et authentification à deux facteurs.

Vous voulez en savoir plus sur comment vous pouvez utiliser Lawmia pour amelliorer la sécurité et la productivité de votre cabinet ? [**Découvrez toutes nos fonctionnalitées**](https://lawmia.fr/features).

## Testez Lawmia gratuitement 🎁
* 🎁 [**Demo**](https://lawmia.fr/demo/) | Navigez à traver notre environnement de démonstartion pour voir par vous même à quoi Lawmia ressemble et comment il s'utilise.
* 🎁🖥 [**Compte d'essai**](https://lawmia.fr/trial/) | Créez un compte pour votre cabinet et obtenez gratuitement votre serveur Lawmia pour votre cabinet. 

## Récupérez votre Lawmia 📦

- ☑️ [**Choisissez**](https://lawmia.fr/signup/) simplement les services proposés par Lawmia services qui vous intéressent (hébergement, formation, customisation, installation, développement de fonctionnalités).
- 🖥 [**Installez**](https://lawmia.fr/install/#instructions-server) un serveur par vous-même sur votre infrastructure.

Vous pouvez aussi [nous contactez si vous avez des questions sur Lawmia](https://lawmia.fr/support) !

## Rejoignez l'équipe 👪

Il y a plein de manières de contribuer au projet 🙌 le développement est l'un d'eux ! Découvrez [comment vous pouvez contribuer](https://lawmia.fr/contribute/), nottament en tant que designer (UX/UI), testeur et plus encore. 😍 

## Notre lien avec Nextcloud

Parce-que ce projet est un fork de nextcloud les guides qu'il proposent pour l'envirennement de développement conviennent à la mise en place d'un environnement de développement pour Lawmia. Les auteurs indiqués dans le code de Lawmia peuvent être des auteurs du code de Nextcloud il faut les laisser.

### Environnement de développement 👩‍💻

1. 🏗️ [Mettez en place votre environnement de développement local](https://docs.nextcloud.com/server/latest/developer_manual/getting_started/devenv.html)
2. 💡 [Choisissez une bonne idée d'amellioration](https://github.com/lawmia/lawmia-server/labels/good%20improvement%20idea)
3. 👩‍🔧 Créez une branche et faites vos changements. Souvenez-vous de signer vos commits avec `git commit -sm "Votre message de commit"`
4. ⬆ Créez un [une demande de pull](https://opensource.guide/how-to-contribute/#opening-a-pull-request) et `@mentionez` les personnes qui on émis la demande pour une revue dans changements proposés.
5. 👍 Réparez les problèmes soulevés durant l'analyse.
6. 🎉 Puis attendez que vos changements soit ajoutés !

Nous avons choisi de garder le mode de fonctionnement de Nextcloud pour les applications, il y a donc plusieurs applications qui ne sont pas incluse dans la branche `master`, elles on chacunes un git pour pouvoir facilement suivre le développement de chacunes comme [le programme de première connexion](https://github.com/lawmia/premiereconnexion) ou [les dossiers client](https://github.com/lawmia/files_clients). Dans la version finale toutes les applications sont ajoutées dans le dossier `apps` puis le fichier de configuration défini quelles fonctionalitées sont activées ou non.

Sinon, les git checkouts peuvent être utilisées comme les packets de version, il fau juste utiliser les branches `stable*`. Cependant il ne faut pas les utiliser sur un environnement de production.

### Travailler sur le code front-end 🤗

Nous ajoutons le code de [Nextcloud](https://github.com/nextcloud/server), ce qui est pertinant dans notre situation pour exploiter l'avantage principal de la communauté opensource.

#### Building

Nextcloud migre de plus en plus son code vers l'utilisation de Vue.js pour le frontend, nous suivons ce mouvement qui permet de simplifier le développement futur, ils commencent par les paramètres. Pour construire le code après un changement utilisez les commandes ci-dessous dans la racine du dossier Lawmia à l'aide d'un terminal :

```bash
# installation des dépendances
make dev-setup

# build pour le développement
make build-js

# build pour le développement et suivre les modifs
make watch-js

# build pour la production avec miniaturisation
make build-js-production
```

#### Envoi des modifications (commit)

**Quand vous envoyez vos modification, pensez à y inclure les fichers compilés!**

Pour le moment les tempalates Handlebars sont encore utilisé dans certains endroits nottament dans Files et Settings. Ils sont progressivement remplacé par Vue.js mais pour le moment il faut les compiler séparément.

Si Handlebars n'est pas encore installé il faut utiliser la commande suivante dans le terminal :
```bash
sudo npm install -g handlebars
```
Ensuite dans la racine de votre dossier de développement de lawmia exécutez cette commande à chaque changement de fichier `.handlebars` pour le compiler :
```bash
./build/compile-handlebars-templates.sh
```
Avant de vérifier les modif en JS il faut également construire Lawmia pour la production :
```bash
make build-js-production
```
Puis ajoutez les fichiers compilés pour votre commit.

Pour gagner du temp et construire juste une application vous pouvez utiliser la commande suivante en remplacant le module par le nom de l'application :
```bash
MODULE=user_status make build-js-production
```

Si vous avez déjà utilisé `make build-js` ou `make watch-js` vous remarquerez que beacoup de fichiers seront noté comme différent, il faut d'abord nettoyer votre espace de travail avant de commit.

### Travailler sur le code back-end 🏗️

Quand vous changez le code PHP du back-end normalement il n'y a rien à faire de spécial avant de vérifier que ça fonctionne.

Cependant si de nouveaux fichiers sont créé il va falloir executer la commande suivante pour mettre à jour les fichier autoloader :
```bash
build/autoloaderchecker.sh
```

Après cela , s'il vous plaît pensez à inclure vos fichiers autoloader avant votre commit.

### Les outils utilisés 🛠️

- [👀 BrowserStack](https://browserstack.com) pour les tests multi navigateur
- [🌊 WAVE](https://wave.webaim.org/extension/) pour les tests d'accesibilité
- [🚨 Lighthouse](https://developers.google.com/web/tools/lighthouse/) pour les tests d'accesibilité, performance et plus


## Règles pour les contributions 📜

Toutes les contributions à ce repository sont sous la licence AGPLv3 ou tout autre version ultérieur.

Lawmia de requière pas d'ALC (Accord de Licence Contributeur).
Les copyright appartiennent à tous les contributeurs individuels.
En l'espèce nous requièrons que chaque contributeur ajoute la ligne suivante dans chaque entête de fichier dès qu'un changement majeur y a été effectué :

```
@copyright Copyright (c) <annéer>, <Votre nom prénom> (<votre adresse mail>)
```

Veuillez lire le [code de bonne conduite](https://nextcloud.com/community/code-of-conduct/).
Ce document permet de s'assurer que tous le monde puisse contribuer de manière efficiente dans une atmosphère positive et inspirante. Il explique également comment ensemble nous pouvons devenir plus fort et s'aider.ere, and to explain how together we can strengthen and support each other.

S'il-vous-plaît lisez également [les règles de la contribution](.github/CONTRIBUTING.md) de ce dépôt.

Plus d'info sur la contribution : [https://nextcloud.com/contribute/](https://nextcloud.com/contribute/)
