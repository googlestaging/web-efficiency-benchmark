# Web Efficiency Benchmark

The web efficiency benchmark is a tool that assists with measuring 
[efficiency metrics][2] for computers using browser based workloads.

This benchmark is a companion to the [native benchmark][1] that has been 
developed by GTD, but is targetted at workloads that can be executed in the
device's browser, for devices where web browsing is the fundamental user
experience.


## Problem Description

There are a large number of devices where the existing native efficiency
benchmark may not be suitable, for example:
* ChromeOS, where there is not a supported native environment to run the
benchmark.
* ARM devices, which are incompatible with the X86 specific native benchmark.
* Netbooks and other devices whose primary intention is to interact with the
web and not perform the kind of workloads that are in the native benchmarks.

For these devices, we require a benchmark that best represents the purpose of
the device, which is primarily to interact using a web browser. Thus we require
a representative benchmarking suite that will reflect a user's core use cases,
while rewarding devices that are able to execute these use cases in an energy
efficient manner. Improvements in efficiency scores should be directly relatable
to an improved user experience on the device.


## Benchmark Design

### Worklets
For details of the execution of the native benchmark refer to [Software
Test-Suite for Computer Energy Efficiency Measurement][1].

What is relevant for this application is that the overall benchmark is broken
down into smaller, individual worklets. A worklet is a set of tasks that can be
combined into a sequence of activities that can easily be reproducible on a
regular basis. Worklets execute on the device under test (DUT).

For web benchmarking, all worklets will execute in the context of the chrome web
browser, running on the operating system of the DUT. Chrome has been chosen
because:
* It is available on all target architectures for testing.
* It is the most popular browser in use today, so results will be reflective of the majority user experience.
* It exposes core user experience metrics that we can use to calculate worklet performance.

### Efficiency Calculations
For complete background please refer to the document [White paper on the
definition of efficiency metrics for computers][2] which goes into detail about
efficiency benchmark calculations. Also refer to chapter 11 of the doc Computer
Efficiency and Performance which details the algorithm for calculating
efficiency used by the native benchmark.

What is relevant for the design is that each worklet must output a performance
metric at the completion of the worklet. This metric can be a value that
increases with improved performance (e.g. frames per second, operations per
second) or that decreases with improved performance (e.g. total time to complete
an operation). This value is then combined with average power to form an
efficiency score for that worklet.

The performance metric generated must be consistent with multiple executions on
the same DUT. Benchmarks can be configured to run multiple times until a target
standard deviation is satisfied. Factors that could be an influence on the
performance value generated should be eliminated where possible, of the impact
reduced by repeating the workload multiple times.

The geometric mean of the worklet efficiency scores can then be used to
calculate the overall power efficiency score of the device under test.


[1]: https://gtd-gmbh.de/assets/img/pceet/GTD-PCEEI-Webinar-2022-09-19-presentation.pdf
[2]: https://gtd-gmbh.de/assets/img/pceet/White_Paper_on_the_Definition_of_Efficiency_Metrics_for_Computers_TR-PCEEI-Metrics.pdf