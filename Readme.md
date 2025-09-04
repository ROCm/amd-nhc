# Advanced Micro Devices NHC Scripts

## Introduction

AMD's NHC Scripts are add-on health checks for the widely utilized [Node Health Check (NHC)](https://github.com/mej/nhc) framework.  These specialized scripts enhance monitoring capablities by adding AMD-specific checks focusing on AI/ML and HPC clusters. Key focuses of this repository are RDMA networking and GPU health checks.

## Installation

First, begin by installing and configuring [Node Health Check](https://github.com/mej/nhc).

To install the additional checks from this repo, simply copy all files under `scripts/` to `/etc/nhc/scripts/` on the host you wish to monitor.  These scripts are now ready to be used!

## Configuration

Once the files have been put into place, just update `/etc/nhc/nhc.conf` with the checks you would like to use.

### Built-in Checks
- [check\_gpu\_count](#check\_gpu\_count)
- [check\_amd\_version](#check\_amd\_version)
- [check\_rdma\_hw](#check\_rdma\_hw)

#### check\_gpu\_count

`check_gpu_count num`

Checks that `num` AMD GPUs exist on the system.

Example:
```
* || check_gpu_count 8
```

#### check\_amd\_version

`check_amd_version driver_ver`

Checks that the AMD driver in use is as defined.

Example:
```
* || check_amd_version 6.12.2
```

#### check\_rdma\_hw

`check_rdma_hw ibdev:port [ optional: bw ] [ optional: MTU ] [ optional: fw ]`

Checks that the defined RDMA Interface exists.  Optionally checks the bandwidth, MTU, and firmware are as defined.  Position matters, so to check firmware, you must also check bandwidth and MTU.

Example:
```
# Checks the interface exists with 200 Gb/s, MTU of 9000,
# and has firmware version 230.0.156.0
* || check_rdma_hw bnxt_re0:1 200 9000 230.0.156.0
# Just verifies the interface exists
* || check_rdma_hw bnxt_re1:1
# Verifies the interface exists with a bandwidth of 100 Gb/s
* || check_rdma_hw bnxt_re2:1 100
# Verifies the interface exists with a bandwidth of 200 Gb/s and MTU of 9000
* || check_rdma_hw bnxt_re3:1 200 9000
```
