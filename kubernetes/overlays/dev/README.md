Note that the dev overlay has these changes from the base and/or the prod overlay:
* 1 replica instead of 2
* dev prefix for namespace and names
* git-sync points at `s3df-dev` branch instead of `s3df`
* ingress host is `s3df-dev.slac.stanford.edu`
