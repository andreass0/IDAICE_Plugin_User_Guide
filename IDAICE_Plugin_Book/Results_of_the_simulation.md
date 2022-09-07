(Results_of_the_simulation)=

# Results of the simulation

## Visual results

For now the simulation results can only be viewed in RFEM itself, {numref}`rfem_sim_results`.

```{figure} img/rfem_sim_results.png
---
height: 350px
name: rfem_sim_results
---
Results of a FE-analysis with RFEM 6 for an exported SIMULTAN model.
```

## Additional information

This restriction is due to the fact that the SIMULTAN Editor has no functionality for mesh visualization implemented
yet. Since simulation results of finite element calculations are dependent on proper visualization it was decided to
delay this feature till the SIMULTAN Editor can provide this functionality.

```{note}
As a workaround one can attach the calculation protocol and the RFEM model to the `Structural Analysis Component`.
```
