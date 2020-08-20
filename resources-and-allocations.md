# Resources and Allocations

## SDF Hardware 

### Compute

#### 88 x Dual 64-core Rome Server (11,264 cores)

Each server consists of
- Dual socket [AMD Rome 7702P](https://www.amd.com/en/products/cpu/amd-epyc-7702) CPU with 64 cores per socket (128 threads) @ 2.0Ghz base close, with boost to 3.35GHz
- 512GB RAM across 32 x 16GB
- Single 960GB shared boot, local scratch (`/lscratch`)

#### 10 x 10-way Nividia Geforce 1080Ti GPU Servers (100 GPUs)

Each server consists of
- 10 x Nvidia Geforce 1080Ti with 11GB each, on a single root pci-e complex
- Dual socket Intel Xeon E5-2670 v3 with 12 cores per socket (24 threads) @ 2.3Ghz
- 256 GB RAM
- Single 480GB SSD boot drive
- 3 x 1.92TB SSD local scratch

#### 26 x 10-way Nvidia Geforce 2080Ti GPU Servers (260 GPUs)

Each server consists of
- 10 x Nvidia Geforce 2080Ti with 11GB each, on a single root pci-e complex
- Dual socket Intel Xeon Gold 5118 with 12 cores per socket (24 threads) @ 2.3Ghz
- 192GB RAM
- Single 480GB SSD boot drive
- 3 x 1.92TB SSD local scratch

#### 7 x 4-way Nvidia Tesla V100 GPU Servers (28 GPUs)

Each server consists of
- 4 x Nvidia Tesla V100 NVLink with 32GB each
- Dual socket Intel Silver 4110 with 8 cores per scoket (16 threads) @ 2.1Ghz
- 192GB RAM
- Single 480GB SSD boot drive
- 2 x 1.92TB SSD local scratch


### Storage

#### 2 x DDN ES18K


## Contributing to SDF :id=contributing-to-sdf
