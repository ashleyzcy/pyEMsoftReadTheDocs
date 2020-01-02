<img src="icon.png" width="200" height="200">

# pyEMsoft

> This is a documentation repository for pyEMsoft, held on 
[readthedocs](https://pyemsoftreadthedocs.readthedocs.io/en/latest/index.html). 

> pyEMsoft is a Python interface to the many Fortran types and subroutines in 
[EMsoft](https://github.com/EMsoft-org/EMsoft).

> An extension module is created automatically with [f90wrap](https://github.com/marcdegraef/f90wrap) that can be directly imported in Python `import pyEMsoft`.

## Installation

> Details on installation can be found in [readthedocs](https://pyemsoftreadthedocs.readthedocs.io/en/latest/Installation.html).

- Install [EMsoft SDK](https://github.com/EMsoft-org/EMsoftSuperbuild)
- Compile [EMsoft](https://github.com/EMsoft-org/EMsoft) onto your local computer
- Install python 3.x (other python packages are needed to run examples include: jupyter notebook, pyyaml, scikit-image, h5py, matplotlib)
- Install [f90wrap](https://github.com/marcdegraef/f90wrap) (windows support is currently being looked at)
- Use `run_pyEMsoft.sh` (located in the EMsoftBuild folder) to generate pyEMsoft module


## Functions

pyEMsoft has access to some of the functions in EMsoft including:

- physical constants (ionic radii, Planck constant, Boltzmann constant, atomic weights, element symbols, etc)
- crystallographic symbols and point/space groups
- quaternion computations (normalization, multiplication, devision, complex conjugate, inner product, inter-quaternion angle, quaterion rotation, interpolation between two quaternions, random quaternion generator, etc)
- conversion between different rotation representations (axis-angle pair, Rodrigues-Frank vector, quarterions, stereographic vector, homochoric vector, cubochoric vector, Euler angles, orientation matrix)
- HDFsupport to export or import EMsoft specific HDF5 data sets (crystal.xtal, EBSDmaster.h5, EBSD_MonteCarloData.h5)
- calculate allowed diffraction vectors
- access to diffraction group, crystal point group, Laue group, projection diffraction group and many 2D symmetry point groups (for bright field, dark field, whole pattern diffraction) based on crystal structure data (.xtal), crystal point group number, zone axis ([uvw]) information.
- Lambert square projection (and its inverse)
- diffraction angle (2 theta) of a plane
- electron's physical properties based on SEM's accelerating voltage
- scattering factor sets, mean inner potential, interaction constant for a given crystal structure file (.xtal)
- etc.

## Contributors

EMsoft started as a source code base used for the creation of all figures in the *Introduction to Conventional Transmission Electron Microscopy* text book (Cambridge University Press, 2003, ISBN 0521629950) by M. De Graef.  It has since grown into an open source project that has had many contributors and testers over the past 15 years (in no particular order):

- Patrick Callahan
- Saransh Singh
- Stuart Wright
- Elena Pascal
- Will Lenthe
- Chaoyi Zhu
- Joseph Tessmer
- Ke-Wei Jin
- Michael Atkinson
- Joao Fonseca
- Michael Jackson
- Joey Kleingers
- Håkon Wiik Ånes
- McLean Echlin

## Financial Support

EBSD/ECP/EKP development of this package, including dictionary indexing for EBSD/ECP, was started with support from 
an AFOSR/MURI grant, FA9550-12-1-0458; the original EBSD code from CTEMsoft 2.0 was developed with support from 
an ONR grant, N00014-12-1-0075. All recent development of TKD and related modalities, including the creation of 
routines that can generate PoVRay visualization script files, was performed with support from an ONR Vannevar Bush 
Fellowship, N00014-­16-­1-­2821.

## License

Copyright © 2013-2019
Marc De Graef Research Group/Carnegie Mellon University

All rights reserved.Redistribution and use in source and binary forms, with or without modification, are 
permitted provided that the following conditions are met:

- Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
- Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
- Neither the names of Marc De Graef, Carnegie Mellon University nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, 
INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE 
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR 
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE 
USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.