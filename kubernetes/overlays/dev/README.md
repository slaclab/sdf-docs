Note that the dev overlay has these changes from the base and/or the prod overlay:
* dev namespace 
* git-sync points at `s3df-dev` branch instead of `s3df`
* ingress host is `s3df-dev.slac.stanford.edu`
* Makefile includes `destroy` recipe
