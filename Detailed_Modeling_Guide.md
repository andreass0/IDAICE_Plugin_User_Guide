# Detailed Modeling Guide

This section provides in-depth documentation for configuring key model components in SIMULTAN for use with the IDA-ICE Plugin.

---

## Building Envelope

The building envelope defines the physical boundary of the conditioned space and includes opaque, transparent, and shading components.

Since most of the data of the building envelope will already be provided with an architectual model the structure of the
plugin focuses on expanding the already existing information, so it is containing all the calculation relevant
information and can be exported to IDA-ICE.

### Opaque Building Components

Opaque elements include walls, slabs, and roofs. To define them:

```{figure} img/Opaque-building-components.png
---
height: 225px
align: center
name: fig-Opaque-building-components
---
Overview of all opaque building components
```

1. Open the **Construction** tab in the plugin UI.
2. Use `Select construction` to view connected surfaces.
3. Use `Edit construction` to set:

   * **Construction Name**
   * **Surface Type**
   * **Layers**: Defined by name, material, and thickness

- Layer Name: Shows the name of your choosen layer. <!-- Kontrollieren ob es wirklich nur diese Funktion hat! -->
- Material: Shows the material of your choosen layer, [**Materials**](#material-properties)
- Thickness: Shows the Thickness (m) of your choosen layer


```{figure} img/overview-constructiontab.png
---
name: overview-constructiontab
---
Construction tab overview
```

```{note}
**Any change made here directly updates the simulation data model.** That's why it is very important to work carefully in the user interface, changes are applied directly, even without explicitly saving or simply closing the user interface.
```

---

### Transparent Building Components

Transparent elements include windows and doors.

The datastructure to export transparent constructions will be shown for a Fenster (window). The procedure is analogues for a
door and other `glass constructions`.

```{figure} img/TransperentBuildingComponents-UI.png
---
name: TransperentBuildingComponents-UI
---
Example: window definition UI
```

The parameters in the image relate to the material properties of transparent components (such as windows) in the IDA ICE building simulation software. These values strongly influence the thermal and solar behavior of the glazing. Here is an explanation of the terms and their meaning.  

**Key parameters:**

* **Solar Heat Gain Coefficient (g)**   
Proportion of solar radiation that enters the building through the window (direct + secondary through heating of the glass).   
* **Solar Transmittance (T)**   
Proportion of directly transmitted solar radiation (without secondary heat conduction).   
* **Visible Transmittance (Tvis)**   
Proportion of visible light that passes through the glazing.  
* **Thermal Conductivity (U)**  
Radiant heat emission from the inner surface (e.g. glass) to the inside.  
* **Emissivity (internal/external)**  
The opposite of 6. so for the outside of the window   

```{note}
**These values are used in IDA ICE to:**

- Calculate heat loss in winter and heat input in summer
- simulate the daylight input, risk of overheating and the energy requirement for heating/cooling
- find optimal window configurations in terms of energy efficiency
```

---

### Shading Elements

A central element in IDA-ICE is the consideration of shading, as it has a considerable influence on daylight, cooling and heating loads and the indoor climate. This is why the plugin has a separate area for this, as you can see in {numref}`Shades-UI`.

```{figure} img/Shades-UI.png
---
name: Shades-UI
---
User interface for shading definition
```

**Parameters include:**

* **Longwave Emissivity**   
Indicates how strongly a surface can emit long-wave heat radiation (infrared).   
* **Shortwave Reflectance**   
Proportion of short-wave sunlight reflected by the surface (in %).  
* **Roughness**   
Beschreibt, wie rau eine Oberfläche ist, was sich auf die Streuung von Licht auswirkt.  
* **Specularity**   
How strongly a surface reflects (directionally).  
* **Transparency**   
How much visible light is transmitted through the surface.  

---

```{tip}
The parameters for the shadings change for each material. This is precisely why this user interface is so important. In IDA-ICE, a distinction is made not only between materials but also between shading types. Here is the most important thing you need to know about them:
```

| Shading Type | Description             | Example                    |
| ------------ | ----------------------- | -------------------------- |
| Fixed        | Architectural overhangs | Balconies, concrete shades |
| Horizontal   | Adjustable louvers      | Awnings                    |
| Vertical     | Side fins               | Deep window recesses       |
| Contextual   | Neighboring buildings   | Trees, adjacent structures |
| Integrated   | Window-mounted          | Venetian blinds            |

```{note}
Shading settings influence both energy performance and daylight modeling.
```

---

## HVAC Configuration via ESBO

The HVAC-System is implemented via the ESBO-Plant of IDA-ICE. {numref}`esbo_simultan` shows all the possible inputs
which are exported with the plugin.

```{figure} img/Esbo-UI.png
---
name: esbo_simultan
---
SIMULTAN components for ESBO systems
```

**In the plugin UI:**

* Use the **Edit Component** area to define system-specific parameters
* Components can be **disabled** if needed

```{tip}
**Disabling a component unlinks all associated data.**
```

```{figure} img/ESBOplant-UI.png
---
name: esbo_off
---
Component toggled off
```

---

```{figure} img/esbo-on.png
---
name: system-on
---
HVAC system enabled
```

```{figure} img/esbo_off.png
---
name: system_off
---
HVAC system disabled
```

```{warning}
**Ensure no conflicting or duplicate HVAC systems are exported to IDA-ICE. This may result in simulation errors.**
```

---

## Internal Gains

The modelling of internal gains due to occupant behaviour is also possible. The SIMULTAN representation is stored under
the component `Nutzung`. This component stores sub-components for each simulation-zone and the assigned internal gains.

```{figure} img/inernal_gains_comp.png
---
name: inernal_gains_comp
---
Internal gains definition
```

Subcomponents include:

* **Equipment**
* **Lighting**
* **Occupants**

each with the needed parameters to describe the needed information for the simulation.

```{figure} img/equipment_para.png
---
name: equipment_para
---
Parameters for equipment gains
```

```{figure} img/light_para.png
---
name: light_para
---
Parameters for lighting gains
```

```{figure} img/occupant_para.png
---
name: occupant_para
---
Parameters for occupant gains
```

---

## Material Properties

`Materials` have been given their own area in the **IDA-ICE-Plugin**. This once again allows users to keep their materials organized and to proceed in a structured manner.

```{figure} img/materials_UI.png
---
name: materials_UI
---
Materials UI
```

**Key properties:**

* **Name**
* **Thermal Conductivity** (W/m·K)   
Indicates how well the material conducts heat.  
Value 0: This means that the material does not conduct any heat at all - it acts as perfect insulation.   
* **Density** (kg/m³)   
Indicates how much mass one cubic meter of the material has.   
* **Specific Heat** (J/kg·K)   
Indicates how much energy (in joules) is required to heat 1 kg of material by 1 Kelvin.   

```{note}
**These parameters determine how materials conduct and store heat within simulations.**
```

New materials become available in the **Construction** tab once defined.

---

## Taxonomy Update

To restore or update all taxonomies for the IDA-ICE Plugin, use the built-in taxonomy update button.

```{figure} img/taxonomyupdate_button.png
---
name: taxonomyupdate_button
---
Taxonomy update button
```

```{warning}
This only updates taxonomy definitions—it does **not** automatically reassign taxonomies to components if the old ones were deleted.
```

---

*End of detailed modeling guide.*
