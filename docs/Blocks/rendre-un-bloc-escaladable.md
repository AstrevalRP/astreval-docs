---
sidebar_position: 2
---

# Rendre un bloc escaladable (Climdable)

Pour ajouter un nouveau bloc escaladable dans votre jeu en utilisant un fichier JSON, vous pouvez suivre ces étapes. Vous devez ajouter le bloc dans le fichier climbable.json comme déjà commencé dans votre exemple.

Voici comment vous pouvez structurer votre fichier climbable.json :

`src/main/resources/data/minecraft/tags/blocks/climbable.json`

```json
{
  "replace": false,
  "values": [
    "astreval-jobs:grappling_rope_block",    
    // ajoutez d'autres blocs ici si nécessaire
  ]
}
```

Étapes à suivre :
- Ajout du bloc : Assurez-vous que "astreval-jobs:grappling_rope_block" est bien listé sous "values" dans climbable.json.

Vérification de conflit : Si vous utilisez d'autres données de blocs ou ressources, vérifiez qu'il n'y a pas de conflits avec d'autres fichiers ou registres de jeu.

Testez en jeu : Lancez votre jeu et placez le bloc pour vous assurer qu'il est bien escaladable. Vous devriez pouvoir vous accrocher à ce bloc comme à une échelle ou à des lianes.

Si vous devez modifier ou ajouter des blocs supplémentaires, suivez simplement le même processus en mettant à jour la liste "values" avec les nouveaux IDs de blocs.
