# cyclogyroOptimization
Optimization procedure to obtain a 3D printed energy efficient hovering cycloidal rotor aircraft

The equations and results coming from this optimization can be seen in the (currently accepted by the [Journal of Applied and Computational Mechanics](https://jacm.scu.ac.ir/)) following paper: 
_**Parametric optimization of a cyclogiro aircraft design for efficient hover with aeroelastic considerations**_ by Louis Gagnon, Marco Morandini, and Stéphane Fournier.
The AEAT and AIAA papers that are mentioned in the code and in the paper can be downloaded here: http://louisgagnon.com/publications.html

This [SageMath](https://www.sagemath.org/) (9.12) code will automatically generate the C++ equations that can be ran with the [Dakota](https://dakota.sandia.gov/) (6.13) optimization toolkit using the [cycloidalEfficiency.in](https://github.com/louisgag/cyclogyroOptimization/blob/main/cycloidalEfficiency.in) input file to find the optimal parameters for best hover energy effiicency.

To generate the C++ code use the following initial parameters:
```
optimRun = bool(1) # true to run an optimization equation generating process (ie skip numerical setting of values)
getCPP = bool(1) # c++ generator
postRun = bool(0) # run as post dakota run thus using the soln values from the dakota result
```
compile the generated code using, for example: `touch test.h; g++ -Wall -O2 -o cycloidalEfficiency cycloidalEfficiency.cpp`
and run it with dakota using: `dakota -i cycloidalEfficiency.in -o cycloidalEfficiency.out > cycloidalEfficiency.stdout`

To obtain the general drone performance indicators (efficiency, deformation, stresses, ...) from a set of parameters (e.g.: the obtained optimum from Dakota) use the following initial parameters:

```
optimRun = bool(0) # true to run an optimization equation generating process (ie skip numerical setting of values)
getCPP = bool(0) # c++ generator
postRun = bool(1) # run as post dakota run thus using the soln values from the dakota result
```

and properly set the parameters in the **if (postRun): # Final values for JACM article** cell.

The code was developped with funding of the [**Polimi International Fellowship**](https://www.polimi.it/en/faculty-and-staff/calls-and-competitions/international-fellowships/) research grant Index no. 1378 - Ref. No. 15881 made available for the [An aeroelastic study of cycloidal rotors used in various configurations](http://louisgagnon.com/cycloPolimiFellowship.html) project which covered the vast majority of the work presented here.

Small revisions to the code were made possible through the support of the [Alexander von Humboldt Foundation](https://www.humboldt-foundation.de/) for the [A Novel and Simple Aircraft Requiring Minimal Power to Hover](http://louisgagnon.com/research/AvH_cyclo.html) project.
