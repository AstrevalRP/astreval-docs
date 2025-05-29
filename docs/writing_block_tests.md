---
sidebar_position: 3
---

# Écrire des Tests pour un Bloc

## Introduction

Ce guide vous montrera comment écrire des tests pour un bloc en utilisant GameTest sur le repo Astreval Jobs. Vous apprendrez à créer des tests simples, à utiliser des structures pour les tests, et à exploiter les méthodes d'aide fournies par `TestHelper.java`.

## Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants :
- Une installation de Minecraft 1.20.1 avec Fabric Loader.
- Le mod Astreval Jobs installé.
- Une bonne compréhension de base de Java et de l'API Minecraft.

## Ajouter un Test Simple

Pour ajouter un test simple, suivez ces étapes :

1. **Créer une nouvelle classe de test** :
   - Créez un nouveau fichier Java dans le package `fr.astreval.test.block` (ou un autre package approprié).
   - Nommez le fichier en fonction de ce que vous testez, par exemple `MyBlockTest.java`.

2. **Implémenter l'interface `FabricGameTest`** :
   - Implémentez l'interface `FabricGameTest` dans votre classe de test.
   - Ajoutez des méthodes de test annotées avec `@GameTest`.

Voici un exemple de test simple pour un bloc :

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

## Utiliser TestHelper.java
TestHelper.java propose plusieurs méthodes pour simplifier l'écriture des tests. Ces méthodes incluent des fonctions pour simuler l'utilisation d'items par un joueur et pour vérifier que le nombre d'items dropés est dans une plage spécifique.

### Méthodes Disponibles
- `abstractPlayerUseItemOnBlock(TestContext context, BlockPos pos, Item stack)` : Simule l'utilisation d'un item par un joueur sur un bloc.
- `abstractPlayerUseEmptyItemOnBlock(TestContext context, BlockPos pos)` : Simule l'utilisation d'un item vide par un joueur sur un bloc.
- `expectItemsInRange(TestContext context, Item item, BlockPos pos, double radius, int minAmount, int maxAmount)` : Vérifie que le nombre d'items dropés est dans une plage spécifique.

### Exemple d'Utilisation
Voici un exemple de test utilisant TestHelper :

```java
// ... existing code ...

import fr.astreval.test.utils.TestHelper;

public class MyBlockTest implements FabricGameTest {

  @GameTest(templateName = FabricGameTest.EMPTY_STRUCTURE)
  public void useScythe(TestContext context) {
    BlockPos pos = new BlockPos(1, 1, 1);
    context.setBlockState(pos, ModBlocks.MY_BLOCK.getDefaultState());

    TestHelper.abstractPlayerUseItemOnBlock(context, pos, ModItems.IRON_SCYTHE);

    TestHelper.expectItemsInRange(context, ModBlocks.MY_BLOCK.asItem(), pos, 1.0, 2, 3);

    context.complete();
  }
}
```

## Ajouter le Fichier de Test dans fabric.mod.json

Pour que vos tests soient exécutés, vous devez ajouter le fichier de test dans le fichier `fabric.mod.json`.

### Ajouter le Fichier de Test
Localiser le Fichier :
 
Le fichier se trouve dans `src/main/resources/fabric.mod.json`.
Ajouter le Chemin du Fichier de Test :

Ajoutez le chemin de votre fichier de test dans la section entrypoints sous fabric-gametest.
Exemple :

```json
{
  ...
  "entrypoints": {
   ...
    "fabric-gametest": [
      "fr.astreval.test.ModTests",
      "fr.astreval.test.block.SquaringStationBlockTest",
      "fr.astreval.test.block.BushBlockTest",
      "fr.astreval.test.block.MushroomPlantBlockTest",
      "fr.astreval.test.item.FertilizerBagTest",
      "fr.astreval.test.item.SeedsTest",
      "fr.astreval.test.block.MyBlockTest" // Ajoutez votre fichier de test ici
    ]
  },
  ...
}
```

## Conclusion
Vous avez maintenant les bases pour écrire des tests pour un bloc en utilisant GameTest sur le repo Astreval Jobs. Utilisez les structures pour définir des environnements de test, exploitez les méthodes d'aide de TestHelper.java, et n'oubliez pas d'ajouter vos fichiers de test dans fabric.mod.json.
