(Results_of_the_simulation)=

# Results of the simulation

## Import of results

The results can be imported back into SIMULTAN with the `Import results button` {numref}`import_results`. You are prompted with a selection
dialogue, please choose your main .idm-file to import the results of the energy load simulation.

```{figure} img/import_results.png
---
name: import_results
---
Button to import the results of the simulation back into SIMULTAN.
```

The results will be stored under the `Taxonomie: Results Zone`.Under `IDA ICE Analysis` the
plugin creates a sub-component for each simulation Zone in the data model (see {numref}`results_comp`). <!-- stimmt nicht, herrausfinden wie es wirklich ist-->

```{figure} img/results_comp.png
---
height: 350px
name: results_comp
---
Component for each of the simulated zones in SIMULTAN
```

Under these components the results of the Energy Load Simulation are stored as timeseries which can be visualized in the
graph visualization function of the Editor {numref}`results_graph`.

```{figure} img/results_graph.png
---
name: results_graph
---
Parameters with timeseries for the individual results of the simulation zones
```
