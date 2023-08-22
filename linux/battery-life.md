# Optimizing battery life on Thinkpad X270

## CPU power management
Start by installing the `cpupower` package and running `sudo cpupower frequency-info`, which tells you the current driver used for CPU power management. By default, my laptop uses `intel_pstate`. Next, install `s-tui` and `powertop` and run them (`sudo powertop --calibrate`).
**TODO LATER: ** follow the rest of this guide [here](https://amanusk.medium.com/an-extensive-guide-to-optimizing-a-linux-laptop-for-battery-life-and-performance-27a7d853856c)

## TLP
Install TLP with `paru -S tlp`.
