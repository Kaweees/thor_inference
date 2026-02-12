# Thor Inference

```bash
export TORCH_CUDA_ARCH_LIST=11.0f
export TRITON_PTXAS_PATH=/usr/local/cuda/bin/ptxas
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

```bash
uv run vllm serve "Qwen/Qwen2.5-1.5B-Instruct" \
   --port 8000 \
   --host 0.0.0.0 \
   --trust-remote-code \
   --max-model-len 8192 \
   --gpu-memory-utilization 0.7
```

This will start an OpenAI-compatible API server on http://localhost:8000 by default. You can then make requests to it like:

```bash
curl http://localhost:8000/v1/completions \
   -H "Content-Type: application/json" \
   -d '{
   "model": "Qwen2.5-1.5B-Instruct",
   "prompt": "San Francisco is a",
   "max_tokens": 50
   }'
```
