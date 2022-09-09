# my-kubeflow quick and dirty test
    https://github.com/kubeflow/manifests#installation
    https://github.com/kubeflow/manifests#connect-to-your-kubeflow-cluster

# Istio Certificates  and to avoid   XSRF-TOKEN errors
    https://www.civo.com/learn/get-up-and-running-with-kubeflow-on-civo-kubernetes

    kubectl edit -n kubeflow gateways.networking.istio.io kubeflow-gateway

    kubectl edit destinationrule -n kubeflow ml-pipeline
    kubectl edit destinationrule -n kubeflow ml-pipeline-ui
    
    # Edit the spec.trafficPolicy.tls.mode section, changing its value from ISTIO_MUTUAL to DISABLE


