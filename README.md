# BeyondMoore
## _Pioneering the Future of Post-Moore Computing_

**BeyondMoore** addresses the timely research challenge of solving the software side of the Post Moore crisis, as Moore's Law reaches its limits in chip manufacturing. This transition requires a shift towards extreme heterogeneity in computing systems. Current programming solutions are host-centric, leading to scalability issues and limited parallelism. BeyondMoore proposes an autonomous execution model where accelerators operate independently, facilitated by a task graph programming abstraction. To efficiently execute this task graph, BeyondMoore develops a software framework that performs static and dynamic optimizations, issues accelerator-initiated data transfers along with supporting tools such as compiler and profiler. Below you can find details of projects comprising BeyondMoore’s software ecosystem. 


## BeyondMoore Software Ecosystem

* [CPU-Free Execution Model](#CPU-Free-Model): A Fully Autonomous Execution Model for Multi-GPU Applications 
* [CPU-Free Task Graph](https://github.com/msasongko17/multigpu_callback): CPU-Free Task Graph Execution using CUDA Graphs
* [CPU-Free Compiler](#CPU-Free-Model-Compiler): Compiler for Generating CPU-Free Multi-GPU code
* [Multi-GPU Callbacks](#Multi-GPU-Callbacks): GPU to CPU Callback Mechanisms
  
_Tools_
* [Snoopie](#Snoopie): A Multi-GPU Communication Profiler and Visualiser
* [PES](#Precise-Event-Sampling): A Precise Event Sampling Benchmark Suite
  
### CPU Free Model

This project proposes a fully autonomous execution model for multiGPU applications that completely excludes the
involvement of the CPU beyond the initial kernel launch. In a typical multi-GPU application, the host serves as the
orchestrator of execution by directly launching kernels, issuing communication calls, and acting as a synchronizer for
devices. We argue that this orchestration, or control flow path, causes undue overhead and can be delegated entirely to
devices to improve performance in applications that require communication among peers. For the proposed CPU-free
execution model, we leverage existing techniques such as persistent kernels, thread block specialization, device-side
barriers, and device-initiated communication routines to write fully autonomous multi-GPU code and achieve significantly
reduced communication overheads. We demonstrate our proposed model on two broadly used iterative solvers, 2D/3D Jacobi
stencil and Conjugate Gradient(CG). Compared to the CPU-controlled baselines, the CPU-free model can improve 3D stencil
communication latency by 58.8% and provide a 1.63x speedup for CG on 8 NVIDIA A100 GPUs. The project code is available
[here](https://github.com/ParCoreLab/CPU-Free-model).

### Snoopie

With data movement becoming one of the most expensive bottlenecks in computing, the need for profiling tools to analyze
communication becomes crucial for effectively scaling multi-GPU applications. While existing profiling tools including
first-party software by GPU vendors are robust and excel at capturing compute operations within a single GPU, support
for monitoring GPU-GPU data transfers and calls issued by communication libraries is currently inadequate. To fill these
gaps, we introduce [Snoopie](https://github.com/parcorelab/snoopie), an instrumentation-based multi-GPU
communication profiling tool built on NVBit, capable of tracking peer-to-peer transfers and GPU-centric
communication library calls. To increase programmer productivity, [Snoopie](https://github.com/parcorelab/snoopie)
can attribute data movement to the source code line and the data objects involved. It comes with multiple
visualization modes at varying granularities, from a coarse view of the data movement in the system as a whole to
specific instructions and addresses. Our case studies demonstrate [Snoopie](https://github.com/parcorelab/snoopie)’s
effectiveness in monitoring data movement, locating performance bugs in applications, and understanding concrete
data transfers abstracted beneath communication libraries. The tool is publicly available
[here](https://github.com/ParCoreLab/snoopie).


### CPU Free Model Compiler

As a follow up to the CPU Free Model presented earlier. This project works on incoperating the CPU Free Model as a
Compiler Optimisation such that higher level GPU Code can benifit from the CPU Free Model allowing for improved
performance when compared to the previous generated applications. The project code is available
[here](https://github.com/ParCoreLab/CPU-Free-Model-Compiler).

### Muli-GPU Call-backs

GPU kernels may suffer from resource underutilization in multi-GPU systems due to insufficient workload to saturate
devices when incorporated within an irregular application. To better utilize the resources in multi-GPU systems, we
propose a GPU-sided resource allocation method that can increase or decrease the number of GPUs in use as the workload
changes over time. Our method employs GPU-to-CPU callbacks to allow GPU device(s) to request additional devices while
the kernel execution is in flight. We implemented and tested multiple callback methods required for GPU-initiated
workload offloading to other devices and measured their overheads on Nvidia and AMD platforms. To showcase the usage of
callbacks in irregular applications, we implemented Breadth-First Search (BFS) that uses device-initiated workload
offloading. Apart from allowing dynamic device allocation in persistently running kernels, it reduces time to solution
on average by 15.7% at the cost of callback overheads with a minimum of 6.50 microseconds on AMD and 4.83 microseconds
on Nvidia, depending on the chosen callback mechanism. Moreover, the proposed model can reduce the total device usage by
up to 35%, which is associated with higher energy efficiency. Part of the project code is available [here](https://github.com/msasongko17/multigpu_callback).

### Ilyas's CUDA Graph Work

(To Be Added)


---

> [!NOTE]
> This project has received funding from the European Research Council (ERC) under the European Union’s Horizon 2020 research and innovation programme (grant agreement No 949587).

<img alt="ERC Logo" src="https://raw.githubusercontent.com/ParCoreLab/BeyondMoore/main/assets/erc_logo-150x150.png" width="75px">
