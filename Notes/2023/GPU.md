# GPUs

1. Cuda: is a parallel computing platform and application programming interface (API) that allows software developers to use a CUDA-enabled graphics processing unit (GPU) for general-purpose processing. CUDA operates at the software level, providing a framework for writing parallel programs that run on NVIDIA GPUs.
2. Nvlink: NVLink is a wire-based communications protocol for high-bandwidth, low-latency data transfer between GPUs, and between GPUs and CPUs. NVLink operates at the hardware level, as it's a physical connection that replaces the older PCI Express (PCIe) standards for connecting multiple GPUs.
3. Different Cores:
    - Cuda Cores: General Computing, the more the better,
    - Tensor Cores: special for ML, only DC Cards have
    - RT Cores: Ray Tracing, for gaming
    - NVENC/NVDEC Cores: video encoding and decoding
  
4. PCIe vs SXM: PCIe for normal desktop, SXM(Socketed Multi-Chip Module), for data center, high bandwidth, low latency between multiple GPUs, liquid cooling. often paired with NVLink. 
