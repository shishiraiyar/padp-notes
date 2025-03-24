---
weight: 2
---


# TPU

## TPU

- Application Specific Integrated Circuit
- High Bandwidth Memory
- Very good at matrix multiplication
- Core: MXU (Matrix Multiply Unit)
- Thousands of multiply-accumulators (multiply and add) that are connected in a large physical matrix called systolic array (128 x 128)

## XLA (Accelerated Linear Algebra)

- JIT compiler
- Takes ML framework graph and compiles linear algebra, loss and gradient calculation into TPU machine code
- These parts are run on TPU
- Rest of the code is run by the TPU host machine

## How TPU works

- Host streams data into an infeed queue
- TPU loads data from infeed queue into High Bandwidth Memory (HBM)
- From HBM data is passed into MXU
- After each multiply, the results are passed to the next multiply-accumulator
- Each multiply-accumulator does its multiply and adds the result onto the result it received from the previous multiply-accumulator
- Final result is the sum of all multiply results
- Results are fed into outfeed queue
- Host reads results from outfeed queue

| **GPU**                                      | **TPU**                                                     |
| -------------------------------------------- | ----------------------------------------------------------- |
| General-purpose parallel compute             | Application Specific Integrated Circuit                     |
| Consists of SIMD multiprocessors             | Consists of MXUs (systolic array architecture)              |
| Flexible for different applications          | Specialized for ML                                          |
| Cost varies (consumer vs enterprise)         | High cost                                                   |
| Runs CUDA code (NVIDIA)                      | Runs XLA compiled code                                      |
| Suitable for medium to large ML applications | Suitable for very large ML applications (weeks of training) |
| Can buy GPUs upfront                         | Only available on Google Cloud                              |
