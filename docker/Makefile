TAG ?= latest
RUNTIME ?= sudo docker
NOCACHE ?= 

docker:
	$(RUNTIME) build . $(NOCACHE) -t slaclab/slac-ondemand:$(TAG)
	$(RUNTIME) push slaclab/slac-ondemand:$(TAG)

docs:
	$(RUNTIME) build . -f Dockerfile.docs -t slaclab/sdf-docs:$(TAG)
	$(RUNTIME) push slaclab/sdf-docs:$(TAG)
