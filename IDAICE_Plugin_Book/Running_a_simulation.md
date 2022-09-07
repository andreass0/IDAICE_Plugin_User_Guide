(Running_a_simulation)=

# Running a simulation

## Exporting the SIMULTAN-model to RFEM

When modelling according to the conventions described in chapter [Setting up a problem](Setting_up_a_problem.md) the
model is ready to be exported. This can be done by clicking the `Export Model` button when you are inside the RFEM
Plugin in the SIMULTAN Editor {numref}`export`.

```{figure} img/export.png
---
height: 250px
name: export
---
Export button to create the XML-file to import into RFEM 6.
```

After clicking the button you will be prompted with a `save dialogue`. Please specify the location where you want to
save the XML-file and confirm.

## Importing into RFEM

To import the XML-file open RFEM 6 and choose the `Import XML function` {numref}`import_xml`.

```{figure} img/import_xml.png
---
height: 250px
name: import_xml
---
Import XML function in RFEM 6.
```

Navigate to the location on your disk where you have saved the exported model and confirm to load it. After the model is
loaded the it will appear in RFEM 6 and is ready for further manipulation {numref}`model_in_rfem`.

```{figure} img/model_in_rfem.jpg
---
height: 250px
name: model_in_rfem
---
Imported model in RFEM 6 based on an export from a SIMULTAN model.
```

```{warning}
In the current state of development the plugin is **NOT** bidirectional. Any adaptations done in RFEM are only 
available in RFEM and cannot be retrieved into the SIMULTAN datamodel. This is a funcitonality which will be 
implemented in the future. For now use RFEM as a solver and adjust the model in the SIMULTAN Editor.  
```

## Running a simulation in RFEM

To run a simulation create load combinations in RFEM and run the simulation as usual in the finite element software.

```{note}
Maybe some equal instances of faces or vertices will be detected by RFEM. Ignore this message for now. This is a known
behaviour of the plugin. The exploration of this will be part of our future development.
```

```{figure} img/plausibility_check_rfem.png
---
height: 250px
name: plausibility_check_rfem
---
Ignore the plausibility check.
```