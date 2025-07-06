(Sync_Import)=

# Sync Import 

The `Sync Import` function enables changes in IDA-ICE to be quickly transferred to SIMULTAN. Without having to import the IDA-ICE file (.idm) again. This saves computing power and time.  
The main focus of the `Sync Import` function is to work with current data. Data can be linked to external applications like IDA-ICE.

## Establish a connection to IDA-ICE

To ensure that parameters with certain values are transferred from IDA-ICE to SIMULTAN, make sure that the `Sync with External Application` function is activated in the **Property Editor** under source. Without this setting, the parameter cannot accept external data.

```{figure} img/parameter_import_sync.png
---
name: parameter_import_sync
---
Button to receive Data from IDA-ICE.
```

If you now press the Sync Import button, the value from IDA-ICE is read.  
This means that it is always possible to work with realistic and variable data in order to achieve an optimum simulation.

## Visual differentiation

```{figure} img/source_unterschied.png
---
name: source_unterschied
---
Difference between source types in Simultan.
```
In {numref}`source_unterschied` you can see that the differently selected source types can also be distinguished visually with different icons.

<!-- Richtigkeit kontrollieren!-->
<!-- alles selber testen um sicher zu gehen dass alles auch so funktioniert!-->
<!-- funtkioniert noch nicht richtig im JupyterBuch -->