# my-kubeflow quick and dirty test
    # https://github.com/kubeflow/manifests#installation
    # https://github.com/kubeflow/manifests#connect-to-your-kubeflow-cluster

# cert-manager   
```
# clean gw, cert andd secrets
# beware of the namespace used... 
# Once done, you can get the cert from your browser and add it to yout trusted root

k delete -f kubeflow-gateway-cert-manager.yaml
k delete -f my-certificate-kubeflow-CN.yaml
k delete secrets  -n kubeflow istio-ingressgateway-certs


k apply -f my-certificate-istio-system-CN.yaml
k apply -f kubeflow-gateway-cert-manager.yaml
```
    # https://istio.io/latest/docs/ops/integrations/certmanager/

# Istio Certificates  and to avoid   XSRF-TOKEN errors
    # https://www.civo.com/learn/get-up-and-running-with-kubeflow-on-civo-kubernetes

    kubectl edit -n kubeflow gateways.networking.istio.io kubeflow-gateway

```
kind: Gateway
metadata:
  name: kubeflow-gateway
  namespace: kubeflow
spec:
  selector:
    istio: ingressgateway
  servers:
  - hosts:
    - '*'
    port:
      name: http
      number: 80
      protocol: HTTP
    tls:
      httpsRedirect: true
  - hosts:
    - kubeflow.gpu01.lysdemolab.fr
    port:
      name: https
      number: 443
      protocol: HTTPS
    tls:
      credentialName: istio-ingressgateway-certs
      mode: SIMPLE
```    
    
    
# Istio Troubleshooting    
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
