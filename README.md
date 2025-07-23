# API
+
+This repository contains example manifests for routing requests through *Gloo Gateway*
+to a sample default-petstore service.
+
+## Deploy the sample service
+
+Apply the Deployment and Service defined in [YAML/default-petstore.yaml](YAML/default-petstore.yaml):
+
+bash
+kubectl apply -f YAML/default-petstore.yaml
+
+
+Ensure the default-petstore Pods are running before proceeding.
+
+## Apply the Gloo Gateway configuration
+
+The following resources configure an upstream that points to the petstore
+service and a virtual service that routes traffic to it.
+
+### Upstream
+
+See [YAML/petstore-upstream.yaml](YAML/petstore-upstream.yaml).
+
+### VirtualService
+
+yaml
+
