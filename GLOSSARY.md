# Scholar Workspace

Cited question answering over scientific papers, organized by research topic. When the collection cannot answer a question, the system proposes research instead of guessing.

## Language

### Collection

**Workspace**:
A research topic owned by one user, with a name, a description, and its own Documents. Nothing crosses Workspace boundaries: the same paper in two Workspaces is two separate Documents.
_Avoid_: project, folder, collection

**Demo workspace**:
A pre-filled Workspace that anyone can ask questions in without signing in. It cannot be changed and cannot start Research jobs.
_Avoid_: sandbox, guest workspace

**Document**:
A scientific paper inside one Workspace, added by upload or by research. A Document is either full text or abstract-only, when the paper is not open access.
_Avoid_: paper (for the system object), file

**Chunk**:
A contiguous passage of a Document with a citable location: page and section, or "abstract" for an abstract-only Document.
_Avoid_: passage, snippet

### Answering

**Conversation**:
A sequence of Turns within one Workspace.
_Avoid_: chat, thread, session

**Turn**:
One user question and the agent's response to it. The response is an answer, a Research proposal, or a partial answer together with a Research proposal for the missing part.
_Avoid_: round, step

**Evidence**:
The set of Chunks whose content was given to the agent during one Turn. An answer may cite only its own Turn's Evidence. Metadata such as section titles or document lists is not Evidence.
_Avoid_: context, sources

### Research

**Research proposal**:
A message that ends a Turn by offering to search for new papers on what the Workspace cannot yet answer. The user may accept or dismiss it at any time, and the Conversation is never blocked while it is pending.
_Avoid_: interrupt, pending confirmation

**Answering agent**:
The agent that answers a Turn using only the Workspace's Documents. It ends every Turn with an answer, a Research proposal, or both.
_Avoid_: chatbot, assistant

**Research agent**:
The agent inside a Research job that searches the Research source, reads abstracts, and chooses which papers to add, recording a short reason for each.
_Avoid_: crawler, searcher

**Research job**:
Background work started when a Research proposal is accepted. The Research agent adds new Documents, then the Answering agent answers the original question again as a new message in the Conversation. One accepted proposal runs exactly one job. A job never starts another job by itself, and Documents it finished adding stay even if the job is cancelled.
_Avoid_: task, crawl

**Research source**:
The external catalogue a Research job searches for papers. Currently only arXiv.
_Avoid_: provider, index

**Research budget**:
The hard limits on one Research job: searches, papers added, wall-clock time, and LLM tokens. The job stops at whichever limit it hits first and reports which one.
_Avoid_: cost estimate

### Evaluation

**Test set**:
A fixed collection of Test cases over one evaluation Workspace on RAG, which also serves as the Demo workspace. Drafted by an LLM and finalized by hand. English only.
_Avoid_: benchmark, dataset

**Test case**:
One question with its type (answerable, partially answerable, or out-of-collection), a reference answer, and Gold citations.
_Avoid_: sample, example

**Gold citation**:
The correct source for a Test case: a paper identifier, a page, and a verbatim quote. A citation is correct when the cited Chunk contains or overlaps that quote, so Gold citations survive changes to chunking.
_Avoid_: label, ground truth chunk

**Out-of-collection question**:
A Test case written from a held-out paper that is deliberately absent from the Workspace. The system should respond with a Research proposal, and a Research job should find the held-out paper.
_Avoid_: unanswerable question

**Baseline**:
The fixed pipeline that retrieves once and then answers, used as the comparison point for the agent.
_Avoid_: naive RAG, vanilla
