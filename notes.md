### Scratch Map
- `machine.debug_info.scratch_map`
- it's debug info though
- addr : (name, length)

### Running cores
About cores
- they can be running, paused or stopped
- `core.pc` is program counter

- `Machine.run()`
- if core is not running it will continue
- if program counter is high, then core is stopped and we also continue
- `self.step` runs the instruction

### Machine.step
- instructions are name: slots

# The instructions
ALU
- does some arithmetic
- alu: op, dest scratch address, a1 addr, a2 addr

VALU
- does a vector of 8 elements
- has vbroadcast, multiply_add and any ops from ALU
- broadcast writes one value into multiple destinations
- multiply add computes a * b + c

LOAD
- load addr into scratch or load an addr + offset into scratch dest + offset
- vload can load 8 things
- const just writes a constant value into scratch

FLOW
- select writes cond != 0 ? a : b. Cond lives in scratch too
- add_imm just adds an imm to scratch[a] so it's like an immediate add, no need to load stuff
- vselect is just vector select
- select dest cond a, b

### scratch write and mem write
- get initialized at every step but deleted at the end
- it does all the instructions first and then it will write scratch writes to scratch and mem write to mem

# Building the kernel
- basically you allocate your scratch ahead of time
- then, you write your kernel and you use `.build()` to add to instructions and yeah.

# Perfetto traces
- run python3 watch_trace.py and you're good. Learn how Perfetto works. 

# Debug instruction
- it's found in the `step`function, you can do compare or vcompare

# Running the thing
- just look at `perf_takehome.py` bottom of page

# Inputs
- wait so inputs is just a bunch of random numbers of size `batch_size`
- you read from input indices and values and t.values, you write to input values and indices but you never modify the tree.

- we can just grab both 2*x+1 and 2 and start modifying that shit

# Mod 1
- let's try modifying `1 if val % 2 == 0 else 2` to just be `val % 2 + 1`
- I also packed some instructions together