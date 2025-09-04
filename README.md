
# 🖥️ Memory Management Simulations

This repository contains Python scripts that simulate **classic memory management techniques** used in Operating Systems:

1. **Relocation with Base & Limit Registers**  
2. **Segmentation (two-segment model)**  

These scripts generate virtual address traces and demonstrate how addresses are translated into physical addresses (or raise segmentation violations).  

---

## 📂 Files
```

Memory-Management-Simulations/
│
├── relocation.py     # Simulates relocation with base & limit registers
├── segmentation.py   # Simulates segmentation with two segments

````

---

## 🚀 Usage

### 1️⃣ Relocation Simulation (`relocation.py`)
Relocation uses **base and limit registers** to map a virtual address to a physical address.

#### Example:
```bash
python relocation.py -s 1 -a 1k -p 16k -n 5 -c
````

#### Options:

* `-s` : Random seed
* `-a` : Address space size (e.g., 1k, 64k, 32m, 1g)
* `-p` : Physical memory size (must be > address space size)
* `-n` : Number of virtual addresses to generate
* `-b` : Base register value (default: random)
* `-l` : Limit register value (default: random)
* `-c` : Compute physical addresses automatically (otherwise, exercise mode)

#### Sample Output:

```
Base-and-Bounds register information:

  Base   : 0x00001000 (decimal 4096)
  Limit  : 512

Virtual Address Trace
  VA  0: 0x000000d2 (decimal:  210) --> VALID: 0x000010d2 (decimal:  4306)
  VA  1: 0x000001fe (decimal:  510) --> SEGMENTATION VIOLATION
```

---

### 2️⃣ Segmentation Simulation (`segmentation.py`)

Segmentation splits the address space into **two segments**:

* **Segment 0** → grows upward (positive direction)
* **Segment 1** → grows downward (negative direction)

#### Example:

```bash
python segmentation.py -s 2 -a 1k -p 16k -n 5 -c
```

#### Options:

* `-s` : Random seed
* `-a` : Address space size
* `-p` : Physical memory size
* `-n` : Number of addresses to generate
* `-A` : Comma-separated list of addresses (instead of random)
* `-b / -l` : Base & Limit for Segment 0
* `-B / -L` : Base & Limit for Segment 1
* `-c` : Compute physical addresses automatically

#### Sample Output:

```
Segment register information:

  Segment 0 base  (grows positive) : 0x00000400 (decimal 1024)
  Segment 0 limit                  : 256

  Segment 1 base  (grows negative) : 0x00001000 (decimal 4096)
  Segment 1 limit                  : 256

Virtual Address Trace
  VA  0: 0x000001e0 (decimal:  480) --> VALID in SEG0: 0x000005e0 (decimal: 1504)
  VA  1: 0x000003f0 (decimal: 1008) --> SEGMENTATION VIOLATION (SEG0)
  VA  2: 0x00000810 (decimal: 2064) --> VALID in SEG1: 0x00000e10 (decimal: 3600)
```

---

## 📊 Concepts Covered

* **Relocation (Base + Limit Registers)**: Simple memory protection & relocation mechanism.
* **Segmentation**: Splitting process address space into logically separate segments.
* **Virtual to Physical Address Translation**.
* **Segmentation Violations** (invalid memory accesses).

---

## 👨‍💻 Author

* Hasan Zarook (2021-CE-58)

---
