### Install Kyverno using Helm
In order to install Kyverno with Helm, first add the Kyverno Helm repository.

```bash
helm repo add kyverno https://kyverno.github.io/kyverno/
```

Scan the new repository for charts.

```bash
helm repo update
helm install kyverno-policies kyverno/kyverno-policies -n kyverno
```
this tutorial is suitable for setting up the kyverno in a standalone environment, if you wish to set it up in your production environemnt, consider using HA.

```bash
helm install kyverno kyverno/kyverno -n kyverno --create-namespace \
--set admissionController.replicas=3 \
--set backgroundController.replicas=2 \
--set cleanupController.replicas=2 \
--set reportsController.replicas=2
```

