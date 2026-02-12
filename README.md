# Thor Inference

```bas
uv run vllm serve Qwen/Qwen2.5-1.5B-Instruct
uv run vllm serve Qwen/Qwen3-4B-Instruct-2507
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
