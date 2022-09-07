# Setting up a problem

A short overview of the representation of the data in the data model will be given in the beginning. After that the
tutorial focuses on modelling with the implemented user interface of the plugin.

## Structural analysis component

In {numref}`struct_comp` a simplified depiction of the structural analysis component is given. This component is used in
the SIMULTAN datamodel to store the information needed to export data with the RFEM Plugin to enable structural analysis
simulations in RFEM 6.

```{figure} img/struct_component.jpg
---
height: 250px
name: struct_comp
---
Simplified depiction of the representation of the structural analysis component.
```

A more in depth look into the SIMULTAN representation of the structural analysis data is given in the
chapter [SIMULTAN Datastructure to incorporate the RFEM Data model](SIMULTAN_Datastructure_to_incorporate_the_IDAICE_Data_model.md)
.

```{warning}
Although this data structure can be implemented manually, it is strongly recommended to use the user interface that
comes with the plugin for modelling. Manuel modelling is always prone to errors and could result in very time
consuming efforts when trying to fix those.
```

## Geometrical modelling

The geometry is created in the Geometry Editor of the SIMULTAN Editor. Please consult
the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki)
for further information on how to use this Geometry Editor.

### Modelling guidelines

```{important}
Either import or start with the provided template file `_temp.simultan`. All the necessary datastructure to operate the
RFEM-plugin will be provided there. The simgeo file has to be called struct_analysis.simgeo. Do not manipulate the 
`Structural Analysis Component`!
```

In {numref}`simultan_geometry` it can be seen that the plugin uses a reference geometry (white) as well as a geometry
for the structural analysis (red). The reference geometry, representing the outer building envelope, can for example be
an architectural model or the model used for the building physics simulations.

```{figure} img/simultan_geometry.png
---
height: 350px
name: simultan_geometry
---
Example of the geometry of a *Tiny House* modelled with the Geometry Editor of the SIMULTAN Editor.
```

For the simulation the structural geometry is exported to RFEM, therefore all of the information exclusively used for
structural analysis will be linked to this geometry.

```{note}
If you are only concerned with structural analysis it is enough to have all the necessary information in the 
struct_analysis.simgeo file.
```

## User Interface

The RFEM-Plugin comes with a user interface {numref}`ui_plugin` to help with the creation of the needed data structure
for the plugin. The user interface itself is closely built around the graphical interfaces of RFEM 6. With this we hope
to provide a familiar experience to all the RFEM users when using this plugin.

```{figure} img/ui_plugin.png
---
height: 500px
name: ui_plugin
---
Example of different layers of the user interface to create the data structure for the plugin when adding a new member.
```

### Creating a new member

To create a new member simply click on `Member` in plugin's tab {numref}`ui_member`. The in {numref}`ui_plugin` will
open.

```{figure} img/ui_member.png
---
height: 200px
name: ui_member
---
Example of the plugin's tab where all the functions for the user-interface can be accessed.
```

Now follow these steps to create a new member:

1. Click on `New` to add a new member.
2. Select the newly created member, and change the name if needed.
3. Create a new section, by clicking on `Section` or choose an already existing section from the dropdown menu.
4. Choose the `Member Type` with the dropdown menu.
5. Adjust `Eccentricities` and `Hinges` if needed.

```{figure} img/ui_member_guide.png
---
height: 500px
name: ui_member_guide
---
Steps to create a new member in the data-model.
```

### Creating a load

Different types of loads can be created:

- Nodal Loads
- Uniform Line Loads
- Varying Loads
- Uniform Surface Loads

```{figure} img/ui_loads.png
---
height: 200px
name: ui_loads
---
Different types of loads that can be created with the plugin and its UI.
```

The general UI for loads will be explained with the window for `Uniform Surface Loads` but is analogous
for `Nodal Loads`
and `Uniform Line Loads`. `Varying Loads`will be explained separately [here](Varying_Loads).

After clicking on `Uniform Surface Loads` its window will appear.

```{figure} img/ui_surface_loads.png
---
height: 500px
name: ui_surface_loads
---
UI for surface loads.
```

Now follow these steps to create a new load:

1. Click on `New` to add a new load.
2. Select the newly created load, and change the name if needed.
3. Choose the `Action Category`. These correspond to the ones in RFEM 6.
4. Choose the `Load Direction`. These correspond to the ones in RFEM 6.
5. Enter the magnitude of the load.
6. Check `Active self-weight` if needed.

(Varying_Loads)=

#### Varying Loads

For `Varying Loads` the process is the same as described above, except that the magnitude of the loads have to be
entered with a table.

