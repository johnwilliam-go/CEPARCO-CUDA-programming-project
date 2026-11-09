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
| x86-64  | N/A | 0.61* | - | - | 0.95x |
| x86-64 XMM | N/A | 0.55* | - | - | 1.05x |
| x86-64 YMM | N/A | 0.55* | - | - | 1.05x |
| CUDA Unified | 256 | 0.206064 | 0.070720 | 4.045760 | 16.71x |
| CUDA Unified | 512 | 0.195509 | 0.072736 | 3.678656 | 17.61x |
| CUDA Unified | 1024 | 0.205222 | 0.082624 | 3.662976 | 16.78x |
| CUDA Prefetch | 256 | 0.078063 | 0.072992 | 0.179200 | 44.11x |
| CUDA Prefetch | 512 | 0.078503 | 0.069248 | 0.097824 | 43.87x |
| CUDA Prefetch | 1024 | 0.086290 | 0.078432 | 0.102112 | 39.91x |
| CUDA Prefetch + Page Creation | 256 | 0.077754 | 0.071872 | 0.172000 | 44.29x |
| CUDA Prefetch + Page Creation | 512 | 0.075431 | 0.069760 | 0.096960 | 45.65x |
| CUDA Prefetch + Page Creation | 1024 | 0.086507 | 0.081248 | 0.100384 | 39.81x |
| CUDA Prefetch + Page Creation + MemAdvise | 256 | 0.078592 | 0.070752 | 0.157280 | 43.82x |
| CUDA Prefetch + Page Creation + MemAdvise | 512 | 0.072035 | 0.065056 | 0.084960 | 47.80x |
| CUDA Prefetch + Page Creation + MemAdvise | 1024 | 0.075698 | 0.068800 | 0.087680 | 45.49x |

### 2^26 elements (67,108,864)
| Implementation | CUDA Block Size | Avg (ms) | Min (ms) | Max (ms) | Speedup |
|---|:---:|---:|---:|---:|---:|
| C (Baseline) | N/A | 272.392262 | 223.871918 | 459.954206 | 1.00x |
| x86-64  | N/A | 39.34* | - | - | 0.98x |
| x86-64 XMM | N/A | 38.42* | - | - | 1.00x |
| x86-64 YMM | N/A | 38.80* | - | - | 0.99x |
| CUDA Unified | 256 | 13.139214 | 4.025728 | 276.571991 | 20.48x |
| CUDA Unified | 512 | 16.058554 | 4.087424 | 362.875336 | 16.76x |
| CUDA Unified | 1024 | 15.365106 | 4.104096 | 341.620117 | 17.51x |
| CUDA Prefetch | 256 | 4.069211 | 4.055008 | 4.093056 | 66.13x |
| CUDA Prefetch | 512 | 4.206043 | 4.188480 | 4.239552 | 63.98x |
| CUDA Prefetch | 1024 | 4.892018 | 4.876096 | 4.921728 | 55.01x |
| CUDA Prefetch + Page Creation | 256 | 4.068992 | 4.055936 | 4.100128 | 66.13x |
| CUDA Prefetch + Page Creation | 512 | 4.064311 | 4.053440 | 4.093760 | 66.21x |
| CUDA Prefetch + Page Creation | 1024 | 4.103267 | 4.090592 | 4.141216 | 65.58x |
| CUDA Prefetch + Page Creation + MemAdvise | 256 | 4.048066 | 3.999072 | 4.101792 | 66.47x |
| CUDA Prefetch + Page Creation + MemAdvise | 512 | 4.087780 | 4.071136 | 4.128864 | 65.83x |
| CUDA Prefetch + Page Creation + MemAdvise | 1024 | 4.103563 | 4.088672 | 4.139872 | 65.58x |

### 2^28 elements (268,435,456)
| Implementation | CUDA Block Size | Avg (ms) | Min (ms) | Max (ms) | Speedup |
|---|:---:|---:|---:|---:|---:|
| C (Baseline) | N/A | 1050.427821 | 896.794912 | 1931.207315 | 1.00x |
| x86-64  | N/A | 191.29* | - | - | 0.89x |
| x86-64 XMM | N/A | 169.32* | - | - | 1.01x |
| x86-64 YMM | N/A | 168.77* | - | - | 1.01x |
| CUDA Unified | 256 | 47.685760 | 16.243168 | 958.953674 | 21.55x |
| CUDA Unified | 512 | 62.024775 | 16.279167 | 1388.098267 | 16.56x |
| CUDA Unified | 1024 | 47.534587 | 16.365696 | 950.947876 | 21.61x |
| CUDA Prefetch | 256 | 16.369804 | 15.998656 | 16.427135 | 62.76x |
| CUDA Prefetch | 512 | 16.277559 | 16.254496 | 16.354496 | 63.12x |
| CUDA Prefetch | 1024 | 16.409190 | 16.343552 | 17.719681 | 62.61x |
| CUDA Prefetch + Page Creation | 256 | 16.386366 | 16.217760 | 16.445280 | 62.69x |
| CUDA Prefetch + Page Creation | 512 | 16.256304 | 16.247583 | 16.290976 | 63.20x |
| CUDA Prefetch + Page Creation | 1024 | 16.337347 | 16.247488 | 16.378592 | 62.88x |
| CUDA Prefetch + Page Creation + MemAdvise | 256 | 16.382229 | 15.984256 | 16.464449 | 62.71x |
| CUDA Prefetch + Page Creation + MemAdvise | 512 | 16.224760 | 16.160608 | 16.291168 | 63.32x |
| CUDA Prefetch + Page Creation + MemAdvise | 1024 | 16.315874 | 16.238144 | 16.357985 | 62.97x |

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

