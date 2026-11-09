# CEPARCO-CUDA-programming-project
Google Colab link: https://colab.research.google.com/drive/1kj7JaL9r50vGm4epSSrF_PN9ZVov-DSn?usp=sharing

## 0.) Group members, project specifications, AI usage declaration
### a. Group members
GO, JOHN WILLIAM <br>
PLACER, PAUL JOHN <br>
ESPERANZA, MJ AJEGRAM <br>
OBAR, DAVID ANGELO <br>

### b. project specifications
#### Vector triad operation

**Input:**
- Scalar variable `n` (integer) containing the length of the vectors.
- Vectors `B`, `C`, and `D` containing single-precision floating-point values.

**Process:**

For each element:

    A[i] = B[i] + C[i] * D[i];

**Output:**
- Store the computed results in vector `A`.

#### Test Configurations

- **Vector Sizes:** `2^20`, `2^26`, and `2^28`
- **CUDA Block Sizes:** `256`, `512`, and `1024` threads per block.

#### Vector Initialization

The input vectors were initialized using the following method:

    #define SEED 0.000001

    for (size_t i = 0; i < ARRAY_SIZE; i++) {
        b[i] = i * SEED;
        c[i] = i * SEED * 2.0;
        d[i] = i * SEED * 3.0;
    }
#### c. AI usage declaration
AI was solely used for assistance in understanding the CUDA concepts and its implementation, as well as grammar and format checking for the README section.

## i.) Screenshot of the program output with correctness check AND execution time for all cases

### a. C version

<img width="699" height="263" alt="image" src="https://github.com/user-attachments/assets/d48e00fb-35ea-4467-9b62-0e6a84c60ad6" />

---

### b. CUDA Variant 2: Grid-stride loop, no prefetch, no mem advise (CUDA Unified)

#### Array size = 2^20

<img width="587" height="251" alt="image" src="https://github.com/user-attachments/assets/0f16f6b3-c078-46dd-bde5-968c7715680e" />

#### Array size = 2^26

<img width="595" height="252" alt="image" src="https://github.com/user-attachments/assets/dcca81b8-2c9d-4fce-bc8b-af0985ee21fe" />

#### Array size = 2^28

<img width="587" height="251" alt="image" src="https://github.com/user-attachments/assets/5193a82d-59b6-42ce-a81a-48bb1f2b7bba" />

---

### c. CUDA Variant 3: Grid-stride loop, with prefetch, no page creation, no mem advise

#### Array size = 2^20

<img width="554" height="199" alt="image" src="https://github.com/user-attachments/assets/4c7ea1f0-3a1e-4db9-93d4-fa596be65339" />

#### Array size = 2^26

<img width="555" height="200" alt="image" src="https://github.com/user-attachments/assets/b5cad6d4-1016-4fb1-a42b-7fcea8be27d1" />

#### Array size = 2^28

<img width="572" height="201" alt="image" src="https://github.com/user-attachments/assets/259b76e2-ac23-4a85-9597-4c7785519e64" />

---

### d. CUDA Variant 4: Grid-stride loop, with prefetch, with page creation, no mem advise

#### Array size = 2^20

<img width="555" height="197" alt="image" src="https://github.com/user-attachments/assets/2995cee2-71ea-4e14-85e6-c0c040a8d383" />

#### Array size = 2^26

<img width="561" height="200" alt="image" src="https://github.com/user-attachments/assets/c3dfcea8-3f99-4bc7-8106-e8e35477471d" />

#### Array size = 2^28

<img width="576" height="202" alt="image" src="https://github.com/user-attachments/assets/87acbdfc-a441-4b7a-b934-cc1ffe1ee25c" />

---

### e. CUDA Variant 5: Grid-stride loop, with prefetch, with page creation, with mem advise

#### Array size = 2^20

<img width="557" height="198" alt="image" src="https://github.com/user-attachments/assets/3a2d9073-7067-47a2-80fe-f8e16b6b081f" />

#### Array size = 2^26

<img width="551" height="202" alt="image" src="https://github.com/user-attachments/assets/a1185f46-a4e8-46bb-9a07-8a98b4f522b4" />

#### Array size = 2^28

<img width="578" height="207" alt="image" src="https://github.com/user-attachments/assets/a11448bb-14f2-4d85-9dbc-d03238329d02" />

## ii.) Screenshot of nsys for all CUDA variants

Profiled with the same configuration for every variant (array size = 2^20, block size = 256).

### a. Variant 2 - CUDA Unified (no prefetch, no mem advise)

<img width="1050" height="487" alt="image" src="https://github.com/user-attachments/assets/d5c26d91-0147-4f30-ba36-3e35646d2269" />

### b. Variant 3 - CUDA Prefetch (no page creation, no mem advise)

<img width="1008" height="498" alt="image" src="https://github.com/user-attachments/assets/e7d06426-705e-4f41-889f-512b8650a1db" />


### c. Variant 4 - CUDA Prefetch + Page Creation (no mem advise)
<img width="1007" height="521" alt="image" src="https://github.com/user-attachments/assets/ec1110bf-aa68-46db-a8d2-bd0ff9b5a327" />



### d. Variant 5 - CUDA Prefetch + Page Creation + Mem Advise
<img width="1010" height="516" alt="image" src="https://github.com/user-attachments/assets/0c4cc42e-fa4e-422e-8697-e031d59aa543" />


## iii.) Comparative table of execution time (C, CUDA variants, x86-64, XMM, YMM)
*Note that the x86-64 implementations were ran in a different machine because they could not be run in the Colab Notebook, so their times are not listed. Their speedups are compared against optimized C (Release Mode in Visual Studio), whose runtimes are 0.58ms, 38.56ms, and 170.69ms for 2^20, 2^26, and 2^28 respectively.

