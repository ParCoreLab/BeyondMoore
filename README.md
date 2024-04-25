# BeyondMoore

<img alt="BeyondMoore Logo" src="https://raw.githubusercontent.com/ParCoreLab/BeyondMoore/main/assets/BeyondMoore-logo.png" width="250px">

## _Pioneering the Future of Computing_

**BeyondMoore** addresses the timely research challenge of solving the software side of the Post Moore crisis, as Moore's Law reaches its limits in chip manufacturing. This transition requires a shift towards extreme heterogeneity in computing systems. Current programming solutions are host-centric, leading to scalability issues and limited parallelism. BeyondMoore proposes an autonomous execution model where accelerators operate independently, facilitated by a task graph programming abstraction. To efficiently execute this task graph, BeyondMoore develops a software framework that performs static and dynamic optimizations, issues accelerator-initiated data transfers along with supporting tools such as compiler and profiler. Below you can find details of projects comprising BeyondMoore’s software ecosystem. 


## BeyondMoore Software Ecosystem

_Compiler, Runtime and Execution Models_
* [CPU-Free Execution Model](#CPU-Free-Model): a fully autonomous execution model for multi-GPU applications 
* [Multi-GPU Callbacks](#Multi-GPU-Callbacks): GPU to CPU callback mechanisms
* [CPU-Free Task Graph](#CPU-Free-Task-Graph): a lightweight runtime system tailored for CPU-free task graph execution
* [CPU-Free Compiler](#CPU-Free-Model-Compiler): compiler for generating CPU-Free multi-GPU code
* [Unified Communication Library](#Unified-Communication-Library): a unified communication library for device-to-device communication
  
_Profiling Tools_
* [Snoopie](#Snoopie): A Multi-GPU Communication Profiler and Visualiser
* [PES AMD vs Intel](#Precise-Event-Sampling): A Precise Event Sampling Benchmark Suite
  
### CPU-Free Model

This project introduces a fully autonomous execution model for multi-GPU applications, eliminating CPU involvement beyond initial kernel launch. In conventional setups, the CPU orchestrates execution, causing overhead. We propose delegating this control flow entirely to devices, leveraging techniques like persistent kernels and device-initiated communication. Our CPU-free model significantly reduces communication overhead. Demonstrations on 2D/3D Jacobi stencil and Conjugate Gradient solvers show up to a 58.8% improvement in communication latency and a 1.63x speedup for CG on 8 NVIDIA A100 GPUs compared to CPU-controlled baselines.

More details about the project [here](https://github.com/ParCoreLab/CPU-Free-model).

### Snoopie

With data movement posing a significant bottleneck in computing, profiling tools are essential for scaling multi-GPU applications efficiently. However, existing tools focus primarily on single GPU compute operations and lack support for monitoring GPU-GPU transfers and communication library calls. Addressing these gaps, we present Snoopie, an instrumentation-based multi-GPU communication profiling tool. Snoopie accurately tracks peer-to-peer transfers and GPU-centric communication library calls, attributing data movement to specific source code lines and objects. It offers various visualization modes, from system-wide overviews to detailed instructions and addresses, enhancing programmer productivity. 

The tool is publicly available [here](https://github.com/ParCoreLab/snoopie).

### Precise-Event Sampling

### Muli-GPU Callbacks

To address resource underutilization in multi-GPU systems, particularly in irregular applications, we propose a GPU-sided resource allocation method. This method dynamically adjusts the number of GPUs in use based on workload changes, utilizing GPU-to-CPU callbacks to request additional devices during kernel execution. We implemented and tested multiple callback methods, measuring their overheads on Nvidia and AMD platforms. Demonstrating the approach in an irregular application like Breadth-First Search (BFS), we achieved a 15.7% reduction in time to solution on average, with callback overheads as low as 6.50 microseconds on AMD and 4.83 microseconds on Nvidia. Additionally, the model can reduce total device usage by up to 35%, improving energy efficiency. 

The call back mechanisms used in project available [here](https://github.com/msasongko17/multigpu_callback).

### CPU-Free Task Graph

We've designed and implemented a lightweight runtime system tailored for CPU-free task graph execution in multi-device systems. Our runtime minimizes CPU involvement by handling task graph initialization exclusively, while executing all subsequent operations on the GPU side. This runtime system provides online scheduling of graph nodes, monitors GPU resource usage, manages memory allocation and data transfers, and synchronously tracks task dependencies. By accepting computational graphs as input, originally designed for single GPUs, it seamlessly scales to multiple GPUs without necessitating code modifications. 

More details about the project will be available soon. The related paper is under review.

### CPU-Free Model Compiler

We're actively crafting a compiler to empower developers to write high-level Python code that compiles into efficient CPU-free device code. This compiler integrates GPU-initiated communication libraries, NVSHMEM for NVIDIA and ROC_SHMEM for AMD, enabling GPU communication directly within Python code. With automatic generation of GPU-initiated communication calls and persistent kernels, we aim to streamline development workflows. Our prototype will be available soon. 

### Unified Communication Library

We're undertaking the design of an API for a unified communication library to streamline device-to-device communication within the CPU-free model by aiming to optimize communication efficiency across diverse devices. 

More details about the project will be available soon. The related paper is under preparation.

---

> [!NOTE]
> This project has received funding from the European Research Council (ERC) under the European Union’s Horizon 2020 research and innovation programme (grant agreement No 949587).

<img alt="ERC Logo" src="https://raw.githubusercontent.com/ParCoreLab/BeyondMoore/main/assets/erc_logo-150x150.png" width="75px">
