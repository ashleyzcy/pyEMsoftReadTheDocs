Installation
====================================
.. role:: bash(code)
   :language: bash

The pyEMsoft modules can only be generated after EMsoft has been built:

- To compile EMsoft, you need to first build the `Software Developer Kit <https://github.com/EMsoft-org/EMsoftSuperbuild>`_ on your operating system. 
- Then, follow the instructions in `EMsoft <https://github.com/EMsoft-org/EMsoft>`_ to compile the EMsoft modules and programs. 
- Toggle ON the build option to build dynamically linked libraris :bash:`BUILD_SHARED_LIBS=ON` e.g. libEMsoftLib.so in the CMakeCache.txt.
- Next, complete the EMsoft package configuration following the `EMsoft Wiki Package Configuration <https://github.com/EMsoft-org/EMsoft/wiki/Package-Configuration>`_.
- To test if EMsoft has been configured correctly,run a simple example such as `Crystal Data Entry Example <https://github.com/EMsoft-org/EMsoft/wiki/Crystal-Data-Entry-Example>`_.
- Create a Ni.xtal crystal file in the XtalFolder folder and this will be later used for unittests.
- Have Python 3.x installed then pip install numpy (other packages are needed to run examples include: jupyter notebook, pyyaml, scikit-image, h5py, matplotlib). 
- Git clone the `f90wrap <https://github.com/marcdegraef/f90wrap>`_ from our repository which contains minor changes for pyEMsoft. Install `f90wrap <https://github.com/marcdegraef/f90wrap>`_ Install with the setup.py (:bash:`python setup.py install`) and check if f90wrap and f2py-f90wrap have been added to path. These are the two important executables to generate the wrappers.
- In the EMsoftBuild, use the auto-generated shell scripts run_pyEMsoft.sh (for pyEMsoft module) to compile the extension modules (_pyEMsoft.*.so and pyEMsoft.py)
- In the EMsoftBuild, run_docs.sh can be used to generate a local copy of the documentation.
- In the Anaconda environment (if f90wrap is install in Anaconda environment), there might potentially be an issue in linking some of the dynamic libraries (see the Debugging section about how to fix these). 
- Install pyEMsoft as a Python package with :bash:`python setup.py install` from the pyEMsoft build folder.

Dependencies
------------------------------------
* Github
* EMsoft_SKD
* EMsoft
* Python 3.x (unittest files and examples provided in Python 3.x)
* recent version of numpy which includes support for f2py
* Fortran compiler gfortran 6.3+ or ifort 12+
* f90wrap

Supported Platforms 
------------------------------------
Currently, Windows system is not fully supported because f90wrap has only been tested on Mac and Linux system. 

For Windows users, we recommend using the `Windows Subsystem for Linux (WSL) <https://docs.microsoft.com/en-us/windows/wsl/install-win10>`_.  

+--------------------------------+-----------------------------------------+----------------------------------------+
| Operating System               |        C/C++ Compiler                   |     Fortran Compiler                   |       
+================================+=========================================+========================================+
| macOS (10.12)                  | Xcode Native tools (8.3.x)              | GFortran 6.3.0 and above               | 
+--------------------------------+-----------------------------------------+----------------------------------------+
| Windows (10)                   | Visual Studio 2015 (CE/Pro)             |      Intel Fortran v17                 |
+--------------------------------+-----------------------------------------+----------------------------------------+
| Linux (Ubuntu 16.x, CentOS 7.x)| GCC 4.8 and Above/Clang 3.8 and greater |     GNU Fortran 5.4.1 20160904 or newer|          
+--------------------------------+-----------------------------------------+----------------------------------------+

Debugging
------------------------------------
For more technical aspects of the build process, please refer to a journal paper by `Pearu Peterson <http://cens.ioc.ee/~pearu/papers/IJCSE4.4_Paper_8.pdf>`_

The error information regarding the build is logged in the build_error.log file. However, if incorrect libraries are linked,
you are not gonna find any clue in the log file unless you import the built pyEMsoft module. 

For macOC (Darwin):
~~~~~~~~~~~~~~~~~~~~~~
To check what dynamic libraries are linked to the shared library file (.so), you can use :bash:`otool -L *.so` to check the linked dynamic libraries. 
Note that the Accelerate.framework is for the lapack library.

