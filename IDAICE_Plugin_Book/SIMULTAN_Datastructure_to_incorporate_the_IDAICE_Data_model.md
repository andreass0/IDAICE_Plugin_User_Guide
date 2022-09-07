(SIMULTAN_Datastructure_to_incorporate_the_RFem_Data_model)=

# SIMULTAN Datastructure to incorporate the RFEM Data model

## Digital Twin and data model for structural analysis

In {numref}`struct_anal_comp` a simplified depiction of the digital twin and the `Structural Analysis Component` is
given. This component is used in the SIMULTAN datamodel to store the information needed to export data with the RFEM
Plugin to enable structural analysis simulations in RFEM 6. The global structural analysis can be simplified into 3 main
containers of information, which are independent of each other. They are represented by their own compoenents in the
SIMULTAN data model, everyone of them holding sub-components for further detailed information.

```{figure} img/schematic_components_struc.jpg
---
height: 750px
name: struct_anal_comp
---
Simplified depiction of the representation of a Digital Twin with a `Structural Analysis Component`.
```

The connection and dependency between some of these components is indicated in {numref}`struct_anal_comp` by the blue
lines with arrows next to `Component with physical information`, `Component for geometric assignment` and
the `Structural Analysis Component`.

In the SIMULTAN Editor these components could be represented in the ways shown in {numref}`digitwin_simultan` and
{numref}`comp_simultan`.

```{figure} img/digitwin_simultan.jpg
---
height: 250px
name: digitwin_simultan
---
Collapsed model of a digital twin for a *Tiny House* in the SIMULTAN Editor.
```

```{figure} img/comp_simultan.jpg
---
height: 750px
name: comp_simultan
---
Representation of the depicted components in the SIMULTAN Editor.
```

## Structural Analysis Component in depth

If we take a more detailed look into the `Structural Analysis Component` we can see the references and dependencies
created to link and store information in {numref}`struct_comp_detail`. Here the data structure with modelling
information, references and dependencies for a section are shown. In this case this section represents a steel beam
which will be exported to RFEM 6 with the plugin for a finite element analysis.

```{figure} img/struct_comp_detail.jpg
---
height: 750px
name: struct_comp_detail
---
Detailed depiction of the representation of a section in the Digital Twin.
```

## Data modelling decisions for data representation

Due to the fact that in structural analysis often times the same data is used in different geometrical locations (e.g.
force attacking at multiple locations) the component storing the information for these repeatedly used data is only
created once and instances of the component are storing the differing geomtrical information. This helps to avoid
cluttering of the data model is avoided.

The instances can be accessed from the SIMULTAN Editor as shown in {numref}`show_instances` and further information is
displayed in the opened tab, {numref}`instance_window`.

```{figure} img/show_instances.png
---
height: 250px
name: show_instances
---
Right click to access instances of a component.
```

```{figure} img/instance_window.png
---
height: 250px
name: instance_window
---
Further information can be accessed from the opened instances tab.
```