### 2^20 elements (1,048,576)
| Implementation | CUDA Block Size | Avg (ms) | Min (ms) | Max (ms) | Speedup |
|---|:---:|---:|---:|---:|---:|
| C (Baseline) | N/A | 3.443607 | 3.084901 | 7.700419 | 1.00x |
| x86-64  | N/A | 0.61* | - | - |  |
| x86-64 XMM | N/A | 0.55* | - | - |  |
| x86-64 YMM | N/A | 0.55* | - | - |  |
| CUDA Unified | 256 | 
| CUDA Unified | 512 | 
| CUDA Unified | 1024 | 
| CUDA Prefetch | 256 | 
| CUDA Prefetch | 512 | 
| CUDA Prefetch | 1024 | 
| CUDA Prefetch + Page Creation | 256 |
| CUDA Prefetch + Page Creation | 512 |
| CUDA Prefetch + Page Creation | 1024 |
| CUDA Prefetch + Page Creation + MemAdvise | 256 |
| CUDA Prefetch + Page Creation + MemAdvise | 512 |
| CUDA Prefetch + Page Creation + MemAdvise | 1024 |

### 2^26 elements (67,108,864)

| Implementation | CUDA Block Size | Avg (ms) | Min (ms) | Max (ms) | Speedup |
|---|:---:|---:|---:|---:|---:|
| C (Baseline) | N/A | 272.392262 | 223.871918 | 459.954206 | 1.00x |
| x86-64  | N/A | 39.34 |  | - |  |
| x86-64 XMM | N/A | 38.42 |  | - |  |
| x86-64 YMM | N/A | 38.80 |  | - |  |
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
| x86-64  | N/A | 191.29* | - | - |  |
| x86-64 XMM | N/A | 169.32* | - | - |  |
| x86-64 YMM | N/A | 168.77* | - | - |  |
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

## v.) Discussion of problems encountered and solutions made, unique methodology used, AHA moments, etc.

### a. Problems encountered and solutions

**1. Large gap between average and minimum time in Variant 2 (CUDA Unified)**

At 2^20 and block size 256, the minimum was 1.02 ms but the average was 4.15 ms and the maximum 94.4 ms. The first launch was slow because managed pages had to migrate from host to GPU through on-demand page faults. Solution: We reported min/avg/max together, and Variants 3 to 5 used cudaMemPrefetchAsync to move the data before the timed kernel.

**2. Fair comparison across variants**

We used the same initialization, sizes, block sizes, and timing method for every variant, and profiled all of them with nsys at 2^20 and block size 256.

**3. Correctness checking at 2^28**

Each array is 1 GiB, so we checked results element by element against the formula instead of keeping duplicate copies.

### b. Unique methodology

We built the CUDA code as four incremental variants (Unified → Prefetch → Page Creation → MemAdvise). Each variant changes one feature, so any timing difference can be traced to that feature. nsys traces were used to explain each result.

### c. AHA moments

- **The kernel is memory-bound.** Prefetch times scale linearly with array size (~1.02, ~4.05, and ~16.3 ms), which works out to about 263 GB/s at every size. The single multiply-add barely matters.
- **The Unified slowdown is page migration, not computation.** The steady-state minimums for Unified and Prefetch are nearly identical (1.02 ms vs. 1.01 ms at 2^20).
- **More features did not mean more speed.** Page creation and MemAdvise gave no gain over plain prefetch, since the data is touched only once by a single GPU.
- **Block size 1024 was sometimes slower** (e.g., 1.25 ms vs. 1.02 ms at 2^20 with page creation). We did not profile this directly, so the cause is a hypothesis.
- **The 60× to 67× speedup is against single-threaded C**, so it would shrink against a multithreaded or SIMD CPU version.

## vi.) SIMD vs. SIMT in handling parallelism: our use case

### a. How each handles parallelism

| | SIMD (x86-64 XMM/YMM) | SIMT (CUDA) |
|---|---|---|
| **Model** | One CPU thread applies one instruction to a packed register (4 floats for XMM, 8 for YMM). | Thousands of threads run the same scalar code, grouped in warps of 32. |
| **Programmer's job** | Manage vector width, alignment, and leftover elements. | Write the code for one element; the grid-stride loop handles any array size. |
| **Scaling** | Limited by register width and CPU core count. | Scales with the number of threads; the GPU hides memory latency by switching warps. |

### b. Which was faster?

SIMT was clearly faster. At 2^28 elements, the C baseline took ~1050 ms while the best CUDA runs took ~16.3 ms (~64×). The triad is bandwidth-bound, so GPU memory bandwidth matters more than wider CPU registers.

### c. Pros and cons

| | Pros | Cons |
|---|---|---|
| **SIMD** | No data transfer; low overhead; good for small arrays; compilers can auto-vectorize the triad | Fixed width (4 or 8); alignment and remainder handling; tied to SSE/AVX; limited by CPU memory bandwidth |
| **SIMT** | Massive parallelism and bandwidth (58× to 67× in our best cases); simple scalar-style code; grid-stride loops handle any size | Needs memory management; page faults cost up to ~94 ms without prefetch; poor for small inputs; needs a GPU |

### d. Use cases

- **SIMD is better** for small arrays already in CPU memory and for latency-sensitive code.
- **SIMT is better** for very large, independent-element workloads like our 2^26 and 2^28 cases, especially when data stays on the GPU across multiple kernels.
