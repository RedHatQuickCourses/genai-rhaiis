
## temp space for storing command while developing this course. 

podman run --rm -it --name rhaiis-server \
  --device nvidia.com/gpu=all \
  --security-opt=label=disable \
  --shm-size=4GB -p 8000:8000 \
  --env "HUGGING_FACE_HUB_TOKEN=$HF_TOKEN" \
  --env "HF_HUB_OFFLINE=0" \
  --env=VLLM_NO_USAGE_STATS=1 \
  -v $HOME/rhaiis-cache:/opt/app-root/src/.cache:Z \
  registry.redhat.io/rhaii/vllm-cuda-rhel9:3.4.1-1780356914 \
  --model RedHatAI/Qwen3-8B-FP8-dynamic


podman run --rm -it --name rhaiis-server \
  --device nvidia.com/gpu=all \
  --security-opt=label=disable \
  --userns=keep-id \
  --shm-size=4GB -p 8000:8000 \
  --env "HUGGING_FACE_HUB_TOKEN=$HF_TOKEN" \
  --env "HF_HUB_OFFLINE=0" \
  --env=VLLM_NO_USAGE_STATS=1 \
  -v $HOME/rhaiis-cache:/opt/app-root/src/.cache:Z \
  registry.redhat.io/rhaii/vllm-cuda-rhel9:3.4.1-1780356914 \
  --model RedHatAI/Qwen3-8B-FP8-dynamic
  --max-model-len=auto
  --gpu-memory-utilization=.95


  curl -X POST http://localhost:8000/v1/completions \
-H "Content-Type: application/json" \
-d '{
  "prompt": "What are the key benefits of using Red Hat AI Inference Server?",
  "model": "RedHatAI/Qwen3-8B-FP8-dynamic",
  "max_tokens": 150
}' | jq .choices[0].text


podman run --rm -it --name rhaiis-server \
  --device nvidia.com/gpu=all \
  --security-opt=label=disable \
  --userns=keep-id \
  --shm-size=4GB -p 8000:8000 \
  --env "HUGGING_FACE_HUB_TOKEN=$HF_TOKEN" \
  --env "HF_HUB_OFFLINE=0" \
  --env=VLLM_NO_USAGE_STATS=1 \
  -v $HOME/rhaiis-cache:/opt/app-root/src/.cache:Z \
  registry.redhat.io/rhaii/vllm-cuda-rhel9:3.4.1-1780356914 \
  --model RedHatAI/granite-3.1-8b-instruct \
  --max-model-len auto \
  --gpu-memory-utilization 0.95


  podman run --rm -it --name rhaii-server \
  --device nvidia.com/gpu=all \
  --security-opt=label=disable \
  --userns=keep-id \
  --shm-size=4GB -p 8000:8000 \
  --env "HUGGING_FACE_HUB_TOKEN=$HF_TOKEN" \
  --env "HF_HUB_OFFLINE=0" \
  --env=VLLM_NO_USAGE_STATS=1 \
  -v $HOME/rhaiis-cache:/opt/app-root/src/.cache:Z \
  registry.redhat.io/rhaii/vllm-cuda-rhel9:3.4.1-1780356914 \
  --model RedHatAI/granite-3.1-8b-instruct \
  --max-model-len 16384 \
  --api-key my-secret-token


  podman run --rm -it --name rhaii-server \
  --device nvidia.com/gpu=all \
  --security-opt=label=disable \
  --userns=keep-id \
  --shm-size=4GB -p 8000:8000 \
  --env "HUGGING_FACE_HUB_TOKEN=$HF_TOKEN" \
  --env "HF_HUB_OFFLINE=0" \
  --env=VLLM_NO_USAGE_STATS=1 \
  -v $HOME/rhaiis-cache:/opt/app-root/src/.cache:Z \
  registry.redhat.io/rhaii/vllm-cuda-rhel9:3.4.1-1780356914 \
  --model RedHatAI/granite-3.1-8b-instruct \
  --max-model-len 16384 \
  --api-key my-secret-token



    curl -X POST http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer my-secret-token" \
  -d '{
    "model": "RedHatAI/granite-3.1-8b-instruct",
    "messages": [
      {"role": "user", "content": "What is the IBM Granite series of models?"}
    ],
    "max_tokens": 150
  }' | jq '.choices[0].message.content'