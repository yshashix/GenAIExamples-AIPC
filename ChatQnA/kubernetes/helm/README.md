# Deploy ChatQnA on Kubernetes cluster

- You should have Helm (version >= 3.15) installed. Refer to the [Helm Installation Guide](https://helm.sh/docs/intro/install/) for more information.
- For more deploy options, refer to [helm charts README](https://github.com/opea-project/GenAIInfra/tree/main/helm-charts#readme).

## Deploy on Xeon

```
export HFTOKEN="insert-your-huggingface-token-here"
helm install chatqna oci://ghcr.io/opea-project/charts/chatqna  --set global.HUGGINGFACEHUB_API_TOKEN=${HFTOKEN} -f cpu-values.yaml
```

## Deploy on Gaudi

```
export HFTOKEN="insert-your-huggingface-token-here"
helm install chatqna oci://ghcr.io/opea-project/charts/chatqna  --set global.HUGGINGFACEHUB_API_TOKEN=${HFTOKEN} -f gaudi-vllm-values.yaml
```

## Deploy variants of ChatQnA

ChatQnA is configurable and you can enable/disable features by providing values.yaml file.
For example, to run with tgi instead of vllm inference engine on Gaudi hardware, use gaudi-tgi-values.yaml file:

```
export HFTOKEN="insert-your-huggingface-token-here"
helm install chatqna oci://ghcr.io/opea-project/charts/chatqna  --set global.HUGGINGFACEHUB_API_TOKEN=${HFTOKEN} -f gaudi-tgi-values.yaml
```

See other *-values.yaml files in this directory for more reference.

## Deploy on Intel AIPC with iGPU
ChatQnA on Intel AIPC ussing IPEX-LLM Ollama Lama3.2 LLM is configurable and you can change some config of ollama model by changing in values.yaml file.

Require: Intel GPU Device Plugin for Kubernetes [ https://github.com/intel/intel-device-plugins-for-kubernetes/blob/main/cmd/gpu_plugin/README.md]

Recommened changes to look in values.yaml:
1. Insert-your-huggingface-token in values.yaml
2. Change iGPU driver as per your system in ollama gpuResourceName
3. Add proxy setting if your setup run behind proxy
4. Update images version in case doesn't match
```
 huggingface:
  token: hf_wxxxxxxxxxxxxxxx
ollama:
  resources:
    gpuResourceName: gpu.intel.com/xe  # or gpu.intel.com/i915
```