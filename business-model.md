# S3DF Business Model

!> We're still beta-testing SDF; if you have any questions or suggestions, please feel free to [contact us](contact-us.md)!

## What is the SDF?

Science at SLAC is often powered by intensive numerical analysis of large datasets: the computation and storage needs for large scale science projects such as [x-ray crystallography](https://lcls.slac.stanford.edu) and [CryoEM](https://cryoem.slac.stanford.edu) often requires petaflops of compute and petabytes of storage. The SDF serves to provide the hardware and software infrastructure in order to keep science ticking.

The SDF is comprised of many high powered compute servers interconnected with high speed networking fabrics. This in turn is connected to high performance storage. This, as well as the ecosystem that utilises all this power, is what we call the SDF. 

SDF is owned and operated by SLAC's Scientific Computing Services in partnership with, and in support of, the SLAC research community.

## Why use SDF?

The SDF is tuned specifically to allow large and small compute and storage tasks. By storing your scientific datasets on the SDF, you will benefit from the economies of scale to help drive down the cost of data management. Through community sharing of compute resources you will be able to obtain compute cycles funded through indirects, whilst at the same time having immediate access to resources that [you own](resources-and-allocations.md#contributing-to-sdf)

## How much does it cost?

All SLAC employees, researchers and facility users have free access to the SDF. Now, free does not necessarily mean capable: every user, by default, is added to a [shared partition](batch-compute.md#shared-partition) that allows you to immediately submit jobs onto the clusters, but which has low priority on the queue. Each user is also entitled to long and short term storage for both themselves and their "groups" free of charge. Please see [Resources](resources-and-allocations.md) for up-to-date information.

If you find that you need more compute and or storage for your scientific needs, please see [contributing to SDF](resources-and-allocations.md#contributing-to-sdf).
 

## Contributing to SDF :id=contributing-to-sdf

All SLAC employees, experimental facility users, and their affiliates are automatically granted permissions to access and utilise SDF resources. By default, all users are granted use of the [shared partition](batch-compute.md#shared-partition] whereby your jobs may be pre-empted for those from higher-priority users (i.e., users/groups who have purchased hardware in SDF will get immediate access to their resources, thereby 'kicking-off' any users using the shared partition that may be using those same servers at the time). Whilst we wish to meet the needs of everyone, it may not be always possible to do conduct your reseearch on the 'free' resources provided by this shared partition. Users and their affiliated group(s) are also provided free storage.

We invite all groups, users, and internal and/or external experiments to purchase resources in SDF to guarantee access.

### Compute

Compute hardware is provided at cost and CPU and GPU compute servers can be selected from a standard list. There are no hosting fee's and we will provide administration, data center hosting and networking free of charge. Whilst we welcome users/groups to pool together to purchase a chassis (of one or more individual servers), we cannot offer unit increments of compute resource of less than one server due to the way we enforce scheduling in the SDF.

!> Provide link to a protected google spreadsheet or something

### Storage

Storage can be purchased in our standard 'Building Blocks' which provide a unit increment that is tuned for our storage environment. We welcome groups/users to pool resources storage procuments together to meet our minimum building block size. The storage will be maintained for the life of the disks (currently five/six/seven??? years) and there shall be no fee's beyond the initial procurement (at cost) costs. The added storage wil show up as a bump up in your [quota](TODO.md)

!> We are still finalising our storage quotas. If you have any suggestions please [contact us!](contact-us.md)


## Who Do I Contact to Access More Resources? :id=allocations

If you are a SDF User, and find that the Shared partition is restrictive for your needs, then please reach out to your local coordinator to be added to different partitions if you need more compute resources, or to increase your $GROUP storage quota. We will not honour increases in $HOME quota. 

| | | |
|--- |--- |--- |
|atlas  |ATLAS Group    |Yee/Wei |
|cryoem |CryoEM Group   |Yee     |
|hps      |HPS Group      |Omar    |
|kipac    |Kipac Group    |Stuart Marshall |
|LCLS     |LCLS Group     |Wilko   |
|ml         |Machine Learning Initiative |      Daniel/Yee |
|neutrino       |Neutrino Group | Kazu |
|shared |Everyone           |Renata/Yee |
|suncat |SUNCAT Group   | Johanne|
|supercdms|SuperCDMS Group | Tina|


