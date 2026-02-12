# Thor Inference

```bash
export TORCH_CUDA_ARCH_LIST=12.1f # Spark, for Thor 11.0a
export TRITON_PTXAS_PATH=/usr/local/cuda/bin/ptxas
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

```bash
sudo sysctl -w vm.drop_caches=3
```

```bas
uv run vllm serve "Qwen/Qwen2.5-1.5B-Instruct" --async-scheduling --port 8000 --host 0.0.0.0 --trust_remote_code --swap-space 16 --max-model-len 32000 --tensor-parallel-size 1 --max-num-seqs 1024 --gpu-memory-utilization 0.7

uv run vllm serve
uv run vllm serve Qwen/Qwen3-4B-Instruct-2507
uv run vllm serve Qwen/Qwen3-4B-Instruct-2507 --disable-frontend-multiprocessing --enforce-eager
uv run vllm serve meta-llama/Llama-3.2-3B-Instruct --disable-frontend-multiprocessing --enforce-eager --gpu-memory-utilization 0.8
uv run vllm serve “Qwen/Qwen3-VL-b32B-Instruct” --async-scheduling --port 8000 --host 0.0.0.0 --trust-remote-code --swap-space 16 --max-model-len 4096 --tensor-parallel-size 1 --max-num-seqs 2 --gpu-memory-utilization 0.95 --kv-cache-dtype fp8 --enable-prefix-caching --dtype half --enable-chunked-prefill
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
