Run Simulation with ModelSim
============================

Prequisition
------------

1. Install GoWin IDE;
2. Install ModelSim.

Preparation
-----------

We have to add GoWin simulation library into ModelSim first. Once done, we do
not always add `prim_sim.v` to the simulation project.

### Create Library Directory

1. Find "simlib" directory from GoWin IDE installation directory;
2. Create directory named "lib" inside both "gw1n" and "gw2a" directories;
3. Note the full path to each "lib" directory, we will use it later.
 
### Create Library in ModelSim

1. Select "File->New->Library..." from the top menu;
2. Select "a new library and a logical mapping to it" from the dialog, change
   the Library Name to "gw1n" and Library Physical Name to the path of "lib"
   directory we have noted, which belongs to "gw1n" directory; (e.g.
   $GOWIN_ROOT/IDE/simlib/gw1n/lib)
3. Select "Compile->Compile..." from the top menu;
4. Select Library "gw1n" from the dialog, and look for `prim_sim.v` from
   "gw1n" directory, then "compile";
5. If compilation succeeded, the "gw1n" library is shown in the Library list,
   with lots of modules;
6. Repeat these steps for "gw2a" library.

Run Simulation for Projects
---------------------------

We will run a simple example in this part. Download any reference design from
GoWin's website, unzip, and create a new project in ModelSim. (Select
"File->New->Project...", setting names and paths, and go on.)

Right click from the Project view and add existing files to the project. If
doubted, view some file such as `vcs.sh` or `verdi.sh` in "simulation"
directory from where the files unzipped to, and get a list of files to be
added to the simulation project.

Select "Compile->Compile All". If error encountered, check the include paths.
Right click the files not compiled, select "Properties", add include paths and
run compilation again.

Select "Simulate->Start Simulation...", choose the design for simulation.
Select "Libraries" tab, "Add..." "gw1n" or "gw2a" as the project target to.
Then "OK", start the simulation.

(Optional) If You Are New to ModelSim ...
-----------------------------------------

### Try Setting Waveform for Input Signal

Select any ports from "Objects" view, right click, select "Modify->Apply
Wave...". Also drag the output ports to the wave. After setting up the
waveform, select "Simulate->Run->Run -All", and check the output.
