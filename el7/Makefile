.PHONY: systemd-base systemd-libvirt jenkins-virtualization-jnlp-agent
.PHONY: jenkins-agent-lago-mock

TOOL              := docker
TARGETS           := systemd-base \
	                 systemd-libvirt \
                     jenkins-virtualization-jnlp-agent \
                     jenkins-agent-lago-mock
REPO              := nonameyet
TAG_PATTERN       := '[0-9].[0-9].[0-9]'
TAG	              := \
	$(shell git describe --tags --always --long --match $(TAG_PATTERN))
VERSION 		  := $(shell cut -d - -f 1 <<< $(TAG))
DISTANCE_FROM_TAG := $(shell cut -d - -f 2 <<< $(TAG))
HASH 		      := $(shell cut -d - -f 3 <<< $(TAG))

jenkins-agent-lago-mock: jenkins-virtualization-jnlp-agent
jenkins-virtualization-jnlp-agent: systemd-libvirt
systemd-libvirt: systemd-base

$(TARGETS):
ifeq (0, $(DISTANCE_FROM_TAG))
	$(eval image_tag := $(REPO)/$@:$(VERSION))
	#$(TOOL) build -t $(REPO)/$@:$(VERSION) $@
else
	$(eval image_tag := $(REPO)/$@:$(TAG))
	#$(TOOL) build -t $(REPO)/$@:$(TAG) $@
endif
	$(TOOL) build -t $(image_tag) $@
	@$(TOOL) login --username ${DOCKERHUB_UNAME} --password ${DOCKERHUB_PW}
	$(TOOL) push $(image_tag)
