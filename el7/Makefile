.PHONY: systemd-base systemd-libvirt jenkins-virtualization-jnlp-agent
.PHONY: jenkins-agent-lago-mock

systemd-base:
	docker build -t local/$@ $@

systemd-libvirt: systemd-base
	docker build -t local/$@ $@

jenkins-virtualization-jnlp-agent: systemd-libvirt
	docker build -t local/$@ $@

jenkins-agent-lago-mock: jenkins-virtualization-jnlp-agent
	docker build -t local/$@ $@