```{figure} img/ui_varying_loads.png
---
height: 500px
name: ui_varying_loads
---
UI for varying loads. Set the value in the table template created for the value by the plugin in the Editor. 
```

After creating the load, the a template table to enter the magnitudes and their geometrical properties can be found
under the created component in the editor.

```{figure} img/editor_varying_loads.png
---
height: 250px
name: editor_varying_loads
---
Varying loads component in the `SIMULTAN-Editor`. Under the parameter `p` the template table can be found to adjust the loads.
```

### Creating Supports

Different types of supports can be created:

- Nodal Supports
- Line Supports
- Surface Supports

```{figure} img/ui_supports.png
---
height: 150px
name: ui_supports
---
Different types of supports that can be created with the plugin and its UI.
```

The general UI for supports will be explained with the window for `Nodal Supports` but is mainly analogous
for `Line Supports` and ` Surface Supports`. Deviations will be explained separately and are mainly part of the
`Nonlinearities`.

After clicking on `Nodal Supports` its window will appear.

```{figure} img/ui_nodal_supports.png
---
height: 500px
name: ui_nodal_supports
---
UI for nodal supports.
```

Now follow these steps to create a new support:

1. Click on `New` to add a new support.
2. Select the newly created support, and change the name if needed.
3. Adjust `Translational Nodal Support Conditions`
4. Adjust `Rotational Nodal Support Conditions`
5. Select `Nonlinearity` for the different directions if needed.

```{note}
Based on the `Nonlinearity` selected either value fields will appear or there will be a note to adjust the values 
in the table of the created component if needed.
```

### Creating Surfaces

The creation of surfaces with the UI is still under development. As a workaround please copy the provided template
component and also its geometry reference counterpart and adjust them to your needs.

```{figure} img/ui_surface_temp_comps.png
---
height: 500px
name: ui_surface_temp_comps
---
Template component for surfaces.
```

Building components which are correctly saved in the datastructure will be recognized by the UI and structural analysis
relevant parameters can be adjusted in the UI itself.

```{figure} img/ui_surfaces.png
---
height: 500px
name: ui_surfaces
---
UI window for surface definitions.
```

```{note}
The thickness has to be adjusted in the `SIMULTAN Editor` for now.
```

## Connecting components with the geometry

The before created components are a representation of the information needed for the structural analysis. Connect the
components to the geometry as needed. Please consult
the [SIMULTAN Editor User Guide](https://github.com/bph-tuwien/SIMULTAN.Documentation/wiki)
for general information on how to link components and geometrical information.

An outline of the most important links and how to create them will be given here.

### Surfaces

Information for surfaces is autogenerated via the already existing reference geometry since this data is not exclusive
to structural analysis.

If you are solely working on structural analysis you can assign the components to the surfaces, just as you are used to.

### Members

Geometrical lines connected to physical properties for structural analysis, e.g. beams or columns, are called members in
RFEM. To add a `Section-Component` existing in the data model to a line follow these steps:

- select the line in the `Geometry Editor`
- Open the `Property Editor` for the selected line
- Choose the Component you want to link from the pop-up window

```{figure} img/add_member.png
---
height: 500px
name: add_member
---
Example how to link a `Section-Component` to a geometrical line in the `Geometry Editor` using its `Property Editor`.
```

### Supports

Supports are linked to vertices/lines/surfaces in the geometrical model. To add an existing `Support-Component` to a
geometry in the geometrical model follow these steps:

- Select the node/line/surface in the `Geometry Editor`
- Open the `Property Editor` for the selected node
- Choose the Component you want to link from the pop-up window

```{figure} img/add_support.png
---
height: 500px
name: add_support
---
Example how to link a `Support-Component` to a geometrical node in the `Geometry Editor` using its `Property Editor`.
```

### Loads

Loads are linked to vertices/lines/surfaces in the geometrical model. To add an existing `Load-Component` to a geometry
in the geometrical model follow these steps:

- Select the node/line/surface in the `Geometry Editor`
- Open the `Property Editor` for the selected node
- Choose the Component you want to link from the pop-up window

```{figure} img/add_load.png
---
height: 500px
name: add_load
---
Example how to link a `Load-Component` to a geometrical node in the `Geometry Editor` using its `Property Editor`.
```

```{note}
The same `Support-Component` or `Load-Component` can be linked to multiple different geometrical instances. 
For example, if the same force is attacking on two differnet surfaces, the same component is used from the data model.
An in depth look at this you can find in [this chapter](SIMULTAN_Datastructure_to_incorporate_the_RFem_Data_model.md).
```
