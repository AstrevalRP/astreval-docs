---
sidebar_position: 1
---

# Introduction

Bienvenue dans le wiki de développement de AstrevalRP ! Ce guide est conçu pour vous aider à comprendre les bases du développement de nos mods Minecraft. Que vous soyez nouveau dans le développement ou que vous ayez déjà de l'expérience, nous espérons que ces informations vous seront utiles.

## Technologies Utilisées

### Fabric
Nous utilisons **Fabric** comme API de modding pour Minecraft. Fabric est une API légère et performante qui permet de créer des mods pour Minecraft version 1.20.1. Elle est facile à installer et à utiliser, ce qui en fait un excellent choix pour les débutants.

### Geckolib
Pour les animations et les mobs, nous utilisons **Geckolib**. Geckolib est une bibliothèque qui facilite la création d'animations complexes pour les entités dans Minecraft. Elle est compatible avec Fabric et permet de donner vie à vos créations avec des animations fluides et réalistes.

## Répertoires de Développement

### astreval-build-mod
Ce répertoire est dédié à la création de tous les blocs et éléments de construction pour le serveur. Vous y trouverez tout ce qui est nécessaire pour ajouter de nouveaux blocs, items, et structures à Minecraft.

### astreval-mod
Ce répertoire se concentre sur la logique des métiers du serveur. Il contient tout le code nécessaire pour gérer les différents métiers, leurs interactions, et leurs fonctionnalités spécifiques.

## Processus de Développement

1. **Utilisation des Répertoires Existants**:
   - Les développeurs doivent utiliser les répertoires existants `astreval-build-mod` et `astreval-mod` pour leurs contributions.
   - Assurez-vous de cloner ces répertoires depuis notre dépôt GitHub et de configurer votre environnement de développement en conséquence.

2. **Développement des Fonctionnalités**:
   - Pour `astreval-build-mod`, ajoutez de nouveaux blocs, items, ou structures en utilisant Fabric.
   - Pour `astreval-mod`, implémentez la logique des métiers et leurs interactions en utilisant Fabric et Geckolib pour les animations.

3. **Tests et Débogage**:
   - Testez régulièrement vos modifications pour vous assurer qu'elles fonctionnent comme prévu.
   - Utilisez les outils de débogage pour identifier et corriger les problèmes.

4. **Publication**:
   - Une fois vos modifications terminées, poussez-les directement sur notre dépôt GitHub.
   - Assurez-vous de suivre les bonnes pratiques de versionnage et de documentation pour faciliter la maintenance et les mises à jour futures.

## Conclusion

Le développement de mods pour Minecraft avec Fabric et Geckolib est une expérience enrichissante qui vous permet de personnaliser et d'améliorer votre jeu préféré. Ce wiki vous guidera à travers les étapes nécessaires pour contribuer à nos répertoires existants et partager vos créations avec la communauté.

N'hésitez pas à explorer les différentes sections de ce wiki pour en savoir plus sur chaque aspect du développement. Bonne chance et amusez-vous bien !
