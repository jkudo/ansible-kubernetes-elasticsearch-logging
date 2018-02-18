<p align="center"><img src="https://github.com/ashleymcnamara/gophers/blob/master/KUBERNETES_GOPHER.png" width="300"></p>

<p align="center"><b>Configuring ElasticSearch logging for your Kubernetes cluster.</b></p>

# Intro #

Playbooks here will help you install logging using ElasticSearch for your Kubernetes cluster.

## Installing

```bash
ansible-playbook install.yaml -e 'kubeconfig=admin.conf' --extra-vars='{"nodes": [node1,node2]}' -v
```

## Deleting
```bash
ansible-playbook delete.yaml -e 'kubeconfig=admin.conf' --extra-vars='{"nodes": [node1,node2]}' -v
```