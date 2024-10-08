# PhaseStim2022_Yu
Real-time phase detection and phase-specific stimulation system. We have a [python package](https://github.com/JhanLiufu/PhaseStimAnalysis2022_Yu/tree/master?tab=readme-ov-file) for analyzing stimulation outcome. For more introduction of the project, see its [project page](https://jhanliufu.github.io/projects/closed_loop_control.html) on Jhan's website.

## Installation
Clone or download this repository, ```cd``` into the repository and run ```pip install .```

## Launch the system
Run the following command: ```python ControlCode --params config/[your-config-file].json```

## Files 
- **[trodes_connection.py](trodes_connection.py)** contains functions to interface with the [Trodes](https://spikegadgets.com/) system. We stream local field potential (LFP) signal from Trodes and issue stimulation command to Trodes.
- **[echt.py](echt.py)** implements the **endpoint-corrected Hilbert transform (ecHT)**, originally proposed by [Schreglmann et.al](https://www.nature.com/articles/s41467-020-20581-7). ecHT is a phase estimation algorithm that tracks the current oscillatory phase of an ongoing oscillatory signal.
- **[detector.py](detector.py)** defines the **Detector** object. A detector iteratively streams LFP from Trodes, estimates the current phase using echt, and issues a stimulation command to Trodes when the current estimated phase reaches the specified target phase.
- **[ControlCode.py](ControlCode.py)** establishes connection with Trodes and starts the detectors. Leveraging [multiprocessing](https://docs.python.org/3/library/multiprocessing.html) in python, the system can run an arbitrary number of detectors, each having their own parameters and output to separate Trodes digital outputs. The detector parameters are specified in JSON configuration files in [config](config).
