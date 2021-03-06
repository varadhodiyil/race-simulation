# Introduction
This repository contains a race simulation for the simulation of motorsport circuit races. The intended application is
the determination of an appropriate race strategy, i.e. of the pit stops (number of stops, inlaps, tire compound choice,
possibly refueling). The race simulation considers long-term effects such as mass reduction due to burned fuel and tire
degradation as well as the interactions between all race participants. It is based on a lap-wise discretization for fast
calculation times. Probabilistic influences are also modeled and can be evaluated using Monte Carlo simulation. For the
making of automated race strategy decisions, we developed the Virtual Strategy Engineer (VSE).

Contact person: [Alexander Heilmeier](mailto:alexander.heilmeier@tum.de).

# List of components
* `helper_funcs`: This folder contains helper functions that are used in more than one of the programs.
* `racesim`: The folder includes all class definitions required to simulate an entire race (`src` folder). The `input`
folder contains the required parameter files for every race, the `output` folder is created during execution and will
then contain .csv files with lap times, race times, and positions in every lap.
* `racesim_basic`: This folder calculates the best race strategy (leading to a minimal race time) under the 
assumption of a free track, i.e. without opponents. Therefore, it can be seen as a minimalistic race simulation.

# Dependencies
Use the provided `requirements.txt` in the root directory of this repo, in order to install all required modules.\
`pip3 install -r /path/to/requirements.txt`

The code is developed with Python 3.8 on Windows 10 and tested with Python 3.8 on Ubuntu.

### Solutions for possible installation problems (Windows)
`cvxpy`, `cython` or any other package requires a `Visual C++ compiler` -> Download the build tools for Visual Studio
2019 (https://visualstudio.microsoft.com/de/downloads/ -> tools for Visual Studio 2019 -> build tools), install them and
chose the `C++ build tools` option to install the required C++ compiler and its dependencies

### Solutions for possible installation problems (Ubuntu)
1. `matplotlib` requires `tkinter` -> can be solved by `sudo apt install python3-tk`
2. `Python.h` required `quadprog` -> can be solved by `sudo apt install python3-dev`

# Intended workflow
The intended workflow is as follows:
* `racesim_basic`: Use the simplified race simulation to determine the fastest basic race strategy. It can be used as a
first guess for the race strategy in the race simulation.
* `racesim`: Use the race simulation to simulate the race and to optimize the race strategy. The VSE can be used for
other participants if you do not want to determine all strategies manually.

# Running the basic race simulation
If the requirements are installed on the system, follow these steps:

* `Step 1`: You have to adjust a given or create a new parameter file (.ini) for the simulation. The parameter files
are contained in `/racesim_basic/input/parameters`.
* `Step 2:` Check the user inputs in `main_racesim_basic.py`.
* `Step 3:` Execute `main_racesim_basic.py` to start the race simulation.

![Race times for various two-stop race strategies](racesim_basic/racesim_basic.png)

# Running the race simulation
If the requirements are installed on the system, follow these steps:

* `Step 1`: You have to adjust a given or create a new parameter file (.ini) for the race to simulate. The parameter
files are contained in `/racesim/input/parameters`.
* `Step 2:` Check the user inputs in the lower part of `main_racesim.py`.
* `Step 3:` Execute `main_racesim.py` to start the race simulation.

![Race simulation real time output for the Yas Marina racetrack](racesim/racesim_yasmarina.png)

### Virtual Strategy Engineer (VSE)
The virtual strategy engineer (VSE) determines the race strategies of the race participants if activated. It eases the
handling for the user of the race simulation since he must not determine the strategies of all race participants
manually. Several variants of the VSE are available: base strategy, real strategy, and supervised. With the base
strategy option, it uses a pre-defined strategy that was optimized for a minimum race duration (under the assumption of
a race without opponents). With the real strategy option, the strategies of the real-world races are applied. With the
supervised option, the VSE is based on two artificial neural networks to make the race strategy decisions. Our VSE is
focused on Formula 1. Thus, it determines whether a driver should come into the pits and which tire compound to fit.
The initial concept of automated decision-making based on artificial neural networks was developed by André Thomaser
during his semester thesis within the project.

### Contained parameter files
We included exemplary parameter files for the 121 Formula 1 races in the seasons 2014 - 2019. They were automatically
created on the basis of our Formula 1 timing database (link is below). The program used for this was developed by
Marcel Faist as part of his master's thesis within the project. Please keep in mind that an exact reproduction of the
real races in the simulation is practically impossible.

### Detailed description of the race simulation (deterministic parts)
Please refer to our paper for further information:\
Heilmeier, Graf, Lienkamp\
A Race Simulation for Strategy Decisions in Circuit Motorsports\
DOI: 10.1109/ITSC.2018.8570012

### Detailed description of the race simulation (probabilistic effects and random events)
Please refer to our paper for further information:\
Heilmeier, Graf, Betz, Lienkamp\
Application of Monte Carlo Methods to Consider Probabilistic Effects in a Race Simulation for Circuit Motorsport\
DOI: 10.3390/app10124229

### Detailed description of the virtual strategy engineer
Please refer to our paper for further information:\
Heilmeier, Thomaser, Graf, Betz\
Virtual Strategy Engineer: Using Artificial Neural Networks for Making Race Strategy Decisions in Circuit Motorsport\
Currently in review...

# Related open-source repositories
* Lap time simulation: https://github.com/TUMFTM/laptime-simulation
* Race track database: https://github.com/TUMFTM/racetrack-database
* Formula 1 timing database: https://github.com/TUMFTM/f1-timing-database
