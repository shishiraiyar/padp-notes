---
weight: 1
---

# Fundamentals Of Computer Design

## Classes of Computers

### Personal Mobile Device

Cellphones, tablets etc

- Cost

- Energy Efficiency

- Responsiveness

- Predictability

- Minimize memory

### Desktop

- Largest market for computers

- Price-performance

- Graphics performance

### Servers

- Availability

- Scalability

- Efficient throughput

### Clusters/Warehouse-Scale

- Growth in SaaS led to clusters

- Group of computers connected by LAN

- Very large clusters are warehouse scale

- Price-performance

- Power consumption

- Cooling

- WSCs, unlike servers, use a large number of cheap components for redundancy

### Embedded

- Wide range in compute and cost

- Price

### Classes of Parallelism

Classes of parallelism in applications

- Data Level Parallelism (DLP)

- Task-Level Parallelism (TLP)

Classes of architectural parallelism:

- Instruction Level Parallelism (ILP): Pipelining

- Data Level Parallelism (DLP): Vector architecture/GPU

- Thread Level Parallelism (TLP)

- Request Level Parallelism (RLP)

Flynn's Taxonomy

1. Single instruction stream, Single data stream (**SISD**): can do ILP

2. **SIMD**: DLP. Eg: GPUs

3. **MISD**: No commercial implementation

4. **MIMD**: Can do TLP. Tightly coupled or loosely coupled

## Defining Computer Architecture

### Old view

- Instruction Set Architecture

- Decisions regarding registers, memory addressing, available operations, control flow instructions, instruction encoding etc

### Real computer architecture

- Maximize performance within constraints such as cost, power and availability

- Includes ISA, microarchitecture etc

ISA must be designed to last many decades and withstand technology changes such as:

- Integrated Circuit technology: transistor density, die size

- DRAM capacity

- Flash capacity

- Magnetic disk technology

### Other considerations

**Bandwidth**: Total work done per unit time

**Latency**: Time between start and completion of an event

Transistor performance scales linearly

Integration density scales quadratically

**Power**:

- Power consumption and cooling. 

- Reducing clock rate reduces power but not energy

- energy = 1/2 x capacitive_load x voltage^2

- power = energy x frequency

- Heat dissipation is the limiting factor for single processor chips

- Turn off inactive modules

- Dynamic voltage-frequency scaling

## Trends in Cost

Probably out of syllabus

## Dependability

- Mean Time to Failure (MTTF)

- Mean Time to Repair (MTTR)

- Mean Time Between Failures (MTBF) = MTTF + MTTR

- Availability = MTTF/MTBF

> MTTF adds like parallel resistors

## Measuring Performance

- Response time

- Throughput

- Wall clock time

- CPU time

Benchmarks:

- Toy programs (eg: sorting)

- Synthetic benchmarks

- Benchmark suites

## Principles of Computer Design

- Take advantage of parallelism

- Principle of Locality

### Amdahl's Law

Speed up, $ S = \frac{T(1)}{T(j)}$

T(1): Time taken by one processor

T(j): Time taken by j processors

$$
S = \frac{N}{(B*N) + (1-B)}
$$

When some operations are optimized:

$$
Time_{new} = Time_{old} \times [(1 - frac_{enh}) + \frac{frac_{enh}}{speedup_{enh}}]
$$

$$
Speedup_{overall} = \frac{Time_{old}}{Time_{new}}
$$

### Processor Performance Equation



$$
CPU time = \frac{CPU\ clock\ cycles\ for\ a\ program}{clock\ rate}
$$



$$
CPI = \frac{CPU\ clock\ cycles\ for\ a\ program}{Instruction\ count}
$$



$$
CPU\ clock\ cycles = \sum_{i=1}^n I \cdot C_i \times CPI_i
$$




