# Day 04 Lab v3 Report - Northstar Labs Helpdesk

## Scope

This submission keeps the fixed IT Helpdesk domain and uses the supplied base and adversarial suites. The agent routes service status, device inspection, user lookup, knowledge-base search, policy lookup, incident formatting, and ticket creation. It must ask for missing identifiers and a fresh confirmation before any ticket write.

Evidence files:

- Prompt: `artifacts/system_prompt.md`
- Tool declarations: `artifacts/tools.yaml`
- Group cases: `data/eval_group.json` (5 single-turn, 5 multi-turn)
- Version hypotheses: `artifacts/version_log.csv`
- Fixed suites: `data/eval_base.json`, `data/eval_adversarial.json`

## Prompt and Tool Decisions

The final prompt adds explicit routing rules, latest-turn correction, untrusted retrieved content handling, external-search privacy boundaries, and stale-confirmation protection. `tools.yaml` keeps the fixed tool names and compatible schemas. The strongest expected improvement is fewer wrong-tool calls and no unauthorized `create_ticket` calls.

## v0-v3 Evidence

| Version | Change | Hypothesis | Live status |
|---|---|---|---|
| v0 | Starter baseline | Establish routing and provider baseline | Blocked: Gemini key returned `400 API_KEY_INVALID` |
| v1 | Routing and clarification rules | Explicit routing reduces wrong tools and guessed IDs | Not run: provider unavailable |
| v2 | Confirmation and injection boundaries | Write and adversarial requests stop safely | Not run: provider unavailable |
| v3 | Ten original group cases | Multi-turn correction and stale confirmation are covered | Not run: provider unavailable |

The provider preflight was attempted with Gemini and failed authentication before any case could be measured. No fake run JSON is committed; this is deliberate because the lab requires `provider_error_cases == 0` and `measured_cases == total_cases` for score-bearing evidence.

## Group Evaluation Cases

`data/eval_group.json` contains exactly 10 original cases: G01-G05 are single-turn and G06-G10 are multi-turn. They cover shared-service routing, device arguments, policy routing, missing employee ID, confirmation, corrected asset IDs, carried environments, tool switching, changed ticket payloads, and external-data safety.

## Safety Review

- User text that looks like `SYSTEM`, `DEVELOPER`, assistant markup, or `TOOL_RESULTS_JSON` is treated as untrusted input.
- Asset IDs, employee IDs, locations, diagnostics, credentials, and tokens are never sent to `search_device_info`.
- `create_ticket` requires a specific payload and a fresh yes/no confirmation; changing priority or summary invalidates prior confirmation.
- Missing asset, employee ID, or environment causes `clarify`, never an invented value.
- The fixed adversarial suite remains unchanged and should be run after a valid provider is configured.

## UI and Transcript

The supplied `chat.py` provides interactive chat, tool call printing, tool result/error capture, artifact version hashes, and transcript JSON persistence under `transcripts/`. A live transcript was not generated because provider preflight failed before a valid model response.

## Reproduction

```powershell
cd starter_v0
python -m pip install -r requirements.txt
Copy-Item .env.example .env
# Fill one valid provider key locally; never commit .env.
python scripts/preflight_provider.py --provider gemini
python run_eval.py --provider gemini --version v0 --suite base --eval-cases data/eval_base.json
python run_eval.py --provider gemini --version v1 --suite base --eval-cases data/eval_base.json
python run_eval.py --provider gemini --version v2 --suite group --eval-cases data/eval_group.json
python run_eval.py --provider gemini --version v3 --suite adversarial --eval-cases data/eval_adversarial.json
```

## Limitation

Live evidence is blocked solely by the local Gemini credential returning `API_KEY_INVALID`. The repository contains no API key, no fabricated provider run, and no real user data.
