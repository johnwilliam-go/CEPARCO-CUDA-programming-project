# CEPARCO-CUDA-programming-project
Google Colab link: https://colab.research.google.com/drive/1kj7JaL9r50vGm4epSSrF_PN9ZVov-DSn?usp=sharing

## 0.) Group members, project specifications, AI usage declaration
## i.) Screenshot of the program output with correctness check AND execution time for all cases

### a. C version
1. Array size = 2^24
<img width="694" height="83" alt="image" src="https://github.com/user-attachments/assets/63a4beaa-3eca-4b78-a251-169641dbbb52" />
2. Array size = 2^26
<img width="684" height="74" alt="image" src="https://github.com/user-attachments/assets/af8fe150-2755-4aa6-995c-5db858cc2bfa" />

3. Array size = 2^28
<!-- paste screenshot here -->

### b. CUDA Variant 2: Grid-stride loop, no prefetch, no mem advise (CUDA Unified)
1. Array size = 2^24
   - Block size = 256
   <img width="430" height="53" alt="image" src="https://github.com/user-attachments/assets/6790ec34-359e-4dd8-b58d-de5571638854" />

   - Block size = 512
<img width="430" height="56" alt="image" src="https://github.com/user-attachments/assets/dc06b748-5cbb-465d-84f4-87be0910dd6b" />

   - Block size = 1024
<img width="436" height="57" alt="image" src="https://github.com/user-attachments/assets/54d9d73d-a757-4861-ad9c-4f40f663496d" />

2. Array size = 2^26
   - Block size = 256
<img width="442" height="55" alt="image" src="https://github.com/user-attachments/assets/5649b340-ef72-482a-89ff-c830f3da6bb4" />

   - Block size = 512
<img width="437" height="55" alt="image" src="https://github.com/user-attachments/assets/db51e746-ee5d-4fc5-9c43-d11a56f5c354" />

   - Block size = 1024
<img width="439" height="53" alt="image" src="https://github.com/user-attachments/assets/f93e9b64-cfc8-4358-8be2-95f915c397be" />

3. Array size = 2^28
   - Block size = 256
<img width="436" height="52" alt="image" src="https://github.com/user-attachments/assets/8f2b80ca-5b61-4a89-ae32-dd5c1456037a" />

   - Block size = 512
<img width="431" height="55" alt="image" src="https://github.com/user-attachments/assets/4f7d26cd-10da-474a-8d0d-6a82b10336ef" />

   - Block size = 1024
<img width="434" height="53" alt="image" src="https://github.com/user-attachments/assets/166fbdf7-1cb3-4329-957b-9e2eb7fc36a7" />


### c. CUDA Variant 3: Grid-stride loop, with prefetch, no page creation, no mem advise
1. Array size = 2^24
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->
2. Array size = 2^26
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->
3. Array size = 2^28
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->

### d. CUDA Variant 4: Grid-stride loop, with prefetch, with page creation, no mem advise
1. Array size = 2^24
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->
2. Array size = 2^26
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->
3. Array size = 2^28
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->

### e. CUDA Variant 5: Grid-stride loop, with prefetch, with page creation, with mem advise
1. Array size = 2^24
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->
2. Array size = 2^26
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->
3. Array size = 2^28
   - Block size = 256
   <!-- paste screenshot here -->
   - Block size = 512
   <!-- paste screenshot here -->
   - Block size = 1024
   <!-- paste screenshot here -->
## ii.) Screenshot of nsys for all CUDA variants

Profiled with the same configuration for every variant (array size = 2^24, block size = 256).

### a. Variant 2 - CUDA Unified (no prefetch, no mem advise)
<img width="1320" height="613" alt="image" src="https://github.com/user-attachments/assets/33985fec-5481-4d32-a750-6b0941958761" />


### b. Variant 3 - CUDA Prefetch (no page creation, no mem advise)
<img width="1284" height="627" alt="image" src="https://github.com/user-attachments/assets/b5bc9614-c700-4a61-b1a2-4b644691310b" />


### c. Variant 4 - CUDA Prefetch + Page Creation (no mem advise)
<img width="1319" height="661" alt="image" src="https://github.com/user-attachments/assets/73b4a73e-f5c5-4a13-ba2c-edf6cf870191" />


### d. Variant 5 - CUDA Prefetch + Page Creation + Mem Advise
<img width="975" height="481" alt="image" src="https://github.com/user-attachments/assets/93b7ddde-eeca-4807-8f84-7b39df8bb8c0" />


## iii.) Comparative table of execution time (C, CUDA variants, x86-64, XMM, YMM)
### 2^24 elements (16,777,216)

