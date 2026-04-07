# Setting up a problem

A short overview of the representation of the data in the data model will be given in the beginning.

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

## Geometrical modelling

The geometry is created in the Geometry Editor of the SIMULTAN Editor. Please consult
the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki)
for further information on how to use this Geometry Editor.

### Modelling guidelines

```{important}
Either import or start with the provided template file `template_esbo_and_shades.simultan`. All the necessary datastructure to operate the
IDA-ICE-plugin will be provided there.
```

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
The geometry file for the IDA-ICE analysis has to be called idaice_analysis.simgeo.
```

## Components used for the building physics simulation

### Building Envelope

Since most of the data of the building envelope will already be provided with an architectual model the structure of the
plugin focuses on expanding the already existing information, so it is containing all the calculation relevant
information and can be exported to IDA-ICE.

In the following the key-parameters and the structure of the components to export them are addressed. In regard of the
building envelope IDA-ICE is differentiating between the following main categories:

- **Opaque building components:**
    - External wall
    - Internal Wall
    - External Slab
    - Internal Slab
    - Roof
- **Transparent building components:**
    - Window
    - Door
- **Shading building components**

#### Opaque building components: Key parameter and layer parameters

The data structure for building components to be exported with the plugin will be explained for an external wall. The
procedure is analogues for the other opaque building components.

To export the external walls of your datamodel please follow these instructions:

- Add a new parameter named `IDA-ICE_surface_types` on the top level of your building component
- Write `EXTERNAL-WALL` as a text into the newly added parameter.

```{figure} img/ext_wall_para.png
---
height: 350px
name: ext_wall_para
---
External Wall parameter for export with the plugin.
```

The plugin recognizes this component now as an external wall for IDA-ICE to be exported by the plugin. The layers have
to be model as sub components and should contain the following parameters:

```{figure} img/layer_para.png
---
height: 500px
name: layer_para
---
Needed Layer parameters of the building component for the simulation.
```

```{note}
Key parameter for other opaque building components:
- `INTERNAL-WALL`
- `EXTERNAL-SLAB`
- `INTERNAL-SLAB`
- `ROOF`
```

#### Transparent building components: Key parameter and layer parameters

The datastructure to export transparent building components will be shown for a window. The procedure is analogues for a
door.

To export the external walls of your datamodel please follow these instructions:

- Add a new parameter named `IDA-ICE_surface_types` to your window component.
- Write `GLASS_CONSTRUCTION` as a text into the newly added parameter.

The needed parameters to enable the export and simulation with the plugin can be seen in {numref}`window_para`.

```{figure} img/window_para.png
---
height: 700px
name: window_para
---
Needed parameters of the window component for the simulation.
```

#### Shading building components: Key parameter and layer parameters

To export the shading components of your datamodel please follow these instructions:

- Add a new parameter named `IDA-ICE_surface_types` to your shading component.
- Write `SHADE` as a text into the newly added parameter.

The needed parameters to enable the export and simulation with the plugin can be seen in {numref}`shade_para`.

```{figure} img/shade_para.png
---
height: 250px
name: shade_para
---
Needed parameters of the shading component for the simulation.
```

### HVAC-System

The HVAC-System is implemented via the ESBO-Plant of IDA-ICE. {numref}`esbo_simultan` shows all the possible inputs
which are exported with the plugin.

```{figure} img/esbo_simultan.png
---
height: 350px
name: esbo_simultan
---
SIMULTAN components for the different ESBO-Plant components.
```

These components confine the defining parameters for the different HVAC-components. {numref}`ambient_air_to_brine_para`
to {numref}`liquid_circuit` show the different parameters which have to be incorporated in the data model to export the
different modules of the ESBO-Plant successfully.

```{tip}
Use the template which holds all the possible ESBO-Plant inputs and delete what you don't need. Refrain from manual 
modelling as much as possible.
```

```{figure} img/ambient_air_to_brine_para.png
---
height: 250px
name: ambient_air_to_brine_para
---
SIMULTAN components with the underlying defining parameters for the different ESBO-Plant components.
```

```{figure} img/ambient_air_to_water_para.png
---
height: 250px
name: ambient_air_to_water_para
---
SIMULTAN components with the underlying defining parameters for the different ESBO-Plant components.
```

```{figure} img/generic_cold_water.png
---
height: 350px
name: generic_cold_water
---
SIMULTAN components with the underlying defining parameters for the different ESBO-Plant components.
```

```{figure} img/generic_photo.png
---
height: 350px
name: generic_photo
---
SIMULTAN components with the underlying defining parameters for the different ESBO-Plant components.
```

```{figure} img/generic_topup.png
---
height: 300px
name: generic_topup
---
SIMULTAN components with the underlying defining parameters for the different ESBO-Plant components.
```

```{figure} img/liquid_circuit.png
---
height: 200px
name: liquid_circuit
---
SIMULTAN components with the underlying defining parameters for the different ESBO-Plant components.
```

```{note}
If you are exporting redundant HVAC-Systems or HVAC-Systems which are in conflict with each other for the 
dynamic simulation IDA-ICE will show an error message.
```

### Internal Gains

The modelling of internal gains due to occupant behaviour is also possible. The SIMULTAN representation is stored under
the component `Nutzung`. This component stores sub-components for each simulation-zone and the assigned internal gains.

```{figure} img/inernal_gains_comp.png
---
height: 400px
name: inernal_gains_comp
---
SIMULTAN components with the underlying defining parameters for the different ESBO-Plant components.
```

The sub-components consist of `Equipment`, `Light`, `Occupants` each with the needed parameters to describe the needed
information for the simulation.

**Equipment**

```{figure} img/equipment_para.png
---
height: 300px
name: equipment_para
---
SIMULTAN component for the description of internal gains by equipments with the underlying defining parameters.
```

**Light**

```{figure} img/light_para.png
---
height: 200px
name: equipment_para
---
SIMULTAN component for the description of internal gains by light with the underlying defining parameters.
```

**Occupants**

```{figure} img/occupant_para.png
---
height: 200px
name: equipment_para
---
SIMULTAN component for the description of internal gains by occupants with the underlying defining parameters.
```

## Connecting components with the geometry

The before created components are a representation of the information needed for the dynamic simulation. Connect the
components to the geometry as needed. Please consult
the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki)
for general information on how to link components and geometrical information.
