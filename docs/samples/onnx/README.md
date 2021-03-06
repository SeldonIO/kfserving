
# Predict on a InferenceService using ONNX
## Setup
1. Your ~/.kube/config should point to a cluster with [KFServing installed](https://github.com/kubeflow/kfserving/blob/master/docs/DEVELOPER_GUIDE.md#deploy-kfserving).
2. Your cluster's Istio Ingress gateway must be network accessible.

## Create the InferenceService
Apply the CRD
```
kubectl apply -f onnx.yaml 
```

Expected Output
```
$ inferenceservice.serving.kubeflow.org/style-sample configured
```

## Run a sample inference

1. Setup env vars

Use `kfserving-ingressgateway` as your `INGRESS_GATEWAY` if you are deploying KFServing as part of Kubeflow install, and not independently.

```
export MODEL_NAME=style-sample
export SERVICE_HOSTNAME=$(kubectl get inferenceservice ${MODEL_NAME} -o jsonpath='{.status.url}' | cut -d "/" -f 3)
export INGRESS_GATEWAY=istio-ingressgateway
export CLUSTER_IP=$(kubectl -n istio-system get service $INGRESS_GATEWAY -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
```
2. Verify the service is healthy
```
SERVICE_URL=http://$CLUSTER_IP/v1/models/$MODEL_NAME
curl ${SERVICE_URL}
```
3. Install dependencies
```
pip install -r requirements.txt
```
4. Run the [sample notebook](mosaic-onnx.ipynb) in jupyter
```
jupyter notebook
```

## Uploading your own model
The sample model for the example in this readme is already uploaded and available for use. However if you would like to modify the example to use your own ONNX model, all you need to do is to upload your model as `model.onnx` to S3, GCS or an Azure Blob.
