## Run LLMs locally

### Mistral 7B

* Define the models to run

```md
model=mistralai/Mistral-7B-Instruct-v0.2
volume=$PWD/data # share a volume with the Docker container to avoid downloading weights every run
```

* Run the models

```md
docker run -d --gpus all --shm-size 1g -p 8080:80 -v $volume:/data ghcr.io/huggingface/text-generation-inference:2.0 --model-id $model
```

### Llama2 7B

* Define the models to run

```md
model=meta-llama/Llama-2-7b-chat-hf
volume=$PWD/data
token=<your cli READ token>
```

* Run the models

```md
docker run --gpus all --shm-size 1g -e HUGGING_FACE_HUB_TOKEN=$token -p 8080:80 -v $volume:/data ghcr.io/huggingface/text-generation-inference:2.0 --model-id $model
```

### Test models with Curl

* Curl the models

```md
curl 127.0.0.1:8080/generate \
    -X POST \
    -d '{"inputs":"What is the capital of Spain?","parameters":{"max_new_tokens":2000}}' \
    -H 'Content-Type: application/json' | jq -r .
```