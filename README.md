#  Cache Performance Optimization 

##  Introduction  

This project focuses on **enhancing memory subsystem performance** using **advanced prefetching techniques**. The aim is to:  

- Reduce cache and TLB misses  
- Improve **L1-D cache MPKI**  
- Increase **IPC (Instructions Per Cycle)**  
- Implement adaptive prefetching policies in the **ChampSim simulator**  

###  Objectives  
- Implement **TLB and Data Prefetchers** in ChampSim  
- Explore **Arbitrary Stride Prefetching (ASP)** for STLB, IP-stride, complex stride, and next-line prefetchers  
- Develop an **adaptive prefetching mechanism** to dynamically select the best prefetcher  
- Evaluate performance across multiple traces and report:  
  - Speedup  
  - L1-D MPKI  

---

## 🔭 Project Scope  

The project is divided into **four tasks**:  

1. **TLB Prefetching** → Implement ASP for STLB to reduce TLB misses  
2. **Data Prefetching** → Implement IP-stride & complex stride prefetchers for L1-D cache  
3. **Adaptive Prefetching** → Develop a dynamic mechanism that chooses the most effective prefetcher per workload  
4. **Bonus Task** → Optimize performance by combining **data + TLB prefetchers**  

---

## ⚙️ System Design & Implementation  

### TLB Prefetching – Arbitrary Stride Prefetcher (ASP)  
- Uses **PC-based indexing** with a **Reference Prediction Table (RPT)**  
- Tracks last address, stride, and state per instruction  
- Initiates prefetch when stride is stable over consecutive accesses  
- Integrated into **STLB** in ChampSim  

 **Metrics Collected:**  
- STLB MPKI  
- IPC  
- Speedup vs. baseline  

---

###  Data Prefetchers  
- **IP-Stride Prefetcher** → Detects constant stride patterns and prefetches future addresses  
- **Complex Stride Prefetcher** → Handles non-constant patterns (e.g., alternating strides)  
- Prefetching restricted within **page boundaries** for correctness  

**Metrics Collected:**  
- L1-D MPKI (Total & Load)  
- IPC  
- Speedup vs. baseline  

---

### Adaptive Prefetcher – *Guldasta-e-Prefetcher* 🌸  
- Combines **IP-stride, complex stride, and next-line prefetchers**  
- Measures **prefetch accuracy** during a fixed **PHASE_LENGTH** after warmup  
- Dynamically selects the most accurate prefetcher  
- Maintains a **consistent prefetch degree** across all strategies  

**Metrics Collected:**  
- Speedup across all traces  
- L1-D MPKI for baseline, individual prefetchers, and optimized combination  

---

### Bonus Task – TLB + Data Prefetcher Optimization  
- Enabled **both TLB and data prefetchers** simultaneously  
- Applied **throttling** to reduce unnecessary memory traffic  
- Achieved overall **performance improvement** with controlled cache overhead  

---

## Programs Implemented  

| Program                  | Functionality                                      |
|---------------------------|---------------------------------------------------|
| `asp.stlb_pref`           | Arbitrary Stride TLB Prefetcher                   |
| `ip_stride.l1d_pref`      | IP-stride L1-D Cache Prefetcher                   |
| `complex_stride.l1d_pref` | Complex Stride L1-D Cache Prefetcher              |
| `next_line.l1d_pref`      | Next-line L1-D Cache Prefetcher                   |
| `optimized.l1d_pref`      | Adaptive combination of multiple prefetchers      |
| `task4_pref` *(Bonus)*    | Combined **Data + TLB Prefetcher** with throttling |

---

## Tools & Environment  

- **Simulator:** ChampSim  
- **Language:** C++  
- **Compiler:** GCC 7.5.0  
- **Hardware:** Intel/AMD x86 machine  
- **Benchmarks:** Provided trace files (`trace1`, `trace2`, `trace3`)  
- **Metrics Used:**  
  - IPC  
  - L1-D MPKI  
  - STLB MPKI  
  - Speedup  

---


## 🚀 How to Run  

1. Clone the repository  
   ```bash
   git clone https://github.com/hirusaam/Cache-Performance-Optimization-Advanced-Prefetching-Techniques-.git
   cd Cache-Performance-Optimization-Advanced-Prefetching-Techniques-
