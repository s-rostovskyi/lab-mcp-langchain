# Agents that Speak MCP Fluently

[lab_proof.md](lab_proof.md) is the evidence entry point for this submission.

The [executed notebook](Lab_agent_speak_fluently.ipynb) connects a local Filesystem
MCP server over stdio and the public LangChain Docs MCP server over HTTP. Each
server has a separate `MultiServerMCPClient`. The remote service requires no
additional token. This follows the lab's allowance for alternative MCP servers.

## Sources and environment

`sample_docs/` contains unchanged copies of the two supplied course handouts:

- `mcp_servers_local_vs_remote.md`
- `mcp_tools_resources_prompts.md`

These handouts replace the Project Atlas documents referenced by the course
notebook but absent from the supplied materials. The questions concern the
handouts themselves; no Project Atlas facts are invented.

The notebook uses Python, Node.js/npx, the packages in `requirements.txt`, and an
`OPENAI_API_KEY` loaded from the local `.env`. The default model is `gpt-4o-mini`;
`OPENAI_MODEL` can override it. No credential is embedded in the notebook.
The local npm server is pinned to `@modelcontextprotocol/server-filesystem@2.0.1`.

## Evidence files

| File | Contents |
|---|---|
| `evidence/discovery.json` | Actual tool inventory and resource discovery |
| `evidence/tool_log.jsonl` | Full MCP tool arguments, responses, scenario labels, and call IDs |
| `evidence/agent_runs.json` | Queries, final answers, and full message traces |
| `evidence/langchain_guide.md` | Snapshot of the MCP resource used as model context |
| `evidence/resource_checks.json` | Resource URI, SHA-256, keyword matches, and source lines |
| `evidence/direct_memory_page.md` | Snapshot used for the direct HTTP comparison |
| `evidence/direct_comparison.json` | Direct HTTP metadata and both comparison answers |
| `evidence/grounding_review.json` | Observed source-reading error and the reason for a targeted recheck |
| `evidence/manifest.json` | Runtime versions, source hashes, and completed scenarios |

The notebook uses top-level `await`, as in the course examples. Its saved outputs
show the observed run; remote documents and model responses can change later.
The Windows stderr adjustment follows the supplied notebook's workaround.

## Scope and limitations

The agents receive an allowlist of read tools. A client-side guard requires
directory discovery before other filesystem operations; blocked attempts remain
visible as errors in the trace. The filesystem root is restricted
to `sample_docs/`, keeping `.env` outside that root. Documentation feedback and
filesystem write tools are excluded from the agent's tool list. The underlying
Filesystem server is trusted software and still implements write operations.

Local stdio does not guarantee local model inference. Tool results supplied to
ChatOpenAI leave the machine for hosted inference. The local handouts and remote
guide are educational data. Secrets and unrelated local files are excluded.

The original assignment and grading rubric remain in
[instructions.md](instructions.md) and [rubric.md](rubric.md). Commits, pushes,
and pull request submission are separate from this local implementation.
