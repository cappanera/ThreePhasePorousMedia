# Three Phase Flow Code
A codebase using deal.ii that solves the three-phase flow problem in porous media. 
Current version is compatible with deal.ii v9.6.2

# Running The Code

Running the code is pretty straight forward, but you need to be careful on what problem you are solving. When considering new applications or new parameters, three files may require modifications:
```
paramters.prm
aux_primary.cc
aux_primary.hh
```
One applications is provided as example. More will be added in 2026 (quarter five spot and viscous fingers generations setups). The related files can be found in the following directory:
```
EXAMPLES_APPLICATIONS/MANUFACTURED_TESTS
```
By default, the code should have the manufactured test case in the main directory. Just copy from the desired directory and put them in the main directory. Just make sure that when you are done that you save your changes. 

Next,  run 
```
cmake .
```
to generate the necessary build files. Then
``` 
make 
```
to compile. you can in addition run 
```
make release
```
but it's not strictly necessary. Once everything is compiled, you can run the code via
```
.\ThreePhase
```
or 
```
mpirun -np N .\ThreePhase
```
if you want to run in parallel. N is the number of processors you give it.


# Regarding use and installation of this software at the University of Houston

# Installing Deal.ii 
 If you are using the Sabine UH cluster, then you shouldn't need to download dealii and you can skip to the section on running the code. See https://www.uh.edu/research/rcdc/support-and-services/user-guide/getting-started-clusters.php for more details on using the Sabine cluster.

 If you are using the department cluster, you should contact Loic Cappanera to install properly petsc andeal.ii locally before you can use the module. You can also try installing these libraries yourself using the following instructions.

## Installing PETSc
PETSc is an external library that handles a lot of the linear algebra used in the code. You first need to download this library and then pass it as a flag when building dealii.
 Your best bet is to pull the repo from https://gitlab.com/petsc/petsc

and then inside the petsc directory run 
```

./configure --with-shared-libraries=1 --download-hypre=1 --download-mumps=1 --download-scalapack=1 --download-metis=1 --download-parmetis=1 --with-debugging=0 --with-x=0
```
You should keep this in a directory separate from where you install dealii. Then compile and install and run the proper tests to verify everything is working ok.
```
make all check
```
## Building Deal.ii
See the dealii website for detailed installation instructions.
https://www.dealii.org/9.6.0/readme.html

The only thing to keep in mind is that you need to include PETSc as flag with the proper link to its' location. You should run the follow command in the build directory inside the dealii directory you pulled from the github which can be found here.
https://github.com/dealii/dealii
```

cmake -DDEAL_II_WITH_PETSC=ON -DCMAKE_INSTALL_PREFIX=/path/to/where/you/want/dealii/installed -DPETSC_DIR=/path/to/where/PETSc/is/installed -DPETSC_ARCH=/path/to/where/petsc/arch/is/installed -DDEAL_II_WITH_MPI=ON -DDEAL_II_WITH_HDF5=OFF ..
```
## Installing Deal.ii
You then proceed to install deal.ii.
run 

```
make --jobs=N install

make test
``` 
where N is the number of processors you want to utilize to install. Make sure you talk to your dvisor or systems adminstrator on the proper number to use as the program does take quite a long time to install. You then run tests to make sure everything is working properly.

WARNING: Just because you are able to successfully build and install everything doesn't mean you will pass all the tests. Only proceed using the library if all tests have been passed.

