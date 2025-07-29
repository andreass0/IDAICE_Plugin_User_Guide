# Setting up a problem

This chapter provides a brief overview of how data is structured within the underlying data model.

---

## Datastructure for the plugin

In {numref}`ida_data` a simplified depiction of the needed datastructure to run the plugin is given. This data structure
holds all the necessary information to enable simplified dynamic multizone climate and energy simulations in IDA-ICE

```{figure} img/schematic_comp_ida.jpg
---
height: 500px
name: ida_data
---
A simplified illustration of the required data structure for running the plugin.
```

A more in depth look into the SIMULTAN representation of the data for building physics simulations is given in the
chapter [SIMULTAN Datastructure to incorporate the IDA-ICE Data model](SIMULTAN_Datastructure_to_incorporate_the_IDAICE_Data_model.md)
.

```{warning}
Although this data structure can be implemented manually, it is strongly recommended to use the provided templates either by exporting them into existing models or adapting them as required. Manuel modelling is always prone to errors and could result in very time
consuming efforts when trying to fix those.
```
<!-- Link zu Templates fehlt -->

**The data structure can be divided into two parts:**
1. [taxonomies](#taxonomies)
2. [components](#components)

---

### Taxonomies

Taxonomies are classification systems used to categorize objects, terms or information into hierarchical groups and subgroups. They are used to structure complex issues and present them clearly. A taxonomy defines the criteria for classification and the relationships between the individual categories.

```{note}
Components without an assigned taxonomy are irrelevant for the data model and are ignored by SIMULTAN.
```

---

#### IDA-ICE relevant taxonomies

Together with the IDA-ICE plugin, new taxonomies are also coming which are essential to establish a connection between IDA-ICE and SIMULTAN. The [User Interface](#modeling-for-ida-ice) of the IDA-ICE Plugin **automatically** assigns the correct taxonomy to make the data model ready for export to IDA-ICE.

```{figure} img/taxonomies_idaice.png
---
name: taxonomies_idaice
---
Overview IDA-ICE taxonomies
```

We recommend that you start with one of our `template files`, which ensures an error-free, synchronized simulation to get used to the plugin.   
To restore the full `taxonomy hierarchy` which is necessary for the **IDA-ICE plugin**, the plugin offers a [solution](#taxonomy-update).
<!-- vorlage verlinken!-->

---

### Components

Components represent the functional building blocks of a simulation model—such as heat pumps, fans, storage tanks, or control valves. They have physical properties and parameters that are used in calculations — for example, power consumption or temperature change. Components can be configured and connected to realistically represent technical systems within a building.

```{figure} img/components_beispiel.png
---
name: components_beispiel
---
Components
```

---

## Geometrical modelling

The geometry is created in the Geometry Editor of the SIMULTAN Editor. Please consult
the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki)
for further information on how to use this Geometry Editor. Or watch our [Videos on YouTube](https://www.youtube.com/watch?v=YDDNtA6lkFU&t=1s). 

---

### Related to IDA-ICE

Geometric modeling is a core aspect of SIMULTAN, so a few important things need to be taken into account here. So that a stable data structure can be created.


---

#### Assign components to the correct areas

The basis of every SIMULTAN file is the assignment of geometries. This means that all surfaces—including walls, ceilings, and floors—must be explicitly assigned. As you can see in the following pictures {numref}`flächen_zuweisen` and {numref}`zuordnung_geometrie`!

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
Data which is connected with the surface
```

In {numref}`flächen_zuweisen` under  `Components` you can see that the selected surface is connected to **6-AW_ZW**. For further Information press the arrow on the right. Once you've done that you end up in the component area where this area is noted.

```{note}
On the buttom of {numref}`zuordnung_geometrie` you can see how this surface gets connected to the **IDA-ICE-Plugin**. More on this later in the chapter [opaque building components](#opaque-building-components-key-parameter-and-layer-parameters)
```

---

#### Assign volume to rooms

... this works in the same way as assigning components to the correct surfaces. The only difference is that it now works with volumes instead of surfaces.

```{figure} img/volumen_zuweisen.png
---
name: volumen_zuweisen
---
Connecting rooms with volumes
```
```{important}
The `4th - 7th button` from the left (yellow gray cube icons) are used to select the different components.   
- **Vertices**   
- **Edges**   
- **Faces**   
- **Volumes**
```


---

### Modelling guidelines

```{important}
Either import or start with the provided template file `template_esbo_and_shades.simultan`. All the necessary datastructure to operate the
IDA-ICE-plugin will be provided there.
```
<!-- Direkten Link einfügen -->

In {numref}`geo_simultan` it can be seen that the plugin uses a reference geometry (white) for the dynamic simulation.
The reference geometry, representing the outer building envelope, can for example be an architectural model or a
designated model used for the building physics simulations.

```{figure} img/geo_simultan.png
---
height: 350px
name: geo_simultan
---
Example of the geometry of a *Tiny House* modelled with the Geometry Editor of the SIMULTAN Editor.
```

For the simulation the reference geometry is exported to IDA-ICE, therefore all of the geometry dependant information
needed for the simulation has to be linked to this model.

```{note}
The geometry file for the IDA-ICE analysis has to be called **idaice_analysis.simgeo**.
```

---

## Setpoints

Just like rooms, `setpoints` are also assigned volumes. Setpoints consist of two parameters, **heating** and **cooling**. Setpoints can be used to define set values for heating and cooling. Setpoints define the limit temperatures within a room. If the temperature falls above or below this range, the room temperature must be adjusted.    Each individual room can have its own **heating** and **cooling** setpoints.

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

### Propagation

Within the property manager under Parameters there is the Propagation area. This includes 3 buttons with different functions. As you can see in {numref}`Propagation`
- Always propagate
- Propagate if instance
- Never propagate   

```{figure} img/propagation.png
---
name: Propagation
---
Propagation buttons
```

---

#### Never propagate

The `Never propagate` button ensures that the `setpoints for heating and cooling` of each room can be overwritten in the geometry view.

```{figure} img/never_propagate.png
---
name: never_propagate
---
Never propagate
```

---

#### Always propagate

If you press the `Always propagate` button in the component area, the overwriting of the **basic heating and cooling values** in the geometry view is blocked. And the cell is grayed out for visibility.

---

#### Propagate if instance


---

### Simultation Data

The simulation data is divided into two distinct phases:
- **Warm-up Phase**   
- **Simulation Phase**

These two areas contain important parameters for the IDA-ICE simulation.

```{figure} img/Simulation_Data.png
---
name: simulation_data
---
Simulation Data
```

---

#### Warm-up Phase

`The warm-up phase` is an **initialization period** at the beginning of the simulation. During this time, the building model adjusts its internal conditions – such as wall temperatures, indoor climate, and thermal mass – **to reach a realistic thermal balance.** The results from this phase are **not** included in the output statistics. Its sole purpose is to ensure that the main simulation (Simulation Phase) starts from **physically meaningful** and **stable conditions**.

---

#### Simulation Phase

`The simulation phase` is the **main calculation period** during which all desired results of the building model are collected. This phase covers the predefined analysis period (e.g., one year) and computes operating states, room temperatures, energy consumption, and other relevant indicators. **Only values determined during the simulation phase are used for analysis, statistics, and reporting.** Thus, this phase provides the essential basis for evaluating the building and its systems.

---

## Modeling for IDA-ICE

The IDA-ICE plugin includes a user interface designed to assist users in building the necessary data structure efficiently. The user interface is very user-friendly and ensures that you keep an overview and do not make any unnecessary mistakes by navigating manually. 

```{figure} img/position-construction.png
---
name: position-construction
---
Possibilities with the IDA-ICE plugin
```

```{warning}
It is very important to work carefully in the user interface, because changes are applied directly, even without explicitly saving or simply closing the user interface.
```

---

### Building Envelope

Since most of the data of the building envelope will already be provided with an architectual model the structure of the
plugin focuses on expanding the already existing information, so it is containing all the calculation relevant
information and can be exported to IDA-ICE.

In the following the key-parameters and the structure of the components to export them are addressed. In regard of the
building envelope IDA-ICE is differentiating between the following main categories:

- **Opaque building components**
    ```{figure} img/Opaque-building-components.png
    ---
    height: 225px
    align: center
    name: fig-Opaque-building-components
    ---
    Overview of all Opaque building components
    ``` 

---

#### Opaque building components: Key parameter and layer parameters

in the example you can see the data structure for a **GROUND-SLAB**. The procedure is analogues for the other opaque building components.

To export Opaque building components using the IDA-ICE user interface, please follow these instructions:

- Open the `construction` tab in Simultan 
- The `construction` tab with all its functions 

```{figure} img/overview-constructiontab.png
---
name: overview-constructiontab
---
Brief overview of the functions of the construction tab
```

1. **`Select construction:`**  
Provides an overview of all objects that are already connected to IDA-ICE Surface Types. It gives you a good overview and lets you edit all the surfaces connected to the IDA-ICE-Plugin with just a few clicks. <!-- Ausdruck! -->
2. **`Edit construction:`**   
This is where the important information for the export to IDA-ICE is added. 


2.1 **Construction Name**  
2.2 **Surface Type:** [opaque building components](#opaque-building-components-key-parameter-and-layer-parameters)  
2.3 **Layers:**  
Shows the structure of the selected construction and the different materials it is made of. You can switch between materials for further information. These are displayed in the three parameters **layer name**, **material** and **thickness**.

- Layer Name: Shows the name of your choosen layer. 
- Material: Shows the material of your choosen layer, [**Materials**](#material-properties) 
- Thickness: Shows the Thickness (m) of your choosen layer

All changes have a direct impact on the data model. This makes it possible to make changes quickly and effectively without losing the overview! 

---

#### Transparent building components: Key parameter and layer parameters

The datastructure to export transparent constructions will be shown for a Fenster (window). The procedure is analogues for a
door and other `glass constructions`.

```{figure} img/TransperentBuildingComponents-UI.png
---
name: TransperentBuildingComponents-UI
---
Example of the data structure for a window
```

The “Glass Constructions definitions” tab is pretty much identical in structure to [“Constructions definitions”](#opaque-building-components-key-parameter-and-layer-parameters). The only difference is in the parameters. <!-- Rausgenommen / überflüssig-->

The parameters in the image relate to the material properties of transparent components (such as windows) in the IDA ICE building simulation software. These values strongly influence the thermal and solar behavior of the glazing. Here is an explanation of the terms and their meaning.  

1. **Name:**  
Any name to name the glass constructions.  
2. **Solar Heat Gain Coeff(g)**  
Proportion of solar radiation that enters the building through the window (direct + secondary through heating of the glass).
3. **Solar Transmittance(T)**  
Proportion of directly transmitted solar radiation (without secondary heat conduction).  
4. **Visible Transmittance(Tvis):**  
Proportion of visible light that passes through the glazing.  
5. **Thermal Conductivity(U):**  
Heat transfer coefficient - how well the window conducts heat.  
6. **Internal Emissivity:**  
Radiant heat emission from the inner surface (e.g. glass) to the inside.  
7. **External Emissivity:**
The opposite of 6. so for the outside of the window  


```{note}
These values are used in IDA ICE to:

- Calculate heat loss in winter and heat input in summer
- simulate the daylight input, risk of overheating and the energy requirement for heating/cooling
- find optimal window configurations in terms of energy efficiency
```

***


#### Shading building components: Key parameter and layer parameters

A central element in IDA-ICE is the consideration of shading, as it has a considerable influence on daylight, cooling and heating loads and the indoor climate. This is why the plugin has a separate area for this, as you can see in {numref}`Shades-UI`.

```{figure} img/Shades-UI.png
---
name: Shades-UI
---
User Interface Shading Surface definitions
```

The individual parameters relate to the surface properties of a material or surface in IDA ICE. They influence thermal radiation, light reflection and the transmission of daylight and energy. Here is a detailed explanation of the individual parameters:

1. **Name:**  
Any name to name the shading.  
2. **Longwave Emissivity:**  
Indicates how strongly a surface can emit long-wave heat radiation (infrared).  
3. **Shortwave Reflectance:**  
Proportion of short-wave sunlight reflected by the surface (in %).  
4. **Roughness:**  
Beschreibt, wie rau eine Oberfläche ist, was sich auf die Streuung von Licht auswirkt.  
5.  **Specularity:**  
How strongly a surface reflects (directionally).  
6.  **Transparency:**  
How much visible light is transmitted through the surface.  

The needed parameters to enable the export and simulation with the plugin can be seen in {numref}`shade_para`.

The parameters for the shadings change for each material. This is precisely why this user interface is so important. In IDA-ICE, a distinction is made not only between materials but also between shading types. Here is the most important thing you need to know about them:

---

| Shading Type                   | Description                                                          | Typical Parameter Variability                                   |
|-------------------------------|----------------------------------------------------------------------|------------------------------------------------------------------|
| Fixed Shading                  | Overhangs, balconies, louvers – permanently attached to the facade   | Material (e.g., concrete, metal, wood), size, transparency (e.g., perforated panels) |
| Horizontal Shading             | Horizontal louvers, awnings                                          | Material, spacing, angle, transparency                           |
| Vertical Shading               | Side fins, vertical louvers                                          | Material, height, spacing, transparency                          |
| Context/Environmental Shading  | Neighboring buildings, trees, walls                                  | Shape, size, material (e.g., tree crowns as partially transparent) |
| Window-Integrated Shading      | Blinds, roller shades, venetian blinds mounted on the window         | Material, opening degree, control (fixed/variable), transparency |
<!-- vllt. rauszulöschen, irrelevante information-->

---

### HVAC-System

The HVAC-System is implemented via the ESBO-Plant of IDA-ICE. {numref}`esbo_simultan` shows all the possible inputs
which are exported with the plugin.

```{figure} img/Esbo-UI.png
---
name: esbo_simultan
---
SIMULTAN components for the different ESBO-Plant components.
```

The **Edit Component** area contains the defining parameters for the various HVAC components. These differ completely between the individual components.

```{tip}
All components can be easily switched off in the user interface. This separates all data connected to the component. As you can see in the screenshot. 
```

```{figure} img/ESBOplant-UI.png
---
name: esbo_off
---
A switched off component
```

Like all other functions in the IDA-ICE-Plugin, changes in the user interface have a direct effect on the data structure. As a result, these functions are powerful and should be used with caution. In the following scrennshots {numref}`system-on` and {numref}`system_off` I have shown the effects on Building Services when an **HVAC-System** is switched off in **ESBO-plant**.
<!-- Rausgenommen / überflüssig-->


```{figure} img/esbo-on.png
---
name: system-on
---
HVAC-System turned on
```

```{figure} img/esbo_off.png
---
name: system_off
---
HVAC-System turned off
```


```{warning}
If you are exporting redundant HVAC-Systems or HVAC-Systems which are in conflict with each other for the 
dynamic simulation IDA-ICE will show an error message.
```


### Materials


`Materials` have been given their own area in the **IDA-ICE-Plugin**. This once again allows users to keep their materials organized and to proceed in a structured manner.

```{figure} img/materials_UI.png
---
name: materials_UI
---
User Interface for materials
```

The layout was deliberately kept simple to ensure high usability and intuitive navigation. In **the materials definitions section**, you can **delete** materials, **copy** materials to customize them and **create completely new materials**. To do the latter, fill in the parameters using the description below. <!-- überflüssig / rausgenommen-->

1. **Name:**  
2. **Thermal Conductivity:**  
Indicates how well the material conducts heat.  
Value 0: This means that the material does not conduct any heat at all - it acts as perfect insulation.
3. **Density:**  
Indicates how much mass one cubic meter of the material has.
4. **Specific Heat:**  
Indicates how much energy (in joules) is required to heat 1 kg of material by 1 Kelvin.

```{note}
These parameters are essential for thermal simulation in IDA ICE. They determine how the material as part of a component (e.g. wall, floor) conducts and stores heat.
```

The newly created material is then displayed directly in the construction tab under **material**. This means that materials only have to be created once and can then be universally linked to the various components.

---

### Taxonomy Update

```{figure} img/taxonomyupdate_button.png
---
name: taxonomyupdate_button
---
Button to Update IDA-ICE taxonomies
```

As already mentioned in [Taxonomies](#taxonomies), taxonomies are one of the basic building blocks of SIMULTAN. That's why the plugin has its own button to update taxonomies.

`If you press the button:`

**All taxonomies of the IDA-ICE plugin are restored or updated to the latest version.**

```{warning}
It does not automatically assign the correct taxonomy to the components again! (if taxonomies were deleted which were linked to components)
```

---

### Internal Gains

The modelling of internal gains due to occupant behaviour is also possible. The SIMULTAN representation is stored under
the component `Nutzung`. This component stores sub-components for each simulation-zone and the assigned internal gains.

```{figure} img/inernal_gains_comp.png
---
name: inernal_gains_comp
---
SIMULTAN components with the underlying defining parameters for the different ESBO-Plant components.
```

The sub-components consist of `Equipment`, `Light`, `Occupants` each with the needed parameters to describe the needed
information for the simulation.

**Equipment**

```{figure} img/equipment_para.png
---
name: equipment_para
---
SIMULTAN component for the description of internal gains by equipments with the underlying defining parameters.
```

**Light**

```{figure} img/light_para.png
---
name: equipment_para
---
SIMULTAN component for the description of internal gains by light with the underlying defining parameters.
```

**Occupants**

```{figure} img/occupant_para.png
---
name: equipment_para
---
SIMULTAN component for the description of internal gains by occupants with the underlying defining parameters.
```

## Connecting components with the geometry

The before created components are a representation of the information needed for the dynamic simulation. Connect the
components to the geometry as needed. Please consult
the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki)
for general information on how to link components and geometrical information.
