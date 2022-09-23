(Running_a_simulation)=

# Running a simulation

## Exporting the SIMULTAN-model to IDA-ICE

When modelling according to the conventions described in chapter [Setting up a problem](Setting_up_a_problem.md) the
model is ready to be exported. This can be done by clicking the `Export Model` button when you are inside the IDA-ICE
Plugin in the SIMULTAN Editor {numref}`export_model`.

```{figure} img/export_model.png
---
height: 200px
name: export_model
---
Export button to create the file structure to import into IDA-ICE.
```

After clicking the button you will be prompted with a `save dialogue`. Please specify the location where you want to
save the project directory and confirm.

## Importing into IDA-ICE

To import the project simply open the project in IDA-ICE as you would do usually.

```{figure} img/open_idaice.png
---
height: 250px
name: open_idaice
---
Open the exported project in IDA-ICE.
```


## Running a simulation in IDA-ICE

Run the simulation via the `Simulation` tab in IDA-ICE. 

```{figure} img/simulation_tab.png
---
height: 350px
name: simulation_tab
---
Simulation tab. Choose the cases you want to run or simply run the whole simulation.
```

```{note}
To import the results into SIMULTAN you need to run the `Energy Load` simulation. For now only those results will be 
imported into SIMULTAN. 
```