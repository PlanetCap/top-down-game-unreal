# File Naming Conventions

This document outlines the file naming standards for our Unreal Engine project. Consistent naming helps with organization, searchability, and team collaboration.

## Quick Reference

| Asset Type | Prefix | Example |
|------------|--------|---------|
| Blueprint Actor | `BP_` | `BP_PlayerCharacter` |
| Blueprint Component | `BPC_` | `BPC_HealthComponent` |
| Widget Blueprint | `WBP_` | `WBP_MainMenu` |
| Animation Blueprint | `ABP_` | `ABP_PlayerAnimations` |
| Static Mesh | `SM_` | `SM_Rock_01` |
| Skeletal Mesh | `SK_` | `SK_PlayerCharacter` |
| Texture | `T_` | `T_PlayerSkin_Diffuse` |
| Material | `M_` | `M_PlayerSkin_Master` |
| Material Instance | `MI_` | `MI_PlayerSkin_Variant01` |
| Audio | `A_` | `A_Player_Footstep_Grass` |

## Blueprint Files naming examples

### Actor Blueprints
```
Format: BP_[Category]_[Name]_[Variant]
Examples:
- BP_PlayerCharacter
- BP_Enemy_Goblin
- BP_Weapon_Sword_Magic
- BP_Pickup_Health_Small
- BP_Interactable_Door_Wooden
```

### Component Blueprints
```
Format: BPC_[Functionality]Component
Examples:
- BPC_HealthComponent
- BPC_InventoryComponent
- BPC_MovementComponent
- BPC_InteractionComponent
```

### Interface Blueprints
```
Format: BPI_[InterfaceName]
Examples:
- BPI_Interactable
- BPI_Damageable
- BPI_Collectible
- BPI_Spawnable
```

### Widget Blueprints (UI)
```
Format: WBP_[UIType]_[Name]
Examples:
- WBP_MainMenu
- WBP_HUD_Player
- WBP_Dialog_Confirmation
- WBP_Inventory_Slot
- WBP_Settings_Audio
```

### Animation Blueprints
```
Format: ABP_[Character/Object]_[Type]
Examples:
- ABP_Player_Locomotion
- ABP_Enemy_Combat
- ABP_Weapon_Sword
- ABP_Vehicle_Car
```

### Other Blueprint Types
```
Blueprint Function Library: BPF_[Category]Utils
- BPF_MathUtils
- BPF_StringUtils
- BPF_GameplayUtils

Behavior Tree: BT_[AI_Name]
- BT_Enemy_Patrol
- BT_NPC_Merchant

Blackboard: BB_[AI_Name]
- BB_Enemy_Base
- BB_NPC_Citizen
```

### Interface Files
```
Format: I[InterfaceName].h
Examples:
- IInteractable.h
- IDamageable.h
- ICollectible.h
```

### Utility Files
```
Format: [Category]Utils.h/.cpp
Examples:
- MathUtils.h/.cpp
- StringUtils.h/.cpp
- GameplayUtils.h/.cpp
```

## Asset Files

### Meshes
```
Static Mesh: SM_[Category]_[Name]_[Variant]_[LOD]
- SM_Prop_Crate_01
- SM_Building_House_Medieval_LOD0
- SM_Weapon_Sword_Iron
- SM_Environment_Rock_Large_01

Skeletal Mesh: SK_[Character/Object]_[Variant]
- SK_Player_Male
- SK_Enemy_Goblin_Warrior
- SK_Weapon_Bow_Elven
```

### Materials
```
Master Material: M_[Category]_[Type]_Master
- M_Character_Skin_Master
- M_Environment_Rock_Master
- M_UI_Button_Master

Material Instance: MI_[Category]_[Name]_[Variant]
- MI_Character_Player_Skin01
- MI_Environment_Rock_Dark
- MI_UI_Button_Hover

Material Function: MF_[Function]
- MF_NoiseGenerator
- MF_FresnelEffect
- MF_VertexAnimation
```

### Textures
```
Format: T_[Object]_[MapType]_[Resolution]
Map Types: Diffuse, Normal, Roughness, Metallic, AO, Emissive

Examples:
- T_PlayerSkin_Diffuse_1024
- T_PlayerSkin_Normal_1024
- T_Rock_Diffuse_512
- T_Metal_Roughness_512
- T_UI_Button_Diffuse_256
```

### Audio
```
Format: A_[Category]_[Name]_[Variant]
Categories: Music, SFX, Voice, UI

Examples:
- A_Music_MainTheme
- A_SFX_Player_Footstep_Grass
- A_SFX_Weapon_Sword_Swing
- A_Voice_Player_Hurt_01
- A_UI_Button_Click
- A_UI_Button_Hover
```

### Animations
```
Animation Sequence: A_[Character]_[Action]_[Variant]
- A_Player_Idle
- A_Player_Walk_Forward
- A_Player_Attack_Sword_01
- A_Enemy_Death_Backward

Animation Montage: AM_[Character]_[Action]
- AM_Player_Attack_Combo
- AM_Player_Dodge_Roll
- AM_Enemy_Special_Attack

Blend Space: BS_[Character]_[Type]
- BS_Player_Locomotion
- BS_Player_Aim_Offset
```

## Level Files
```
Format: L_[LevelType]_[Name]_[Variant]
Types: Menu, Gameplay, Test, Template

Examples:
- L_MainMenu
- L_Gameplay_Forest_01
- L_Gameplay_Dungeon_Boss
- L_Test_PlayerMovement
- L_Template_BasicLevel
```

## Data Assets
```
Data Table: DT_[Category]_[Type]
- DT_Weapons_Stats
- DT_Characters_Dialogue
- DT_Items_Properties

Curve Table: CT_[Category]_[Type]
- CT_Gameplay_LevelProgression
- CT_Audio_VolumeSettings

Enum: E_[Category][Name]
- E_WeaponType
- E_PlayerState
- E_DamageType
```
