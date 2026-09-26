# Quest #15490 demo transcripts

Live transcripts of the /v1/messages translation layer (PR with `Fixes #15490`)
exercised against the live Chat Completions pipeline at gen.pollinations.ai:

- 01-plain.json - curl, plain request (model openai), Anthropic message + usage
- 02-stream.sse - curl, SSE stream (message_start / content_block_* / message_delta / message_stop)
- 03-tooluse.json - curl, tool use round trip (tool_use block, stop_reason: tool_use)
- 04-python-sdk.txt - official Anthropic Python SDK 1.8.0 (plain + streaming + tool use)
- 05-ts-sdk.txt - official Anthropic TypeScript SDK (plain + streaming + tool use)

The endpoint was exercised through the exact translation modules of the PR
(messagesToChatRequest / chatCompletionToMessage / toAnthropicMessageStream);
the worker-level wiring (Hono route + middleware chain) is covered by the
four unit test files added in the PR (47 tests, node vitest pool).
