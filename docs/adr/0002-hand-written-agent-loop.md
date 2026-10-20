# Hand-written agent loop instead of LangGraph

Both the Answering agent and the Research agent are a plain loop over an OpenAI-compatible chat completions API with tool calls, written by hand. The main reason to use LangGraph was interrupt and checkpointing to pause a Turn while a Research proposal waits for the user. We decided instead that a Research proposal ends the Turn, and accepting it starts a separate Research job. Nothing ever has to pause mid-graph. What remains (tool dispatch, call limits, Evidence tracking, streaming) is roughly 200 lines that we fully understand, which matters because Evidence checking and the Test set depend on exact control over what enters the context.

## Considered Options

- **LangGraph**: rejected because its key features, interrupt and checkpointing, are unused once proposals end the Turn.
- **Pydantic AI**: lighter, but still hides the loop we need to instrument.
