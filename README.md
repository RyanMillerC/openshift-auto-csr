# openshift-auto-csr

OpenShift manages internal TLS certificates and will automatically approve
certificate signing requests (CSRs) under normal circumstances. If you
frequently turn off your OpenShift cluster (lab, etc.), you'll quickly find
that if a certificate expires while the cluster is powered off, OpenShift will
**NOT** automatically renew that certificate. Instead, OpenShift will generate
pending CSRs will hang indefinitely until manually approved with `oc adm
cerficiate approve`.

This Helm chart deploys a CronJob that will check for any pending CSRs and
automatically approve them every 5 minutes.

## How to Use

* `helm install --namespace auto-csr --create-namespace auto-csr .`
