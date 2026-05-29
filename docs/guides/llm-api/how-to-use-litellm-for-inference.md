# How to use LiteLLM for inference

## Running inference

Send a chat completion request to the LiteLLM proxy using the OpenAI-compatible API:

```sh
curl -s https://litellm.safe.ai/v1/chat/completions \
  -H "Authorization: Bearer $LITELLM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "<model-name>",
    "messages": [
      {"role": "user", "content": "Say hello in one sentence."}
    ]
  }' | jq
```

Set `LITELLM_API_KEY` to your API key (it starts with `sk`), or replace `$LITELLM_API_KEY` with the key directly. Replace `<model-name>` with any model available on the proxy — you can list them with:

```sh
curl -s https://litellm.safe.ai/v1/models \
  -H "Authorization: Bearer $LITELLM_API_KEY" \
  | jq '.data[].id'
```

## Checking your API budget

CAIS provides access to a shared LLM proxy at `litellm.safe.ai`. You can check your current budget and usage at any time using your API key.

```sh
curl -fsSL https://litellm.safe.ai/usage/self/budget \
  -H "Authorization: Bearer <your-api-key>" \
  | jq
```

Replace `<your-api-key>` with your API key (it starts with `sk`).

The response shows your current spend, budget limit, and reset period:

```json
{
  "spend": 1.23,
  "max_budget": 50.0,
  "budget_duration": "monthly",
  "budget_reset_at": "2026-06-01T00:00:00Z"
}
```

!!! tip
    If you don't have `jq` installed, you can omit it — the raw JSON will still be printed to your terminal.
