# Créer un Item Lançable (`ThrownItemEntity`)

## Introduction

Cette documentation explique comment créer un item lançable dans Minecraft en utilisant un Grappling Hook comme exemple. Un item lançable peut être utilisé pour interagir avec le monde de manière dynamique, comme placer des objets ou appliquer des effets.

## Étapes pour Créer un Item Lançable

### Entity Class - `GrapplingHookEntity`

- Fichier : `src/main/java/fr/astreval/block/entity/GrapplingHookEntity.java`

Ajoutez une nouvelle classe étendant `ThrownItemEntity`, qui définit comment l'item se comporte lorsqu'il est lancé.

`GrapplingHookEntity.java`

```java
// ... existing code ...

public class GrapplingHookEntity extends ThrownItemEntity {
  public GrapplingHookEntity(EntityType<? extends ThrownItemEntity> entityType, World world) {
    super(entityType, world);
  }

  // Initialisation de l'entité avec d'autres paramètres...
  // Override des méthodes pour gérer les collisions...
}
```

### Enregistrement de l'Entité - `ModEntities`

- Fichier : `src/main/java/fr/astreval/entity/ModEntities.java`
Enregistrez le type d'entité afin qu'il soit reconnu par le jeu.

`ModEntities.java`

```java
// ... existing code ...

public static final EntityType<GrapplingHookEntity> GRAPPLING_ENTITY_TYPE = Registry.register(
    Registries.ENTITY_TYPE, 
    new Identifier(AstrevalJobs.MOD_ID, "grappling_hook"), 
    FabricEntityTypeBuilder.<GrapplingHookEntity>create(SpawnGroup.MISC, GrapplingHookEntity::new)
      .dimensions(EntityDimensions.fixed(0.25f, 0.25f))
      .build()
);
// ... rest of code ...
```

### Enregistrement du Rendu Client - `ModClientEntities`

- Fichier : `src/main/java/fr/astreval/entity/client/ModClientEntities.java`

Assurez-vous que votre entité a un renderer associé pour le client.

`ModClientEntities.java`

```java
// ... existing code ...

public class ModClientEntities {
  public static void registerEntities() {
    EntityRendererRegistry.register(ModEntities.GRAPPLING_ENTITY_TYPE, FlyingItemEntityRenderer::new);
  }
}
```

### Item Class - `GrapplingHookItem`

- Fichier : `src/main/java/fr/astreval/item/blacksmith/GrapplingHookItem.java`

Définissez comment l'item doit réagir quand le joueur l'utilise.

`GrapplingHookItem.java`

```java
// ... existing code ...

public class GrapplingHookItem extends Item {
  public GrapplingHookItem(Settings settings) {
    super(settings);
  }

  @Override
  public TypedActionResult<ItemStack> use(World world, PlayerEntity user, Hand hand) {
    ItemStack itemStack = user.getStackInHand(hand);
    world.playSound(null, user.getX(), user.getY(), user.getZ(),
        SoundEvents.ENTITY_SNOWBALL_THROW, SoundCategory.NEUTRAL, 0.5f, 0.4f / (world.getRandom().nextFloat() * 0.4f + 0.8f));
    if (!world.isClient) {
      GrapplingHookEntity grapplingHookEntity = new GrapplingHookEntity(user, world);
      grapplingHookEntity.setItem(itemStack);
      // Set velocity for a more arched, less powerful throw
      float velocity = 0.7f; // Reduced velocity for a lighter throw
      float inaccuracy = 1.0f; // Adjust as needed for more arch
      grapplingHookEntity.setVelocity(user, user.getPitch() - 20.0f, user.getYaw(), 0.0f, velocity, inaccuracy);
      world.spawnEntity(grapplingHookEntity);
    }
    user.incrementStat(Stats.USED.getOrCreateStat(this));
    if (!user.getAbilities().creativeMode) {
      itemStack.decrement(1);
    }
    return TypedActionResult.success(itemStack, world.isClient());
  }
}
```

Cette méthode use illustre comment l'item est lancé par le joueur, en créant l'entité GrapplingHookEntity et en lui appliquant une vélocité ajustée. Le son de lancer est joué, et l'item est consumé à moins que le joueur ne soit en mode créatif.

## Conclusion

En suivant ces étapes, vous pouvez créer votre propre item lançable dans Minecraft. Le Grappling Hook sert d'exemple de base pour implémenter des fonctionnalités similaires.
