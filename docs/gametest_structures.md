---
sidebar_position: 4
---

# Utilisation des Structures dans GameTest

## Introduction

Les structures dans GameTest sont des fichiers JSON qui définissent l'environnement initial pour vos tests. Elles permettent de créer des scénarios spécifiques pour tester des fonctionnalités de jeu de manière automatisée. Ce guide vous montrera comment créer et utiliser des structures pour vos tests GameTest.

## Structures par Défaut

Par défaut, les structures utilisées dans les tests GameTest sont vides. Cela signifie que le test commence dans un environnement vide, sans aucun bloc ou entité pré-placé. Cette configuration est définie en utilisant l'annotation `@GameTest(templateName = FabricGameTest.EMPTY_STRUCTURE)`.

Exemple de test utilisant la structure par défaut :

```java
package fr.astreval.test.block;

import fr.astreval.block.ModBlocks;
import net.fabricmc.fabric.api.gametest.v1.FabricGameTest;
import net.minecraft.entity.player.PlayerEntity;
import net.minecraft.item.ItemStack;
import net.minecraft.item.Items;
import net.minecraft.test.GameTest;
import net.minecraft.test.TestContext;
import net.minecraft.util.Hand;
import net.minecraft.util.math.BlockPos;

public class MyBlockTest implements FabricGameTest {

  @GameTest(templateName = FabricGameTest.EMPTY_STRUCTURE)
  public void useBoneMeal(TestContext context) {
    BlockPos pos = new BlockPos(1, 1, 1);
    context.setBlockState(pos, ModBlocks.MY_BLOCK.getDefaultState());

    PlayerEntity player = context.createMockSurvivalPlayer();
    ItemStack boneMealStack = new ItemStack(Items.BONE_MEAL);
    player.setStackInHand(Hand.MAIN_HAND, boneMealStack);
    context.useBlock(pos, player);

    context.expectBlockProperty(pos, ModBlocks.MY_BLOCK.getAgeProperty(), 1);

    context.complete();
  }
}
```

## Créer une Structure Personnalisée

Pour tester des scénarios spécifiques, vous pouvez créer des structures personnalisées. Voici comment procéder :

1. Créer un Fichier JSON :

Créez un fichier JSON dans le dossier `src/main/resources/data/astreval-jobs/structures`.
Nommez le fichier en fonction de la structure, par exemple `my_structure.json`.

2.  Définir la Structure :

Utilisez le format JSON pour définir les blocs et les entités dans la structure.

Exemple de structure JSON :

```json
{
  "size": [3, 3, 3],
  "palette": {
    "air": { "block": "minecraft:air" },
    "stone": { "block": "minecraft:stone" }
  },
  "blocks": [
    [ "stone", "stone", "stone" ],
    [ "air", "stone", "air" ],
    [ "stone", "stone", "stone" ]
  ],
  "entities": []
}
```

###  Utiliser la Structure dans un Test

Référencez la structure dans votre méthode de test en utilisant l'annotation @GameTest.

```java
// ... existing code ...

@GameTest(templateName = "astreval-jobs:my_structure")
public void testWithStructure(TestContext context) {
  BlockPos pos = new BlockPos(1, 1, 1);
  context.setBlockState(pos, ModBlocks.MY_BLOCK.getDefaultState());

  // Ajoutez votre logique de test ici

  context.complete();
}
```

## Conclusion
Les structures dans GameTest sont un outil puissant pour créer des environnements de test réalistes et spécifiques. Par défaut, les structures sont vides, mais vous pouvez créer des structures personnalisées pour tester des scénarios complexes. En utilisant ces structures, vous pouvez automatiser vos tests et vous assurer que votre mod fonctionne comme prévu dans diverses situations.
