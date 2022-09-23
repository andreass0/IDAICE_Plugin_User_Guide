(Results_of_the_simulation)=

# Results of the simulation

## Import of results

The results can be imported back into SIMULTAN with the `Import results button`. You are prompted with a selection
dialogue,please choose your main .idm-file to import the results of the energy load simulation.

```{figure} img/import_results.png
---
height: 200px
name: import_results
---
Button to import the results of the simulation back into SIMULTAN.
```

The results will be stored under the component `Performance` -> `HygrthermSim` -> `Ergebnisse`. Under this component the
plugin creates a sub-component for each simulation Zone in the data model.

```{figure} img/results_comp.png
---
height: 350px
name: results_comp
---
Component for each of the simulated zones in SIMULTAN
```

Under these components the results of the Energy Load Simulation are stored as timeseries which can be visualized in the
graph visualization function of the Editor.

```{figure} img/results_graph.png
---
height: 500px
name: results_graph
---
Parameters with timeseries for the individual results of the simulation zones
```
