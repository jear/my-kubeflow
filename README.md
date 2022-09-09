# my-kubeflow quick and dirty test
    https://github.com/kubeflow/manifests#installation
    https://github.com/kubeflow/manifests#connect-to-your-kubeflow-cluster

# Istio Certificates  and to avoid   XSRF-TOKEN errors
    https://www.civo.com/learn/get-up-and-running-with-kubeflow-on-civo-kubernetes

    kubectl edit -n kubeflow gateways.networking.istio.io kubeflow-gateway

    
    # Edit the spec.trafficPolicy.tls.mode section, changing its value from ISTIO_MUTUAL to DISABLE
    kubectl get destinationrule -n kubeflow
    NAME                              HOST                                                         AGE
    metadata-grpc-service             metadata-grpc-service.kubeflow.svc.cluster.local             6d16h
    ml-pipeline                       ml-pipeline.kubeflow.svc.cluster.local                       6d16h
    ml-pipeline-minio                 minio-service.kubeflow.svc.cluster.local                     6d16h
    ml-pipeline-mysql                 mysql.kubeflow.svc.cluster.local                             6d16h
    ml-pipeline-ui                    ml-pipeline-ui.kubeflow.svc.cluster.local                    6d16h
    ml-pipeline-visualizationserver   ml-pipeline-visualizationserver.kubeflow.svc.cluster.local   6d16h

    kubectl edit destinationrule -n kubeflow ml-pipeline
    kubectl edit destinationrule -n kubeflow ml-pipeline-ui
    ...
