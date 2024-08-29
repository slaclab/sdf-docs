Note that the prod overlay has these changes from the base and/or dev:
* 2 replicas
* prod prefix for namespace and names
* git-sync points at `s3df` branch (vs `s3df-dev` in the dev overlay)
* ingress host is `s3df.slac.stanford.edu` (vs `s3df-dev.slac.stanford.edu` in the dev overlay)
