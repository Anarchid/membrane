- OpenAI Responses subscription mode now sends a stable `session_id` header
  (and matching `prompt_cache_key`) per logical stream: an adapter-lifetime id
  plus a digest of the instructions and first input item. The ChatGPT backend
  keys its prompt cache on that header and ignores the body key, so every
  request used to get a fresh random key and a byte-stable 170k-token prefix
  read `cached_tokens: 0` on every call. New `sessionId` config pins the base
  id; a request's `extra.prompt_cache_key` is used verbatim instead.
