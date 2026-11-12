MATLAB & SIUMULINK code for the flight control computer (FCC) of a challenger 3500.
Control systems are focused on the roll control surfaces.

This FCC is meant to be used in the test plan of the validation and verification plan of the AERO390 project for team R5.

Any stated values come from the aileron hinge moment calculations performed by team R5.

This FCC is a very simplified version of a regular FCC found on the CL3500.

How to generate the Simulink model
1. Open MATLAB with Simulink and Stateflow available.
2. Put `build_Challenger3500_RollFCC_VV.m` in the MATLAB working directory.
3. Run the script.
4. It creates and opens `Challenger3500_RollFCC_VV.slx` and defines parameter structure `P_RollFCC` in the base workspace.
5. Open 'Simulation.slx'. Change any of the 5 input values according to the test at hand and run.
6. Double click on relevant scope blocks to see outputs. Click on data inspector to see output of x&y graph.

First-pass model behavior
- Normal mode: aileron and spoiler commands have the same sign for a given roll command.
- Aileron jam: aileron command is removed and spoiler command remains.
- Spoiler jam: spoiler command is removed and aileron command remains.
- Both jammed: both commands are removed.
- The plant includes simplified first-order/rate-limited surface actuators and a rigid-body roll integrator.

Team R5 based the FCC on the following:

[1]Dr. Salahudden, Aircraft Roll Control Design | SD and Control With MATLAB and Simulink by Dr. Salahudden, (Sep. 26, 2025). Accessed: Nov. 10, 2026. [Video]. Available: https://www.youtube.com/watch?v=rm2tXvYYkNk&t=218s

[2]Siddharth Jawahar, “Pitch-Rate-Controller-For-Aircraft,” Mathworks.com. Accessed: Nov. 03, 2026. [Online]. Available: https://www.mathworks.com/matlabcentral/fileexchange/129809-pitch-rate-controller-for-aircraft

[3]VDEngineering, MATLAB & Simulink Lecture: The Aerospace Blockset (Walkthrough + 2 Examples), (Feb. 10, 2018). Accessed: Nov. 10, 2026. [Video]. Available: https://www.youtube.com/watch?v=X_dGm1mhHsM&list=WL&index=3&t=30s


Created by:
Adèle Pinheiro St-Pierre
40309682
