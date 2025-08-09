(Sync_Import)=

# Sync Import 

The `Sync Import` function enables changes in IDA-ICE to be quickly transferred to SIMULTAN. Once the data model has been imported from IDA-ICE into Simultan, all subsequent changes in IDA-ICE can be updated in Simultan using the *Sync Import* button. This saves time and makes it easy to always have the latest data from IDA-ICE in Simultan. <!-- Logik und Lesbarkeit vebessert! -->

## Establish a connection to IDA-ICE

To ensure that parameters with certain values are transferred from IDA-ICE to SIMULTAN, make sure that the `Sync with External Application` function is activated in the *Property Editor* under source {numref}`parameter_import_sync`. Without this setting, the parameter cannot accept external data.

```{figure} img/parameter_import_sync.png
---
name: parameter_import_sync
---
Button to receive Data from IDA-ICE.
```

If you now press the *Sync Import* button, the value from IDA-ICE is read.  
This allows users to obtain the latest data from IDA-ICE directly into their Simultan model with minimal effort. <!-- Satz wurde verbessert und richtiggestellt!-->

## Visual differentiation

```{figure} img/source_unterschied.png
---
name: source_unterschied
---
Difference between source types in Simultan.
```
In {numref}`source_unterschied` you can see that the differently selected source types can also be distinguished visually with different icons.


