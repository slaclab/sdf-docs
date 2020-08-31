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

All SLAC employees and experimental facility users and affiliate are automatically granted permissions to access and utilise SDF resources. By default, all users are granted use of the [shared partition](batch-compute.md#shared-partition] whereby your jobs may be pre-empted to higher priority users (ie users/groups whom have purchased hardware resources add onto SDF will get immediate access to their resources, thereby 'kicking-off' any users using the shared partition that may be using their servers at that time). Whilst we wish to meet the needs of everyone, it may not be always possible to do conduct your reseearch on the 'free' resources provided by this shared partition. Users and their affiliated group(s) are also provided free storage.

We invite all groups, users, and internal and/or external experiments to purchase additional resources.

### Compute

Compute hardware is provided at cost and CPU and GPU compute servers can be selected from a standard list. There are no hosting fee's and we will provide administration, data center hosting and networking free of charge. Whilst we welcome users/groups to pool together to purchase a chassis (of one or more individual servers), we cannot offer unit increments of compute resource of less than one server due to the way we enforce scheduling in the SDF.

!> Provide link to a protected google spreadsheet or something

### Storage

Storage can be purchased in our standard 'Building Blocks' which provide a unit increment that is tuned for our storage environment. We welcome groups/users to pool resources storage procuments together to meet our minimum building block size. The storage will be maintained for the life of the disks (currently five/six/seven??? years) and there shall be no fee's beyond the initial procuremnt (at cost) costs. The added storage wil show up as a bump up in your [quota](TODO.md)

!> We are still finalising our storage quotas. If you have any suggestions please [contact us!](contact-us.md)


## Who Do I Contact to Access More Resources? :id=allocations

If you are a SDF User, and find that the Shared partition is restrictive for your needs, then please reach out to your local coordinator to be added to different partitions if you need more compute, or to increase your $GROUP storage quota. We will not honour increases in $HOME quota. 

| | | |
|--- |--- |--- |
|atlas  |ATLAS Group    |Yee/Wei |
|cryoem |CryoEM Group   |Yee     |
|hps      |HPS Group      |Omar    |
|LCLS     |LCLS Group     |Wilko   |
|ml         |Machine Learning Initiative |      Daniel/Yee |
|neutrino       |Neutrino Group | Kazu |
|shared |Everyone           |Renata/Yee |
|suncat |SUNCAT Group   | Johanne|
|supercdms|SuperCDMS Group | Tina|


