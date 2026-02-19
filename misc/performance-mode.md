# Performance Mode Settings for Consistent Benchmarking Results

### TL;DR

- Hardware are built with various power management features to tradeoff
  performance with energy consumption. A side effect of these power management
  features is performance nondeterminism. While this is a feature very useful
  for production envinronments, for our lab experiments, we prefer
  reproducibility and performance stabilty, that's why we need to disable those
  power management settings to ensure all the hardware will run at performance
  mode. 

- Simply put, 
  - CPU power management features
    - [Disable] C-states / P-states, two ways to do this
      - Kernel parameters ``intel_idle.max_cstate=0 idle=polling``
      - ``/dev/cpu_dma_latency`` interface, run the 
    - [Disable] Turbo boost feature for Intel CPUs so that CPUs run at a
      constant frequency
      - ``echo 1 | sudo tee /sys/devices/system/cpu/intel_pstate/no_turbo``
  - PCIe ASPM power management
    - ``echo 'performance' | sudo tee /sys/module/pcie_aspm/parameters/policy``

- We have a script to do this all in one place and you should run it first before your experiments.

### More details

- CPU P-states: voltage & frequency, performance states
  - Tools: `cpupower`
  - CPU will do work in any P-state, the difference is how fast it's working at
  - governors
    - performance: force CPU to use the highest possible clock frequency, which
      will be statically set and will not change 
    - powersave: force CPU to use the lowest possible clock frequency, which
      will be statically set and will not change [[speed limiter]]
    - ondemand: dynamically adjust CPU speed according to load, at the expense
      of latency between frequency switching 
    - userspace, used with user space program like `cpuspeed`
    - conservative, like `ondemand` mode, but change frequency gradually, at
      the expense of much worse latency ((why?))
  - intel_pstate, only supports `powersave` and `performance`

- C-states, idle/power states, different sleep levels, higher levels need more
  time to wake up
  - **Tuning**: 
    - `intel_idle.max_cstate=0` disable C-states
    - `processor.max_cstate=1`, prevent from entering power-saving states
    - `idle=polling`, for fastest time out of the idle states, no MWAIT
      mechanism to halt in the idle routine, ((not good for HT??))
    - `/dev/cpu_dma_latency`, write latency QoS (e.g. 0 represent C0), keep FD
      open (alternative to the above kernel parameter method)
  - Tools to use: **i7z** will show how much time CPU stays at each C-state
    level
  - Background knowledge
    - C0: the operating state, meaning the CPU is active and busy doing
      something, all the CPU components are turned on
    - C1: (Halt) not executing instructions, but can return to an executing
      state instaneously 
    - C2: (Stop-Clock), maintains all sw-visible state, take longer to wake up
    - C3: (Sleep), doesn't need to keep its cache coherent, but maintain other
      states

    ```In some sense, P-states and C-states are orthonognal

                  P0   P1   P2   P3   ..
             +-------------------------------------
             |
       +>C0  |    4G   3G   2G   800M (examples for explanation)
       |     |
       | C1  |
       |     |
       +-C2  |    XX
             |
         ..  |

    ```
- Turbo Boost
  - turn off: ``echo 1 | sudo tee /sys/devices/system/cpu/intel_pstate/no_turbo``
  - turn on : ``echo 0 | sudo tee /sys/devices/system/cpu/intel_pstate/no_turbo``


### Some of Huaicheng's Obselete Notes

- River machine tuning
  - Intel Xeon E5-2670 V3, Base frequency: 2.3 GHz, Max Turbo freq: 3.10 GHz
  - By forcing CPU to be always in C0 state, the frequency is 2.6 GHz
  - Next: continue tune BIOS
    - 2.6 GHz is already good, next step is to allow Turbo Boost in BIOS to see
      if it will go better
      - to see if we can get a higher stable frequency level
      - **finally, we would prefer performance stability for reproducible
        results**
    - remove kernel parameters, give more control over OS, do dynamic tuning at
      runtime
    - Enable HyperThreading to see if the performance gets worse
    - Solve the new kernel problem .. Should 4.12 be able to run on River2

- Ucare-07 Tuning
  - Intel Core i7-6700K, Base frequency: 4.0 GHz, Max Turbo freq: 4.20 GHz
  - powersave P-state only ==> freq changes frequently from 800MHz to 4.2GHz
  - change P-state from `powersave` to `performance`, freq still dynamically
    change as `powersave` mode, 99-100% time in C1
  - force C0 state, stable at 4.2GHz
  - adjust `scaling_min_freq` and `scaling_max_freq` to some middle values, the
    CPU frequency will change accordingly ((change from performance to
    powersave mode doesn't affect the results, this seems that C0 is in
    charge!)

- Device Active Power management (PCIe ASPM)
  - ``echo 'performance' | sudo tee /sys/module/pcie_aspm/parameters/policy``
