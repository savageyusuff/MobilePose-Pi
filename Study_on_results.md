1.0 ShufflenetV2: FPS is 1.09 and Model size is 5.3MB  
From [paper](https://arxiv.org/pdf/1807.11164.pdf), I will calculate estimated FPS.

Author's environment:
>ARM.
> A Qualcomm Snapdragon 810. We use a highly-optimized Neon-based
> implementation. A single thread is used for evaluation.
([ShuffleNet V2: Practical Guidelines for Efficient
CNN Architecture Design](https://arxiv.org/pdf/1807.11164.pdf) p.3)  

> 324~388.8GFLOPS  
(https://gpuflops.blogspot.com/2015/02/gpu-flops-list.html?m=1)  

my environment([source](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/))　:
>  A 900MHz quad-core ARM Cortex-A7 CPU  
>  1GB RAM

From our environment, we can estimate execution time.  
> pi@raspberrypi:~ $ lscpu  
> Architecture:          armv7l  
> Byte Order:            Little Endian  
> CPU(s):                4  
> On-line CPU(s) list:   0-3  
> Thread(s) per core:    1  
> Core(s) per socket:    4  
> Socket(s):             1  
> Model:                 4  
> Model name:            ARMv7 Processor rev 4 (v7l)  
> CPU max MHz:           624.0000  
> CPU min MHz:           600.0000  
> BogoMIPS:              38.40  
> Flags:                 half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32  

> Raspberry Pi 2 	Cortex-A7 	4.8 GFLOPS 	0.6GHz 	4 	8 	NEON: 2(mad) x1(simd) x4(core) x0.6(clock) = 4.8 GFLOPS  
(I referred here https://dench.flatlib.jp/opengl/cpuflops to derive estimation.)  

24.4x(4.8GFLOPS/324GFLOPS)=0.36  

Therefore, the estimated FPS is 0.36.  
This is just a third of actual FPS(1.09).  
I will continue to investigate to know the reason.  
