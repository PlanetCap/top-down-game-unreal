# Top-Down Project Structure

*Documented on: June 3rd, 2025*

This document outlines the complete project structure for our top-down action game in Unreal Engine, including blueprints, data structures, and naming conventions.

## 📁 Project Structure

### Characters
```
/Characters
  /Player
    - BP_PlayerCharacter (base) → Main player with movement and abilities
    - BP_PlayerAnimBP → Player animations
    
  /Enemies
    - BP_EnemyBase (base) → Generic enemy base class
    - BP_BossEnemy (child) [BP_EnemyBase] → Boss with special abilities
    - BP_EnemyAIController → Enemy AI logic
    - Animations/
    - SkeletalMeshes/
```

### Weapons System
```
/Weapons
  /Blueprints
    - BP_WeaponActor → Collectible weapon in the world
    - BP_ProjectileBase (base) → Generic projectile
    - BP_Projectile_Fire (child) [BP_ProjectileBase] → Fire damage projectile
    - BP_Projectile_Laser (child) [BP_ProjectileBase] → Laser beam projectile
    
  /Logic
    - BP_WeaponLogicBase (base UObject) → Base weapon logic
    - BP_WeaponLogic_Single (child) [BP_WeaponLogicBase] → Single shot
    - BP_WeaponLogic_Radial (child) [BP_WeaponLogicBase] → Circular shooting
    - BP_WeaponLogic_Burst (child) [BP_WeaponLogicBase] → Burst fire
    
  /Components
    - BP_WeaponComponent → Equipped weapon component
    - BP_AutoShootComponent → Auto-shoot when detecting enemies
    
  /Meshes/
  /VFX/
  /Sounds/
```

### Combat System
```
/Combat
  /Components
    - BP_HealthComponent → Health, damage and death
    - BP_XPComponent → Experience and level system
    - BP_StatusEffectComponent → Applies effects like fire or slow
    
  /Effects
    - BP_ExplosionEffect → Visual explosion effect
    - BP_StatusEffect_Burn (child) [BP_StatusEffectComponent] → Progressive fire damage
    - BP_StatusEffect_Slow (child) [BP_StatusEffectComponent] → Slows affected target
    
  /Upgrades
    - BP_UpgradeBase (base UObject) → Base upgrade applicable to player
    - BP_Upgrade_IncreaseDamage (child) [BP_UpgradeBase] → Damage upgrade
    - BP_Upgrade_HealOnKill (child) [BP_UpgradeBase] → Heal on enemy kill
```

### Pickups
```
/Pickups
  - BP_Pickup_Weapon → Weapon that player can collect
  - BP_Pickup_Upgrade → Passive or active upgrade
  - BP_Pickup_Heal → Restores health when collected
```

### Game Management
```
/Game
  - BP_GameMode_Main → Controls rules, waves, start/end
  - BP_GameState → Shared game state
  - BP_GameInstance → Persistent data between levels
  - BP_WaveManager → Manages wave logic
```

### User Interface
```
/UI
  /Widgets
    - WBP_HUD → Main player HUD
    - WBP_HealthBar → Health bar
    - WBP_XPBar → Experience bar
    - WBP_UpgradeSelector → Upgrade selection
    
  /Textures/
  /Fonts/
```

### Data Assets
```
/Data
  /Tables
    - DT_Weapons → Weapon data table
    - DT_Enemies → Enemy types table
    - DT_Waves → Wave configuration table
    - DT_Upgrades → Available upgrades table
    
  /Structs
    - FWeaponData → Weapon struct
    - FEnemyData → Enemy struct
    - FWaveConfig → Wave configuration struct
    - FUpgradeData → Upgrade data struct
    
  /Enums
    - EWeaponType → Weapon type
    - EEnemyType → Enemy type
    - EUpgradeType → Upgrade type
    
  /Interfaces
    - BPI_Interactable → Allows interaction with pickups
    - BPI_Damageable → Defines how to receive damage
    - BPI_StatusEffectReceiver → Receives and processes status effects
```

## 📊 Data Structures

### 🟦 FWeaponData – Weapon Data

| Field | Data Type | Description |
|-------|-----------|-------------|
| `WeaponID` | `FName` | Unique weapon identifier |
| `DisplayName` | `FText` | Visible name in interface |
| `BaseDamage` | `float` | Damage per hit/shot |
| `Cooldown` | `float` | Time between each attack |
| `Range` | `float` | Maximum attack distance |
| `StatusEffectChance` | `float (0.0–1.0)` | Probability of applying effect |
| `Icon` | `UTexture2D*` | Weapon icon for UI |
| `FireSound` | `USoundBase*` | Sound played when firing |
| `SM_Asset` | `TSoftObjectPtr<UStaticMesh>` | Weapon mesh |
| `WeaponType` | `EWeaponType` | Weapon type (Ex: Radial, Laser, Melee) |
| `WeaponLogicClass` | `Class BP_WeaponLogic_Burst` | Logic that controls shooting |
| `StatusEffectClass` | `Class BP_StatusEffect_Burn` | Effect applied if activated |

