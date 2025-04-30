# Green System Design: Estimating the Environmental Footprint of Computing Systems

This repository is made in order to accompany the paper with the aforementioned title, by providing access to the Testbed configuration of our system, as well as the experimentation data exported.

## 📄 IEEE Accepted Paper
This repository contains the **accepted version** of our IEEE paper.
Please note that this is **not the final published version**.

©2025 IEEE. Personal use of this material is permitted. 
However, permission to reprint/republish this material for advertising or promotional purposes or 
for creating new collective works for resale or redistribution must be obtained from the IEEE.

The author's accepted manuscript of the following article is located at `/paper` of this repository.

The paper will be presented in **System of Systems Engineering Conference SoSE 2025**.

The published version is available at: [Waiting for URL]

## 📚 Citation

If you use this work, please cite it as:
```
[Waiting for bibtex]
```

## Setup Guide to measure metrics on a Ubuntu OS

This guide is a reference for the paper: "Green system design: Estimating the environmental footprint of computing systems"

In this README, you will find all the steps were done to setup the machine, to be able to measure energy and performance using [Scaphandre](https://github.com/hubblo-org/scaphandre).

## Tech Stack (Hardware/Software)
The machine is an Intel PC architecture with Ubuntu OS. The tools needed:

- Kubernetes
- Docker
- Prometheus
- Grafana Dashboard

## Setup Guide

### Scaphandre Installation

```bash
$ git clone https://github.com/hubblo-org/scaphandre
$ cd scaphandre
$ helm install scaphandre helm/scaphandre
```

### Prometheus Installation
```bash
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo add kube-state-metrics https://kubernetes.github.io/kube-state-metrics
$ helm repo update

#Create port forwarding for Prometheus WebUI
$ kubectl port-forward deploy/prometheus-server 9090:9090
```

### Docker Installation
```bash
$ sudo apt install docker.io
$ docker -version 
$ sudo systemctl enable docker 
$ sudo systemctl start docker
```

### Docker UI Installation (to enable Kubernetes Engine)
```bash
# Add Docker's official GPG key:
$ sudo apt-get update
$ sudo apt-get install ca-certificates curl
$ sudo install -m 0755 -d /etc/apt/keyrings
$ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
$ sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
$ echo 'deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
$ (. /etc/os-release && echo '$VERSION_CODENAME') stable' | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

$ sudo apt-get update

$ wget https://desktop.docker.com/linux/main/amd64/145265/docker-desktop-4.29.0-amd64.deb

$ sudo apt-get install ./docker-desktop-4.29.0-amd64.deb
```

### Prometheus Setup
```bash
$ helm upgrade --install prometheus prometheus-community/prometheus --set prometheus-node-exporter.hostRootFsMount.enabled=false --set prometheus-node-exporter.hostRootFsMount.mountPropagation='HostToContainer'
```


