- OpenAI Responses subscription mode now sends a stable `session_id` header
  (and matching `prompt_cache_key`): an adapter-lifetime id plus a digest of
  the instructions and first input item, which groups requests by serialized
  head. The ChatGPT backend keys its prompt cache on that header and ignores
  the body key, so every request used to get a fresh random key and a
  byte-stable 170k-token prefix read `cached_tokens: 0` on every call. New
  `sessionId` config pins the base id across restarts; a request's
  `extra.prompt_cache_key` replaces the computed id. `extraHeaders` now
  override built-in headers case-insensitively.
