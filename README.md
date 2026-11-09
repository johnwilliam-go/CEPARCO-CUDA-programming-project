# CEPARCO-CUDA-programming-project
Google Colab link: https://colab.research.google.com/drive/1kj7JaL9r50vGm4epSSrF_PN9ZVov-DSn?usp=sharing

## 0.) Group members, project specifications, AI usage declaration
## i.) Sreenshot of the program output with correctness check AND execution time for all cases

## ii.) Screenshot of nsys for all CUDA variants
## iii.) Comparative table of execution time (C, CUDA variants, x86-64, XMM, YMM)
| Implementation | CUDA Block Size | Avg (ms) | Min (ms) | Max (ms) | Speedup |
|---|:---:|---:|---:|---:|---:|
| C (Baseline) | N/A | -- | -- | -- | 1.00x |
| x86-64 | N/A | -- | -- | -- | --x |
| x86-64 SIMD XMM | N/A | -- | -- | -- | --x |
| x86-64 SIMD YMM | N/A | -- | -- | -- | --x |
| CUDA Unified | 256 | -- | -- | -- | --x |
| CUDA Unified | 512 | -- | -- | -- | --x |
| CUDA Unified | 1024 | -- | -- | -- | --x |
| CUDA Prefetch | 256 | -- | -- | -- | --x |
| CUDA Prefetch | 512 | -- | -- | -- | --x |
| CUDA Prefetch | 1024 | -- | -- | -- | --x |
| CUDA Prefetch + Page Creation | 256 | -- | -- | -- | --x |
| CUDA Prefetch + Page Creation | 512 | -- | -- | -- | --x |
| CUDA Prefetch + Page Creation | 1024 | -- | -- | -- | --x |
| CUDA Prefetch + Page Creation + MemAdvise | 256 | -- | -- | -- | --x |
| CUDA Prefetch + Page Creation + MemAdvise | 512 | -- | -- | -- | --x |
| CUDA Prefetch + Page Creation + MemAdvise | 1024 | -- | -- | -- | --x |

## iv.) Analysis of results
            -Analysis of kernel execution time.  
           - Analysis of speed performance across all platforms
--Guide questions for analysis (for all CUDA variants).  This is not comprehensive; add more analysis as necessary --
a.) How does block size affect execution time (observing various elements and using max blocks)?  Which block size will you recommend?
b) Is prefetching always recommended, or should CUDA manage memory?  Give some use cases in which one is better than the other.
c.) Between SIMD and SIMT, which one is faster? Give some use cases in which one is better than the other.

## v.) Discussion the problems encountered and solutions made, unique methodology used, AHA moments, etc.
## vi.) Discuss, based on your experience on the particular project use case, the differences between SIMD and SIMT in handling parallelism.  Include also the PROS and CONS of using SIMD and SIMT in your use case.
