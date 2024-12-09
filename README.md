# VHDL Counter Race Condition

This repository demonstrates a potential race condition in a simple VHDL counter.  The counter is designed to increment on each rising clock edge, resetting to 0 when it reaches its maximum value (15). However, the current implementation has a vulnerability due to the way the reset and counting logic interact, which can be observed under certain circumstances.

The `buggy_counter.vhdl` file contains the flawed code, while `fixed_counter.vhdl` provides a corrected version.

## Race Condition Explanation

The primary issue lies in the combination of asynchronous reset (`rst`) and the `rising_edge(clk)` sensitivity list within the main process. Depending on the timing relationship between `rst` transitions and the clock, there's a small window where `internal_count` might not update correctly.  This is particularly true at higher clock frequencies.

## Solution

The solution involves using a synchronous reset and separating the reset and increment logic to avoid the potential race condition. This results in more robust counter behavior, even under adverse clock conditions.

## How to Run

1.  Compile and simulate both `buggy_counter.vhdl` and `fixed_counter.vhdl` using your preferred VHDL simulator (e.g., ModelSim, GHDL). 
2. Apply different reset and clock conditions to observe the subtle differences in the counter's output between the two versions.