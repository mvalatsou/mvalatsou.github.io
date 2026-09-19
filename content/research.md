+++
title = 'Research'
subtitle = 'Modelling exoplanetary interiors and atmospheres'
math = true
toc = true
+++

## Overview

In my PhD, I am curious to uncover the diversity of super-Earth (planets like the Earth but more massive) atmospheres. From these planets forming to how we observe them today, they have undergone several processes including chemical equilibration, thermal loss, atmospheric escape, and more, and we expect these processes to leave an imprint on the resulting atmospheres --- additionally we expect these processes to grant great diversity! And maybe some of them end up having habitable environments..

## Themes

{{< cards >}}
{{< card title="Interior structure" >}}
Equations of state and mass–radius relations for rocky and volatile-rich
planets.
{{< /card >}}
{{< card title="Interior structure inference" >}}
How to use observations to infer the interior structure of exoplanets.
{{< /card >}}
{{< card title="Fractionated atmospheric escape" >}}
XUV-driven hydrodynamic winds that strip planetary atmospheres, and how the selective loss of lighter species reshapes what is left behind.
{{< /card >}}
{{< card title="Interior–atmosphere coupling" >}}
How outgassing and magma-ocean chemistry set the atmospheric composition we observe.
{{< /card >}}
{{< /cards >}}

## BOREAS

I have developed BOREAS (https://github.com/ExoInteriors/BOREAS, publicly available but not open source yet), a hydrodynamic atmospheric escape code for exoplanetary atmospheres. BOREAS computes mass loss by solving a one-dimensional hydrodynamic Parker-wind formulation that self-consistently determines the wind structure, the XUV absorption radius, and the resulting escape rate. I have coupled it to a fractionation model that self-consistently accounts for different atoms escaping at different rates from a planet's atmosphere, following an established diffusion-drag formalism for multi-species mixtures (H, O, C, N, S). 

## Tools and codes

I have developed BOREAS fully in python. 

I have worked with:
- **MR code** - our group's in house interior structure model, used to calculate radii of planets, interior and atmospheric structures, and used to run interior structure inferences via surrogate model construction and the use of MCMC --- working to make it public (maybe with a new name).
- **Global Chemical Equilibrium** - our group's in house equilibrium chemistry for the entire planet, that redistributes volatiles between core, mantle, atmosphere (https://github.com/ExoInteriors/GlobalChemicalEquilibrium_Release).
- **FastChem** — equilibrium chemistry for exoplanetary atmospheres (https://github.com/newstrangeworlds/fastchem).
