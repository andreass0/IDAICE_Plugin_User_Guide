# Setting up a problem

A short overview of the representation of the data in the data model will be given in the beginning.

---

<!-- Taxonomien einfügen, Taxonomien sind einzigartige Schlüssel, SImultan arbeitet im Hintergrund anssschließlich über die Keys, abhängigkeiten | Plugin erwartet bei bestimmt zugewiesenen TExonomien bestimmte WErte usw. VIdeo 00:02:02-->

## Datastructure for the plugin

In {numref}`ida_data` a simplified depiction of the needed datastructure to run the plugin is given. This data structure
holds all the necessary information to enable simplified dynamic multizone climate and energy simulations in IDA-ICE

```{figure} img/schematic_comp_ida.jpg
---
height: 500px
name: ida_data
---
Simplified depiction of the needed datastructure to run the plugin is given.
```

A more in depth look into the SIMULTAN representation of the data for building physics simulations is given in the
chapter [SIMULTAN Datastructure to incorporate the IDA-ICE Data model](SIMULTAN_Datastructure_to_incorporate_the_IDAICE_Data_model.md)
.

```{warning}
Although this data structure can be implemented manually, it is strongly recommended to use the provided templates and export them to 
existing models or adjust them as needed. Manuel modelling is always prone to errors and could result in very time
consuming efforts when trying to fix those.
```
<!-- Link zu Templates fehlt -->

---

## Geometrical modelling

The geometry is created in the Geometry Editor of the SIMULTAN Editor. Please consult
the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki)
for further information on how to use this Geometry Editor. Or watch our [Videos on YouTube](https://www.youtube.com/watch?v=YDDNtA6lkFU&t=1s). <!-- Neu -->

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

## User Interface <!-- Neuer Sektor | Reihenfolge mit oberigen Kapitel vllt tauschen -->

The IDA-ICE-Plugin comes with a user interface {numref}`UserInterface_example` to help with the creation of the needed data structure for the plugin. The user interface is very user-friendly and ensures that you keep an overview and do not make any unnecessary mistakes by navigating manually. <!-- Formulierung nochmal überarbeiten!!-->

```{figure} img/position-construction.png
---
name: position-construction
---
Possibilities with the IDA-ICE plugin
```

```{warning}
It is very important to work carefully in the user interface, because changes are applied directly, even without explicitly saving or simply closing the user interface.
```

<!-- Wortwahl: "Method"-->
<!-- noch klären wie es wirklich intern in ida-ice vorgeht und werter bearbeitet, ... -->
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
- **Transparent building components:**
    - Window
    - Door
- **Shading building components**

---

#### Opaque building components: Key parameter and layer parameters

in the example you can see the data structure for a **GROUND-SLAB**. The procedure is analogues for the other opaque building components.

To export Opaque building components using the IDA-ICE user interface, please follow these instructions:

- Open the `construction` tab in Simultan <!-- Kontrollieren -->
- The `construction` tab with all its functions <!-- Vllt bisschen kleiner -->

```{figure} img/overview-constructiontab.png
---
name: overview-constructiontab
---
Brief overview of the functions of the construction tab
```

```{note}
To create a new construction, press the NEW button, then simply assign the following parameters to your preferences. The parameters are explained in more detail below.

This is how quickly it is possible to create new constructions with the IDA-ICE user interface!
```

1. **`Select construction:`**  
Provides an overview of all objects that are already connected to IDA-ICE Surface Types. It gives you a good overview and lets you edit all the surfaces connected to the IDA-ICE-Plugin with just a few clicks. <!-- Ausdruck! -->
2. **`Edit construction:`**   
This is where the important information for the export to IDA-ICE is added. <!-- Auschmücken und Unterpunkte näher erklären! -->  


2.1 **Consturction Name**  
2.2 **Surface Type:** [opaque building components](#opaque-building-components-key-parameter-and-layer-parameters)  
2.3 **Layers:**  
Shows the structure of the selected construction and the different materials it is made of. You can switch between materials for further information. These are displayed in the three parameters **layer name**, **material** and **thickness**.

- Layer Name: Shows the name of your choosen Layer. <!-- Kontrollieren ob es wirklich nur diese Funktion hat! -->
- Material: Shows the material of your choosen Layer, [**Materials**](#materials) 
- Thickness: Shows the Thickness (m) of your choosen Layer

All changes have a direct impact on the data model. This makes it possible to make changes quickly and effectively without losing the overview! <!-- Probieren ob automatisch jede komponente in der geometrie einem IDA-ICE surface type zugewissen wird, bzw. ob auch objekte ohne zuweisung im User Interface angezeigt werden-->

---

#### Transparent building components: Key parameter and layer parameters

The datastructure to export transparent building components will be shown for a Fenster (window). The procedure is analogues for a
door and other `glass constructions`. <!-- -->

```{figure} img/TransperentBuildingComponents-UI.png
---
name: TransperentBuildingComponents-UI
---
Example of the data structure for a window
```

The “Glass Constructions definitions” tab is pretty much identical in structure to [“Constructions definitions”](#opaque-building-components-key-parameter-and-layer-parameters). The only difference is in the parameters.

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

As you can see, we have decided to use the same structure throughout the Plugin. So that users can find their way around as quickly as possible and concentrate on the essentials.

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
<!-- überlegen rauszulöschen, unnötige information, nicht auf das wesentliche konzentriet-->

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
<!-- nicht sicher ob es auch beim User Interface noch passend ist-->
<!-- am ende noch bisschen text eventuelle noch bisschen informationen über HVAC SYstem / Esbo-Plant in IDA ICE allgemein-->

### Materials
<!-- anordnung der Überschirft klären!!-->

`Materials` have been given their own area in the **IDA-ICE-Plugin**. This once again allows users to keep their materials organized and to proceed in a structured manner.

```{figure} img/materials_UI.png
---
name: materials_UI
---
User Interface for materials
```

As you can see, we have also used a simple layout here to maximize user-friendliness. In **the materials definitions section**, you can **delete** materials, **copy** materials to customize them and **create completely new materials**. To do the latter, fill in the parameters using the description below.

1. **Name:**  
Any name to name the material.
2. **Thermal Conductivity:**  
Indicates how well the material conducts heat.  
Value 0: This means that the material does not conduct any heat at all - it acts as perfect insulation (which does not occur in reality).
3. **Density:**  
Indicates how much mass one cubic meter of the material has.
4. **Specific Heat:**  
Indicates how much energy (in joules) is required to heat 1 kg of material by 1 Kelvin.

```{note}
These parameters are essential for thermal simulation in IDA ICE. They determine how the material as part of a component (e.g. wall, floor) conducts and stores heat.
```

The newly created material is then displayed directly in the construction tab under **material**. This means that materials only have to be created once and can then be universally linked to the various components.

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
<!-- Herrausfinden ob diese Kapitel noch notwendig sind!!!-->
<!-- SyncImport und Taxonomie Update nicht hinzugefügt, keine Information darüber, wenn es hinzugefügt wird dann in Results_of_the_simulation.md-->
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