.. code-block:: bash

    _pyEMsoft.cpython-37m-darwin.so:
    /usr/local/gfortran/lib/libgomp.1.dylib (compatibility version 2.0.0, current version 2.0.0)
    /usr/local/gfortran/lib/libgfortran.3.dylib (compatibility version 4.0.0, current version 4.0.0)
    /Applications/Build_SDK/EMsoft_SDK/fftw-3.3.8/lib/libfftw3.3.dylib (compatibility version 9.0.0, current version 9.8.0)
    /System/Library/Frameworks/Accelerate.framework/Versions/A/Accelerate (compatibility version 1.0.0, current version 4.0.0)
    /usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1238.60.2)
    /usr/local/gfortran/lib/libgcc_s.1.dylib (compatibility version 1.0.0, current version 1.0.0)
    /usr/local/gfortran/lib/libquadmath.0.dylib (compatibility version 1.0.0, current version 1.0.0)

In Anaconda environment, the f90wrap will link against libraries in the ../Anaconda/lib folder which contains outdated version of 
libgfortran library (does not support ieee_arithmetic) and probably an incomplete libgomp (openMP) library. 

If you are not certain what's missing in the library (usually import pyEMsoft will tell you), use the :bash:`nm` command to reveal all the linked (statically and dynamically) contents and compare with the linked contents (also :bash:`nm` command) of
the shared library (.so). In mac, you can also use :bash:`install_name_tool -change old new` to fix the libraries without needing to rebuild pyEMsoft. 


For Linux (Ubuntu):
~~~~~~~~~~~~~~~~~~~~~~
To check what dynamic libraries are linked to the shared library file (.so), you can use :bash:`ldd *.so` to check the dynamically linked dynamic libraries. One potential issue might be related to the location of fftw3 library since for some systems it is located in the lib64 folder instead of lib folder.

Here is an example successfully built from WSL. Because a program needs to know where to look for library files, we must add that location to the environmental variable. For missing link to any .so file, add the environment variable using the following command: :bash:`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/full path/to/so.file/`

.. code-block:: bash

    linux-vdso.so.1 (0x00007ffecc7a6000)
    libgfortran.so.5 => /lib/x86_64-linux-gnu/libgfortran.so.5 (0x00007f46f6f4a000)
    libEMsoftLib.so => /home/chaoyi/EMsoftBuild/Release/Bin/libEMsoftLib.so (0x00007f46f6143000)
    libEMsoftHDFLib.so => /home/chaoyi/EMsoftBuild/Release/Bin/libEMsoftHDFLib.so (0x00007f46f5bdf000)
    libEMOpenCLLib.so => /home/chaoyi/EMsoftBuild/Release/Bin/libEMOpenCLLib.so (0x00007f46f5bbc000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f46f59ca000)
    libquadmath.so.0 => /lib/x86_64-linux-gnu/libquadmath.so.0 (0x00007f46f5980000)
    libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007f46f582f000)
    libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007f46f5814000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f46f7e17000)
    libfftw3.so.3.5.7 => /home/chaoyi/EMsoft_SDK/fftw-3.3.8/lib/libfftw3.so.3.5.7 (0x00007f46f56ed000)
    liblapack.so.3 => /lib/x86_64-linux-gnu/liblapack.so.3 (0x00007f46f5049000)
    libmvec.so.1 => /lib/x86_64-linux-gnu/libmvec.so.1 (0x00007f46f501d000)
    libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007f46f5015000)
    libgomp.so.1 => /lib/x86_64-linux-gnu/libgomp.so.1 (0x00007f46f4fd3000)
    libOpenCL.so.1 => /lib/x86_64-linux-gnu/libOpenCL.so.1 (0x00007f46f4dc8000)
    libblas.so.3 => /lib/x86_64-linux-gnu/libblas.so.3 (0x00007f46f4d5b000)
    libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f46f4d38000)

Unit tests
------------------------------------
A collection of unit tests can be found in the pyEMsoft/unittests folder. Execute any of them with the following command: :bash:`python test_XXXX.py`. Some of them might require a crystal file or euler angle file relative to the EMdatapathname.

Examples
------------------------------------
We have included several examples of how pyEMsoft can be used as a python package.

- Example 1: how to create a cystal (xtal) file step by step with pyEMsoft.
- Example 2: basic crystallographic computations
- Example 3: plot a Kikuchi sphere from EBSD master pattern
- Example 4: read and analyze crystal data
- Example 5: how to use image filters 
- Example 6: global optimization for pattern center, orientation and deformation tensor inference
