## Setting up a Problem

This chapter provides a brief overview of how data is structured within the underlying data model.

---

## Data Structure for the Plugin

In {numref}`ida_data`, a simplified illustration of the required data structure for running the plugin is shown. This structure holds all the necessary information to enable dynamic multizone climate and energy simulations in IDA-ICE.

```{figure} img/schematic_comp_ida.jpg
---
height: 500px
name: ida_data
---
Simplified representation of the required data structure to run the plugin.
```

A more in-depth description of the SIMULTAN data representation for building physics simulations can be found in the chapter [SIMULTAN Datastructure to incorporate the IDA-ICE Data model](SIMULTAN_Datastructure_to_incorporate_the_IDAICE_Data_model.md).

```{warning}
Although it is technically possible to define this structure manually, we strongly recommend using the provided templates to avoid errors. Manual modeling is error-prone and can lead to time-consuming troubleshooting.
```

The data structure consists of two main elements:

1. [Taxonomies](#taxonomies)
2. [Components](#components)

---

### Taxonomies

Taxonomies are classification systems used to organize elements into hierarchical categories and subcategories. They help structure complex models and define relationships between entities.

```{note}
Components that are not assigned to a taxonomy are ignored by SIMULTAN.
```

#### IDA-ICE Relevant Taxonomies

The IDA-ICE plugin introduces new taxonomies essential for establishing the connection between IDA-ICE and SIMULTAN. Tools of the plugin's [user interface](#modeling-for-ida-ice) <!-- verknüpfung zur nächsten seite!-->automatically assign the appropriate taxonomy to each component for compatibility.

```{figure} img/taxonomies_idaice.png
---
name: taxonomies_idaice
---
Overview of IDA-ICE taxonomies
```

We recommend starting with one of the provided `template files` <!--Link-->to ensure synchronization and reduce the risk of errors. To restore the complete taxonomy hierarchy required by the plugin, refer to the section on [taxonomy updates](#taxonomy-update). <!-- verknüpfung zur nächsten seite!-->

<!-- TODO: Insert link to taxonomy template file -->

---

### Components

Components represent the functional building blocks of a simulation model. Examples include heat pumps, fans, storage tanks, or control valves. Each component has specific properties and parameters relevant to simulation, such as power consumption or temperature change.

```{figure} img/components_beispiel.png
---
name: components_beispiel
---
Components
```

<!-- TODO: Check completeness of components shown in this figure -->

---

## Geometrical Modeling

Geometrical elements are created using the Geometry Editor in SIMULTAN. For detailed guidance, consult the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki) or watch our [YouTube tutorial](https://www.youtube.com/watch?v=YDDNtA6lkFU&t=1s).

### IDA-ICE Specific Geometry Considerations

Since geometric modeling is central to SIMULTAN, several aspects are critical to ensure a consistent and stable data structure.

#### Assigning Components to Geometrical Surfaces

Each surface—walls, ceilings, and floors—must be explicitly assigned within the model.

```{figure} img/flächen_zuweisen.png
---
name: flächen_zuweisen
---
Assigned components
```

```{figure} img/zuordnugn_geometrie.png
---
name: zuordnung_geometrie
---
Data linked to a surface
```

In {numref}`flächen_zuweisen`, under `Components`, the selected surface is connected to **6-AW\_ZW**. Clicking the arrow on the right opens the corresponding component.

```{note}
At the bottom of {numref}`zuordnung_geometrie`, the connection to the **IDA-ICE Plugin** is indicated. More information is available in [Opaque Building Components](#opaque-building-components-key-parameter-and-layer-parameters).
```

<!-- TODO: Review this entire section for completeness and consistency -->

#### Assigning Volume to Rooms

The process is analogous to surface assignment, but applies to volumes.

```{figure} img/volumen_zuweisen.png
---
name: volumen_zuweisen
---
Connecting rooms with volumes
```

```{important}
The `4th - 7th buttons` from the left (yellow-grey cube icons) allow you to select:
- **Vertices**
- **Edges**
- **Faces**
- **Volumes**
```

---

## Modeling Guidelines

```{important}
Start with or import the provided template file `template_esbo_and_shades.simultan`, which contains all necessary structures for operating the IDA-ICE Plugin.
```

```{figure} img/geo_simultan.png
---
height: 350px
name: geo_simultan
---
Geometry of a *Tiny House* modeled in the SIMULTAN Geometry Editor.
```

In {numref}`geo_simultan`, a reference geometry (white) is used for the dynamic simulation. This may be an architectural model or a dedicated model for simulation purposes. This reference geometry is exported to IDA-ICE. Therefore, all geometry-dependent information must be linked to this model.

```{note}
The geometry file for IDA-ICE must be named **idaice_analysis.simgeo**.
```

---

## Setpoints

Setpoints are defined temperature thresholds used for heating and cooling control. Like rooms, setpoints are assigned to volumes and consist of two parameters: **heating** and **cooling**. These define the acceptable temperature range for each room. If the temperature deviates from this range, heating or cooling is triggered.

```{figure} img/setpoints.png
---
name: setpoints
---
Setpoints
```

```{figure} img/cooling_heating.png
---
name: cooling_heating
---
Heating and cooling parameters
```

---

### Propagation Settings

Propagation controls how values—such as heating and cooling setpoints—are transferred between components and geometry.

You can find the propagation settings under *Parameters > Propagation*.

```{figure} img/propagation.png
---
name: Propagation
---
Propagation buttons
```

The three options are:

* **Always propagate**: Prevents changes to setpoints in the geometry view. These values remain fixed.
* **Never propagate**: Allows manual overwriting of heating and cooling setpoints in the geometry view.
* **Propagate if instance**: Applies values only to instantiated components. *(Note: If unclear, clarify this setting's behavior.)*

```{figure} img/never_propagate.png
---
name: never_propagate
---
Never propagate
```

---

## Simulation Data

The simulation data is divided into two main phases:

1. **Warm-up Phase**
2. **Simulation Phase**

```{figure} img/Simulation_Data.png
---
name: simulation_data
---
Simulation Data
```

### Warm-up Phase

`The warm-up phase` is an initialization period at the beginning of the simulation. During this time, the building model adjusts its internal conditions – such as wall temperatures, indoor climate, and thermal mass – to reach a realistic thermal balance. The results from this phase are not included in the output statistics. Its sole purpose is to ensure that the main simulation (Simulation Phase) starts from physically meaningful and stable conditions.


### Simulation Phase

`The simulation phase` is the main calculation period during which all desired results of the building model are collected. This phase covers the predefined analysis period (e.g., one year) and computes operating states, room temperatures, energy consumption, and other relevant indicators. Only values determined during the simulation phase are used for analysis, statistics, and reporting. Thus, this phase provides the essential basis for evaluating the building and its systems.

---

## Final Steps

The plugin setup is now complete. You can proceed with exporting and executing simulations in IDA-ICE. Make sure all geometry and component assignments are consistent and that taxonomies are up to date.

```{note}
Refer to the respective documentation chapters for detailed guidance on:
- Building Envelope
- Transparent and Shading Elements
- HVAC Configuration via ESBO
- Internal Gains
- Material Properties
```

---

*This concludes the setup instructions for using the SIMULTAN plugin for IDA-ICE.*