At 2^20 and block size 256, the minimum was 0.071 ms but the average was 0.206 ms and the maximum 4.05 ms. The first launch was slow because managed pages had to migrate from host to GPU through on-demand page faults. Solution: we reported min, avg and max together, and Variants 3 to 5 used `cudaMemPrefetchAsync` to move the data before the timed kernel.

**2. Fair comparison across variants**

We used the same initialization, sizes, block sizes and timing method for every variant, and profiled all of them with nsys at 2^20 and block size 256.

**3. Correctness checking at 2^28**

Each array is 1 GiB, so we checked results element by element against the formula instead of keeping duplicate copies.

### b. Unique methodology

We built the CUDA code as four incremental variants (Unified → Prefetch → Page Creation → MemAdvise). Each variant changes one feature, so any timing difference can be traced to that feature. nsys traces were used to explain each result.

### c. AHA moments

- **The kernel is memory-bound.** Prefetch times scale linearly with array size (about 4 ms at 2^26 and 16 ms at 2^28), which works out to about 250 to 263 GB/s. The single multiply-add barely matters.
- **The Unified slowdown is page migration, not computation.** The steady-state minimums for Unified and Prefetch are nearly identical (0.0707 vs 0.0730 ms at 2^20, 4.03 vs 4.06 ms at 2^26, 16.24 vs 16.00 ms at 2^28). Only the averages and maximums differ.
- **More features did not mean more speed.** At 2^26 and 2^28, Page Creation and MemAdvise gave no gain over plain Prefetch, since the data is touched only once by a single GPU.
- **Block size 1024 was sometimes slower, but not consistently.** For example, 4.89 ms vs 4.07 ms at 2^26 with plain Prefetch, and 0.086 ms vs 0.078 ms at 2^20. The slow row changed between runs, and at 2^28 all three block sizes tied at about 16.3 ms. We did not profile this directly, so we treat it as run-to-run variation.
- **The speedup is against single-threaded, unoptimized C.** The Prefetch variants were about 55x to 66x faster at 2^26 and about 63x at 2^28, and about 63x to 76x at 2^20. These would shrink against a multithreaded or SIMD CPU version.

---

## vi.) SIMD vs. SIMT in handling parallelism: our use case

### a. How each handles parallelism

| | SIMD (x86-64 XMM/YMM) | SIMT (CUDA) |
|---|---|---|
| **Model** | One CPU thread applies one instruction to a packed register (4 floats for XMM, 8 for YMM). | Thousands of threads run the same scalar code, grouped in warps of 32. |
| **Programmer's job** | Manage vector width, alignment, and leftover elements. | Write the code for one element; the grid-stride loop handles any array size. |
| **Scaling** | Limited by register width and CPU core count. | Scales with the number of threads; the GPU hides memory latency by switching warps. |

### b. Which was faster?

SIMT was clearly faster than our scalar C baseline. At 2^28 elements, the C baseline took about 1027 ms while the best CUDA runs took about 16 ms (about 63x). At 2^20 the best runs were about 70x faster. The triad is bandwidth-bound, so GPU memory bandwidth matters more than wider CPU registers.

### c. Pros and cons

| | Pros | Cons |
|---|---|---|
| **SIMD** | No data transfer; low overhead; good for small arrays; compilers can auto-vectorize the triad | Fixed width (4 or 8); alignment and remainder handling; tied to SSE/AVX; limited by CPU memory bandwidth |
| **SIMT** | Massive parallelism and bandwidth (about 63x to 66x over C at 2^26 and 2^28 in our best cases); simple scalar-style code; grid-stride loops handle any size | Needs memory management; worst runs reached about 1.4 s at 2^28; poor for small inputs; needs a GPU |

### d. Use cases

- **SIMD is better** for small arrays already in CPU memory and for latency-sensitive code.
- **SIMT is better** for very large, independent-element workloads like our 2^26 and 2^28 cases, especially when data stays on the GPU across multiple kernels.