### 🟥 FEnemyData – Enemy Data

| Field | Data Type | Description |
|-------|-----------|-------------|
| `EnemyID` | `FName` | Unique enemy identifier |
| `DisplayName` | `FText` | Visible name |
| `EnemyClass` | `TSubclassOf<AActor>` | Enemy blueprint to instantiate |
| `MaxHealth` | `float` | Maximum health |
| `Damage` | `float` | Damage dealt to player |
| `MoveSpeed` | `float` | Movement speed |
| `XPGranted` | `int` | Experience granted on death |
| `Mesh` | `TSoftObjectPtr<USkeletalMesh>` | Visual mesh |
| `SpawnEffect` | `UNiagaraSystem*` | Visual effect on spawn (optional) |
| `EnemyType` | `EEnemyType` | Enemy classification (Normal, Boss, etc.) |
| `Tags` | `GameplayTagContainer` | (optional) Allows categorization or filtered logic |

### 🟩 FWaveConfig – Wave Configuration

| Field | Data Type | Description |
|-------|-----------|-------------|
| `WaveID` | `FName` | Wave identifier |
| `DisplayName` | `FText` | Visible name (ex. "Final Wave") |
| `EnemyEntries` | `TArray<FEnemySpawnEntry>` | List of enemies with quantity per type |
| `SpawnInterval` | `float` | Time between each enemy spawned |
| `SpawnDelay` | `float` | Wait time when starting the wave |
| `IsBossWave` | `bool` | If it's a special boss wave |
| `RewardMultiplier` | `float` | Multiplier for XP, drops, etc. on completion |

> 💡 **FEnemySpawnEntry** auxiliary struct:
> - `EnemyID` (FName)
> - `Quantity` (int)

### 🟨 FUpgradeData – Upgrade Data

| Field | Data Type | Description |
|-------|-----------|-------------|
| `UpgradeID` | `FName` | Unique upgrade identifier |
| `DisplayName` | `FText` | Visible name in UI |
| `Description` | `FText` | Upgrade description |
| `UpgradeClass` | `TSubclassOf<UUpgradeBase>` | Logic class that applies the upgrade |
| `Icon` | `UTexture2D*` | Icon shown in selection |
| `UpgradeType` | `EUpgradeType` | Classification (Active, Passive, Instant...) |
| `Rarity` | `int (or enum)` | Rarity level for spawn control |
| `StatModifiers` | `TMap<FName, float>` | (optional) Dictionary with stats to modify |

## 📋 Enumerations

### 🟦 EWeaponType – Weapon Type

| Value | Description |
|-------|-------------|
| `None` | No specific type (default value) |
| `SingleShot` | Single frontal shot |
| `Burst` | Fires multiple times in burst |
| `Radial` | Circular or area shot around player |
| `Laser` | Continuous straight beam |
| `Explosive` | Fires projectile that explodes on impact |
| `Orbiting` | Rotates around player causing damage |
| `Homing` | Projectile that chases enemy |
| `Melee` | Close-range melee weapon |

### 🟥 EEnemyType – Enemy Type

| Value | Description |
|-------|-------------|
| `Normal` | Common enemy, no special abilities |
| `Fast` | Low health but high speed enemy |
| `Tank` | High health and reduced speed enemy |
| `Exploder` | Self-destructs when approaching player |
| `Shooter` | Attacks at distance with projectiles |
| `Swarm` | Appears in large quantities, low health |
| `Boss` | Powerful boss with unique behavior |

### 🟨 EUpgradeType – Upgrade Type

| Value | Description |
|-------|-------------|
| `Passive` | Automatic upgrade (damage, speed, health...) |
| `Active` | Upgrade that player can manually activate |
| `OnKill` | Activates when eliminating enemies |
| `Instant` | Applies immediately when collected |
| `WeaponModifier` | Affects only equipped weapon (direct upgrade) |
| `Aura` | Upgrade that generates constant effect around it |

## 🔗 Interfaces

### BPI_Interactable
- Allows interaction with pickups and interactive objects
- Methods: `OnInteract()`, `CanInteract()`, `GetInteractionText()`

### BPI_Damageable
- Defines how entities receive damage
- Methods: `TakeDamage()`, `GetCurrentHealth()`, `OnDeath()`

### BPI_StatusEffectReceiver
- Receives and processes status effects
- Methods: `ApplyStatusEffect()`, `RemoveStatusEffect()`, `GetActiveEffects()`

---

**Related Documentation:**
- [File Naming Conventions](file-naming-conventions.md)
- [Blueprint Architecture](../architecture/blueprints.md)
- [Coding Standards](coding-standards.md)

*This structure follows our established naming conventions and modular design patterns for maintainable and scalable development.*