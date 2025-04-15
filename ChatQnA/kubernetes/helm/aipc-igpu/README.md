
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