| Implementation | CUDA Block Size | Avg (ms) | Min (ms) | Max (ms) | Speedup |
|---|:---:|---:|---:|---:|---:|
| C (Baseline) | N/A | 60.625244 | 56.303079 | 117.028668 | 1.00x |
| CUDA Unified | 256 | 4.145169 | 1.019616 | 94.365471 | 14.63x |
| CUDA Unified | 512 | 4.560891 | 1.016256 | 107.089500 | 13.29x |
| CUDA Unified | 1024 | 2.936491 | 1.026016 | 58.173504 | 20.65x |
| CUDA Prefetch | 256 | 1.023716 | 1.011200 | 1.137984 | 59.22x |
| CUDA Prefetch | 512 | 1.018745 | 1.004896 | 1.046272 | 59.51x |
| CUDA Prefetch | 1024 | 1.044943 | 1.033856 | 1.079968 | 58.02x |
| CUDA Prefetch + Page Creation | 256 | 1.022852 | 1.013280 | 1.125760 | 59.27x |
| CUDA Prefetch + Page Creation | 512 | 1.037619 | 1.027264 | 1.061184 | 58.43x |
| CUDA Prefetch + Page Creation | 1024 | 1.251183 | 1.245376 | 1.267488 | 48.45x |
| CUDA Prefetch + Page Creation + MemAdvise | 256 | 1.026281 | 1.014336 | 1.153984 | 59.07x |
| CUDA Prefetch + Page Creation + MemAdvise | 512 | 1.049524 | 1.035648 | 1.083328 | 57.76x |
| CUDA Prefetch + Page Creation + MemAdvise | 1024 | 1.257167 | 1.243520 | 1.440064 | 48.22x |

### 2^26 elements (67,108,864)

| Implementation | CUDA Block Size | Avg (ms) | Min (ms) | Max (ms) | Speedup |
|---|:---:|---:|---:|---:|---:|
| C (Baseline) | N/A | 272.392262 | 223.871918 | 459.954206 | 1.00x |
| CUDA Unified | 256 | 11.603806 | 4.075456 | 229.627106 | 23.47x |
| CUDA Unified | 512 | 11.153206 | 4.077024 | 215.917511 | 24.42x |
| CUDA Unified | 1024 | 15.851581 | 4.108928 | 356.220856 | 17.18x |
| CUDA Prefetch | 256 | 4.058710 | 4.038976 | 4.082336 | 67.11x |
| CUDA Prefetch | 512 | 4.086373 | 4.070272 | 4.120896 | 66.66x |
| CUDA Prefetch | 1024 | 4.109995 | 4.097984 | 4.141536 | 66.28x |
| CUDA Prefetch + Page Creation | 256 | 4.054480 | 4.047680 | 4.080384 | 67.18x |
| CUDA Prefetch + Page Creation | 512 | 4.075839 | 4.063360 | 4.107040 | 66.83x |
| CUDA Prefetch + Page Creation | 1024 | 4.108581 | 4.093152 | 4.142144 | 66.30x |
| CUDA Prefetch + Page Creation + MemAdvise | 256 | 4.060057 | 4.049664 | 4.086496 | 67.09x |
| CUDA Prefetch + Page Creation + MemAdvise | 512 | 4.076357 | 4.064288 | 4.104704 | 66.82x |
| CUDA Prefetch + Page Creation + MemAdvise | 1024 | 4.907161 | 4.885376 | 4.945760 | 55.51x |

### 2^28 elements (268,435,456)

| Implementation | CUDA Block Size | Avg (ms) | Min (ms) | Max (ms) | Speedup |
|---|:---:|---:|---:|---:|---:|
| C (Baseline) | N/A | 1050.427821 | 896.794912 | 1931.207315 | 1.00x |
| CUDA Unified | 256 | 48.173068 | 16.254593 | 973.001831 | 21.81x |
| CUDA Unified | 512 | 65.560450 | 16.279585 | 1494.225220 | 16.02x |
| CUDA Unified | 1024 | 46.075185 | 16.365313 | 907.032410 | 22.80x |
| CUDA Prefetch | 256 | 16.351541 | 16.242912 | 16.381439 | 64.24x |
| CUDA Prefetch | 512 | 16.268822 | 16.251968 | 16.354656 | 64.57x |
| CUDA Prefetch | 1024 | 16.415888 | 16.342112 | 18.172352 | 63.99x |
| CUDA Prefetch + Page Creation | 256 | 16.333385 | 16.025761 | 16.384895 | 64.31x |
| CUDA Prefetch + Page Creation | 512 | 16.257561 | 16.236671 | 16.473152 | 64.61x |
| CUDA Prefetch + Page Creation | 1024 | 16.353796 | 16.338177 | 16.385376 | 64.23x |
| CUDA Prefetch + Page Creation + MemAdvise | 256 | 16.356226 | 16.240864 | 16.377760 | 64.22x |
| CUDA Prefetch + Page Creation + MemAdvise | 512 | 16.258186 | 16.091648 | 16.291168 | 64.61x |
| CUDA Prefetch + Page Creation + MemAdvise | 1024 | 16.361675 | 16.348640 | 16.392736 | 64.20x |
## iv.) Analysis of results
            -Analysis of kernel execution time.  
           - Analysis of speed performance across all platforms
--Guide questions for analysis (for all CUDA variants).  This is not comprehensive; add more analysis as necessary --
a.) How does block size affect execution time (observing various elements and using max blocks)?  Which block size will you recommend?
b) Is prefetching always recommended, or should CUDA manage memory?  Give some use cases in which one is better than the other.
c.) Between SIMD and SIMT, which one is faster? Give some use cases in which one is better than the other.

## v.) Discussion the problems encountered and solutions made, unique methodology used, AHA moments, etc.
## vi.) Discuss, based on your experience on the particular project use case, the differences between SIMD and SIMT in handling parallelism.  Include also the PROS and CONS of using SIMD and SIMT in your use case.
