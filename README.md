# AM32 — Exuav / MAD Motors Lightning 70A (AT32F421)


Firmware AM32 **v2.20** pour l’ESC standalone **Exuav / MAD Motors Lightning 70A 3–6S** (MCU **AT32F421K8U7**, 32×16,5 mm).
Deux variantes sont proposées : LED fixe (comportement standard) ou LED configurable via le configurator AM32.
---
## Matériel compatible
| Élément | Détail |
|---------|--------|
| ESC | Exuav / MAD Motors **Lightning 70A** standalone |
| MCU | Artery **AT32F421K8U7** |
| Tension | 3–6S LiPo |
| LED | RGB **discrète** (3 GPIO) — **PB8** rouge, **PB5** vert, **PB3** bleu |
| Base firmware | Dérivé de la cible AM32 `AT32DEV_F421` (documentée NeutronRC / MAD Motors) |
> **Non compatible** avec la variante AIO 4-en-1 (`NEUTRON_2_6S_AIO_F421`).
---
## Fichiers firmware
| Fichier | Nom configurator | Usage |
|---------|------------------|-------|
| `AM32_EXUAV_LIGHTNING_70A_F421_2.20.hex` | **Exuav70A** | LED fixe — rouge désarmé, vert armé |
| `AM32_EXUAV_LIGHT_HE_70A_F421_2.20.hex` | **ExuavHE70** | LED configurable via **Use Hall Sensors** |
### Variante LIGHTNING (standard)
| État | Couleur |
|------|---------|
| Désarmé | Rouge |
| Armé | Vert |
### Variante LIGHT_HE (configurable)
Permet d’attribuer une couleur d’armement différente par ESC via le configurator AM32, en réutilisant l’option **Use Hall Sensors** (aucun capteur Hall requis sur l’ESC) :
| État | Use Hall Sensors **OFF** | Use Hall Sensors **ON** |
|------|--------------------------|-------------------------|
| Désarmé | Rouge | Rouge |
| Armé | **Vert** | **Rouge** |
**Exemple — quad 4 moteurs, 2 paires :**
- ESC paire 1 → firmware **LIGHT_HE**, Use Hall Sensors **OFF** → vert à l’armement
- ESC paire 2 → firmware **LIGHT_HE**, Use Hall Sensors **ON** → rouge à l’armement
La variante **LIGHTNING** convient si vous n’avez pas besoin de différencier les paires de moteurs.
---
## Flash
1. Ouvrir [AM32 Configurator](https://am32.ca) (Web ou desktop).
2. Connecter l’ESC (signal wire + alimentation).
3. **Flash Firmware** → sélectionner le `.hex` correspondant.
4. Après flash, vérifier le nom affiché : `Exuav70A` ou `ExuavHE70`.
> Flasher **uniquement** le fichier adapté à votre besoin. Les deux variantes partagent la même base moteur ; seul le comportement LED diffère.
---
## Réglages configurator recommandés
| Paramètre | Valeur | Note |
|-----------|--------|------|
| Protocole | **DShot600** (ou PWM) | Selon votre FC |
| Bi-directional DShot | **ON** | Si télémétrie RPM via DShot |
| 30 ms Telemetry | **OFF** | À garder OFF avec DShot bi-directionnel |
| Motor KV | **300** | Pour moteurs ~310 KV (granularité firmware : pas de 40 KV) |
| Use Hall Sensors | Voir variante | **LIGHT_HE** uniquement — contrôle couleur armé |
---
## English summary
Custom AM32 **v2.20** firmware for the **Exuav / MAD Motors Lightning 70A** standalone ESC (AT32F421K8U7) with discrete RGB LED support (PB8/PB5/PB3).
- **`AM32_EXUAV_LIGHTNING_70A_F421_2.20.hex`** — Fixed LED: red disarmed, green armed.
- **`AM32_EXUAV_LIGHT_HE_70A_F421_2.20.hex`** — Configurable armed color via configurator **Use Hall Sensors** (OFF = green armed, ON = red armed). No physical Hall sensor required.
Flash with the [AM32 Configurator](https://am32.ca). Keep **30 ms Telemetry** OFF when using bi-directional DShot.
---
## Avertissement
Firmware communautaire, non officiel Exuav / MAD Motors / AM32.  
Utilisation à vos risques. Vérifiez le bon modèle d’ESC avant flash.  
Conservez un firmware stock ou un backup EEPROM si possible.
---
## Crédits
- [AM32](https://github.com/am32-firmware/AM32) — firmware open source
- Base cible : `AT32DEV_F421`
- Broches LED confirmées via cible `ODDITYRC_F80_F421`
