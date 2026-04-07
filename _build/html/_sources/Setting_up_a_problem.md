## Setting up a Problem

This chapter provides a brief overview of how data is structured within the underlying data model.

---

## Data Structure for the Plugin

In {numref}`ida_data`, a simplified illustration of the required data structure for running the plugin is shown. This structure holds all the necessary information to enable dynamic multizone climate and energy simulations in IDA-ICE.

```{figure} img/schematic_comp_ida.png
---
height: 500px
name: ida_data
---
Simplified representation of the required data structure to run the plugin.
```

A more in-depth description of the SIMULTAN data representation for building physics simulations can be found in the chapter [SIMULTAN Datastructure to incorporate the IDA-ICE Data model](SIMULTAN_Datastructure_to_incorporate_the_IDAICE_Data_model.md).

```{warning}
Although it is technically possible to define this structure manually, we strongly recommend using the provided templates and the user interfaces to avoid errors. Manual modeling is error-prone and can lead to time-consuming troubleshooting.
```


The data structure consists of two main elements:

1. [Taxonomies](#taxonomies)
2. [Components](#components)

---

### Taxonomies

Taxonomies are classification systems used to organize elements into hierarchical categories and subcategories. They help structure complex models and define relationships between entities.

```{note}
**Components that are not assigned to a taxonomy are ignored by the plugin.**
```

#### IDA-ICE Relevant Taxonomies

The IDA-ICE plugin introduces new taxonomies essential for establishing the connection between IDA-ICE and SIMULTAN {numref}`taxonomies_idaice`. Tools of the plugin's [user interface](Detailed_Modeling_Guide.md#modeling-for-ida-ice) automatically assign the appropriate taxonomy to each component for compatibility.

```{figure} img/taxonomies_idaice.png
---
name: taxonomies_idaice
---
Overview of IDA-ICE taxonomies
```

We recommend starting with one of the provided [template files](files/250512_cb_house_water_rad_modified_as.simultan) to ensure synchronization and reduce the risk of errors. To restore the complete taxonomy hierarchy required by the plugin, refer to the section on [Taxonomy Update](Detailed_Modeling_Guide.md#taxonomy-update).

---

### Components

The *ComponentBuilder* represent the functional building blocks of a simulation model as shown in {numref}`components_beispiel`. Examples include heat pumps, fans. Each component has specific properties and parameters relevant to simulation, such as power consumption.

```{figure} img/components_beispiel.png
---
name: components_beispiel
---
Some components of a data model
```

---

## Geometrical Modeling

Geometrical elements are created using the *GeometryViewer* in SIMULTAN. For detailed guidance, consult the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki) or watch our [YouTube tutorial](https://www.youtube.com/watch?v=YDDNtA6lkFU&t=1s).

### IDA-ICE Specific Geometry Considerations

Since geometric modeling is central to SIMULTAN, several aspects are critical to ensure a consistent and stable data structure.

#### Geolocation in the *SitePlanner* 

To access the ***SitePlanner*** in SIMULTAN open the corresponding `.spdxf` file (see {numref}`siteplanner`).
```{figure} img/siteplanner.png
---
name: siteplanner
---
Accessing the *SitePlanner* in SIMULTAN
```

##### Orientation within the *SitePlanner*

**Once opened, the *SitePlanner* displays a map-based environment for spatial orientation.**  

- In the top-left drop-down menu ({numref}`dropdown_siteplanner`), you can locate geometries from your data model.   
- Upon selection, the view automatically zooms to the selected geometry’s location. 

```{note}
The relative positioning of the geometries plays an important role when exporting to IDA-ICE. This positioning is transferred to the exported IDA-ICE model.
``` 

```{figure} img/dropdown_sitplanner.png
---
name: dropdown_siteplanner
---
Drop-down menu to locate geometries
```

```{tip}
In the *SitePlanner*, it is also possible to easily move selected geometries using the **G key**.
``` 

##### Control the positioning of geometries within the *GeometryViewer*

To manually define the placement of a geometry, open the *GeometryViewer*.
In the ribbon interface, click on *Geo-Reference Manager*. This opens a configuration tab where you can set the geometry's position by defining three reference nodes (see {numref}`georeferencemanager`).

```{figure} img/GeoReferenceManager.png
---
name: GeoReferenceManager
---
*Geo-Reference Manager* within the *GeometryViewer*
``` 

##### Adding Shading Elements for the IDA-ICE Simulation

```{tip}
To simulate shadows in IDA-ICE, create a new geometry and assign the **Shading** component to it (see {numref}`shadingsimulation`).
```

```{figure} img/shadingsimultations.png
---
name: shadingsimulation
---
Assigning a Shading component to a geometry
```

**Adding a new shading geometry to the *SitePlanner*:**

1. Open the *SitePlanner*
2. Drag and drop the new geometry into the map area
3. Move it to the desired position on the building using the mouse (left-click to place)


#### Assigning Components to Geometrical Surfaces

Each surface—walls, ceilings, and floors—must be explicitly assigned within the model.

```{figure} img/flächen_zuweisen.png
---
name: flächen_zuweisen
---
*GeometryViewer* view of components assigned to a surface
```

In {numref}`flächen_zuweisen`, under `Components`, the selected surface is connected to **6-AW\_ZW**. Clicking the arrow on the right opens the corresponding component within the *ComponentBuilder* {numref}`zuordnung_geometrie`.

```{figure} img/zuordnugn_geometrie.png
---
name: zuordnung_geometrie
---
Corresponding component with all its parameters within the *ComponentBuilder*
```

```{note}
At the bottom of {numref}`zuordnung_geometrie`, the connection to the **IDA-ICE Plugin** is indicated | Can be recognized by the assigned taxonomy *Constructional Element*. More information is available in [Opaque Building Components](#opaque-building-components-key-parameter-and-layer-parameters).
```

#### Assigning Volume to Rooms

The process is analogous to surface assignment, but applies to volumes {numref}`volumen_zuweisen`.

```{figure} img/volumen_zuweisen.png
---
name: volumen_zuweisen
---
Selected volume in the *GeometryViewer*
```

```{important}
The `4th - 7th buttons` from the left in {numref}`volumen_zuweisen` (yellow-grey cube icons) allow you to select:
- **Vertices**
- **Edges**
- **Faces**
- **Volumes**
```

---

## Modeling Guidelines

```{important}
Start with or import the provided template file [template_esbo_and_shades.simultan](files/template_esbo_and_shades.simultan), which contains all necessary structures for operating the IDA-ICE Plugin.
```

```{figure} img/geo_simultan.png
---
height: 350px
name: geo_simultan
---
Geometry of a *Tiny House* modeled in the SIMULTAN *GeometryViewer*.
```

In {numref}`geo_simultan`, a reference geometry (white) is used for the dynamic simulation. This may be an architectural model or a dedicated model for simulation purposes. This reference geometry is exported to IDA-ICE. Therefore, all geometry-dependent information must be linked to this model.

```{note}
The geometry file for IDA-ICE must be named **idaice_analysis.simgeo**.
```

---

## Room Unit Exports

**What is a Room Unit in IDA ICE?**   
A Room Unit in IDA ICE represents a single thermal zone whose indoor climate and energy performance are simulated. It is the core element for modeling room comfort, energy demand, and system operation. All relevant influences and technical systems affecting a room are brought together and calculated within the Room Unit.

**Typical Characteristics of a Room Unit:**
- **Geometry and Building Elements:**   
The Room Unit includes the room dimensions and all surfaces with their physical properties.
- **Usage:**   
User profiles, occupancy, internal loads (e.g., from equipment or lighting), and schedules are defined here.
- **Building Systems:**   
Central interface for heating, cooling, ventilation, shading, and control.
- **Controls:**   
Setpoints such as target temperature, CO₂ limits, or humidity levels are applied to the Room Unit.
- **Energy Flows:**   
The required energy for heating, cooling, and ventilation as well as internal gains and losses are calculated per Room Unit.
- **Comfort Evaluation:**   
Comfort indicators like overheating hours, temperature profiles, or air quality are evaluated for each Room Unit.

### Ideal Heating and Cooling

The Ideal Heater and Ideal Cooler are standard room units for simplified simulation of heating and cooling within a thermal zone. They provide or remove exactly the amount of heat needed to maintain the specified room temperature setpoints—regardless of the technical limitations or control losses typically present in real systems.

```{tip}
[Temperature setpoints](#setpoints): Define when heating or cooling is activated.
```

### SIMULTAN Relevant Knowledge

```{figure} img/Ideal_heating_cooling.png
---
name: ideal_heating_cooling
---
Parameters of ideal heating and ideal cooling subordinated to the *Building Services* component
```
Ideal Cooler and Heater can be found in SIMULTAN under *Building Services*. <!-- Satz abgeändert / verbessert-->

In {numref}`ideal_heating_cooling` you will see a yellow icon next to the names of the Ideal Cooler and Heater, which indicates that this component is connected to a geometry. Connecting the component to a volume is essential for exporting to IDA-ICE.

<!-- ergänzung folgt... | Gelbes Icon bei Never Propagate und Instanzen im GeometryViewer-->

### Water Radiator

After using the Ideal Heater/Cooler for simplified, direct room temperature control, the Water Radiator adds realism by simulating an actual hydronic radiator with water flow, heat transfer limits, and response delays. Unlike the Ideal Heater, the Water Radiator tries to reflect physical system constraints and integrates with real heating circuits, making it essential for detailed, system-based simulations.

```{figure} img/water_radiator.png
---
name: water_radiator
---
List of parameters for the detailed and simple water radiator
```

The water radiator behaves in the same way as an ideal heater/cooler. Therefore, it must be assigned to a volume/zone! You find it under *Building Services* {numref}`water_radiator`.

---

### Setpoints

Setpoints are defined temperature thresholds used for heating and cooling control. Like rooms, setpoints are assigned to volumes ({numref}`setpoints`) and consist of two parameters: heating and cooling ({numref}`cooling_heating`). These define the acceptable temperature range for each room. If the temperature deviates from this range, heating or cooling is triggered. In {numref}`Setpoints_geometrie_view` the setpoint is assigned to a volume.

```{warning}
**Setpoints must always be assigned to a volume!**
``` 

```{figure} img/setpoints.png
---
name: setpoints
---
Example in which setpoints, water radiator, and a room are assigned to the same volume
```

```{figure} img/cooling_heating.png
---
name: cooling_heating
---
Setpoint component with his parameters heating and cooling
```

```{figure} img/Setpoints_geometrie_view.png
---
name: Setpoints_geometrie_view
---
Setpoint adjustments to instances in the GeometryViewer
```
<!-- neues bild zu Setpoints im GeometrieViewer-->

---

### Propagation Settings

Propagation controls how values—such as heating and cooling setpoints—are transferred between components and geometry.

**You can find the propagation settings under *Parameters > Propagation*.** {numref}`propagation`

```{figure} img/propagation.png
---
name: Propagation
---
Propagation buttons within the *Property Editor*
```

The three options are:

* **Always propagate**: Prevents changes to setpoints in the *GeometryViewer*. These values remain fixed.
* **Never propagate**: Allows manual overwriting of heating and cooling setpoints in the GeometryViewer. {numref}`never_propagate`
* **Propagate if instance**: <!-- konnte keinen unterschied zu Always propagate finden, auch nicht den sinn des overwrite buttons!-->

```{figure} img/never_propagate.png
---
name: never_propagate
---
Showcase of how never propagate influences the settings of the *GeometryViewer*
```

---

## Simulation Data

{numref}`simulation_data` The simulation data is divided into two main phases:

1. **Warm-up Phase**
2. **Simulation Phase**

```{figure} img/Simulation_Data.png
---
name: simulation_data
---
Simulation Data with its subcomponents Simulation Phase and Warmup Phase and their parameters
```

### Warm-up Phase

`Warm-up phase` is an initialization period at the beginning of the simulation. During this time, the building model adjusts its internal conditions – such as wall temperatures, indoor climate, and thermal mass – to reach a realistic thermal balance. The results from this phase are not included in the output statistics. Its sole purpose is to ensure that the main simulation (Simulation Phase) starts from physically meaningful and stable conditions.


### Simulation Phase

`Simulation phase` is the main calculation period during which all desired results of the building model are collected. This phase covers the predefined analysis period (e.g., one year) and computes operating states, room temperatures, energy consumption, and other relevant indicators. Only values determined during the simulation phase are used for analysis, statistics, and reporting. Thus, this phase provides the essential basis for evaluating the building and its systems.

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
