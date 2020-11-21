# NAMD GPU FEP example input files

This example is modified from the [FEP tutorial of NAMD](https://www.ks.uiuc.edu/Training/Tutorials/namd/FEP/tutorial-FEP.pdf), and the GPU resident mode is used.

## Traditional GPU mode

In many case you will need applying restraints in alchemical calculations. Sadly, currently NAMD has no stable support of running the GPU-resident mode with [Colvars](https://github.com/Colvars/colvars) enabled. Consequently, if you have to use Colvars in your alchemical calculations, you can only accelerate the simulations with the traditional GPU code path, which evaluates all forces on GPU and then integrates on CPU. Of course, the traditional GPU code path is still faster than the pure CPU version.

For enabling the traditional GPU mode, you just need to keep the same input files as how you run your CPU-only simulations. Nothing needs to be changed.

## GPU-resident mode

If you do not need Colvars or other features that are not available in the GPU-resident mode, you can enable this mode to accelerate the FEP simulations a lot by inserting the following option in your NAMD configuration file:
```
CUDASOAintegrate on
```

## NAMD version

Only NAMD 3.0 supports accelerating FEP simulations on GPU, the download links can be found at:

[NAMD 3.0 Alpha](https://www.ks.uiuc.edu/Research/namd/alpha/3.0alpha/)

Please note the multi-GPU version is still broken for running FEP with GPU-resident mode, so you would use the "NAMD 3.0 **Single-GPU-Per-Replicate** Alpha Versions".

## Running this example

```
namd3 +devices 0 +p2 +idlepoll ./forward-shift-long.namd
```
