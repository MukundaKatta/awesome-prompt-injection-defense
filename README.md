# Awesome Prompt Injection Defense [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of tools, papers, datasets, and resources for defending Large Language Models against prompt injection and indirect prompt injection attacks.

Prompt injection is the leading security risk in production LLM systems. The defense ecosystem is fragmented across academic preprints, vendor blogs, npm/PyPI utilities, and ad-hoc system prompts. This list is an attempt to bring it together in one place.

## Contents

- [Detection libraries](#detection-libraries)
- [RAG-specific guardrails](#rag-specific-guardrails)
- [Evaluation datasets](#evaluation-datasets)
- [Live demos](#live-demos)
- [GitHub Actions for CI](#github-actions-for-ci)
- [Research papers and preprints](#research-papers-and-preprints)
- [Adjacent reliability tooling](#adjacent-reliability-tooling)
- [Background reading](#background-reading)
- [Contributing](#contributing)

## Detection libraries

Drop-in checks you call before passing untrusted text to an LLM.

- [prompt-injection-shield](https://github.com/MukundaKatta/prompt-injection-shield) (npm) - Zero-dep detector for classic override, URL exfiltration, system-prompt impersonation, and tool-call hijack patterns.
- [prompt-injection-shield-py](https://pypi.org/project/prompt-injection-shield-py/) (PyPI) - Python port of the above with the same rule set.
- [Rebuff](https://github.com/protectai/rebuff) - Self-hardening prompt injection detector, originally by ProtectAI.
- [LLM Guard](https://github.com/protectai/llm-guard) - Comprehensive LLM input/output security suite, includes prompt injection scanner.
- [PromptArmor](https://github.com/promptarmor/promptarmor) - Hosted prompt injection detection API.
- [Lakera Guard](https://www.lakera.ai/lakera-guard) - Commercial guardrail with a generous free tier.

## RAG-specific guardrails

Prompt injection in RAG often hides inside retrieved documents (indirect injection) or poisoned vectors.

- [vector-poison-score](https://github.com/MukundaKatta/vector-poison-score) (npm) / [vector-poison-score-py](https://pypi.org/project/vector-poison-score-py/) (PyPI) - Heuristic score for whether a retrieved chunk has been poisoned.
- [rag-guardrails-action](https://github.com/MukundaKatta/rag-guardrails-action) - GitHub Action that runs both detectors over a fixtures directory in CI.
- [LangChain Guardrails](https://python.langchain.com/docs/guardrails/) - Built-in chain-of-trust patterns for LangChain-based RAG.
- [LlamaIndex SafetyToolkit](https://docs.llamaindex.ai/en/stable/module_guides/evaluating/) - Evaluation hooks usable as guardrails.
- [HOL Guard](https://github.com/hashgraph-online/hol-guard) - Local-first runtime security for AI coding agents. Intercepts shell commands, secret reads, and MCP changes before execution with configurable protection levels.

## Evaluation datasets

Labeled corpora for benchmarking detectors.

- [prompt-injection-eval](https://huggingface.co/datasets/mukunda1729/prompt-injection-eval) - 74 hand-curated rows across 9 categories (classic override, URL exfil, system impersonation, tool hijack, role override, encoded, indirect RAG poison, borderline, benign). MIT.
- [deepset/prompt-injections](https://huggingface.co/datasets/deepset/prompt-injections) - Larger English/German prompt injection corpus.
- [JailbreakBench](https://github.com/JailbreakBench/jailbreakbench) - Standardised benchmark for jailbreaks (related but broader category).
- [Lakera Gandalf prompts](https://gandalf.lakera.ai/) - Real attack prompts collected from the Gandalf game.

## Live demos

Try detectors in the browser.

- [Prompt Injection Shield Demo](https://huggingface.co/spaces/mukunda1729/prompt-injection-shield-demo) - Streamlit app on Hugging Face Spaces, paste a passage and see severity-scored hits.
- [Lakera Gandalf](https://gandalf.lakera.ai/) - Interactive game for designing prompts that bypass guardrails.

## GitHub Actions for CI

Plug into pull-request flows.

- [rag-guardrails-action](https://github.com/MukundaKatta/rag-guardrails-action) - Composite Action wrapping prompt-injection-shield + vector-poison-score. Fail on high severity, warn on medium.

## Research papers and preprints

- [Small-Rule Guardrails for Retrieval-Augmented Generation](https://zenodo.org/records/20057632) - Mukunda Rao Katta. Zenodo + Figshare DOI. Companion to prompt-injection-shield.
- [Greshake et al., Not what you've signed up for](https://arxiv.org/abs/2302.12173) - Foundational paper on indirect prompt injection.
- [Perez and Ribeiro, Ignore Previous Prompt](https://arxiv.org/abs/2211.09527) - Early study of prompt injection.
- [Liu et al., Prompt Injection Attacks and Defenses in LLM-Integrated Applications](https://arxiv.org/abs/2310.12815) - Systematisation of attack and defense space.

## Adjacent reliability tooling

Not strictly prompt-injection but commonly composed with it.

- [APort](https://github.com/aporthq/aport-integrations) - Open-source integration toolkit for APort, a neutral trust rail for AI agents.
- [agentvet](https://github.com/MukundaKatta/agentvet) - Validate LLM tool-call arguments before execution.
- [agentguard](https://github.com/MukundaKatta/agentguard) - Network egress firewall for tool-using agents.
- [agentcast](https://github.com/MukundaKatta/agentcast) - Validate-and-retry loop for structured outputs.
- [agentsnap](https://github.com/MukundaKatta/agentsnap) - Snapshot tests for tool-call traces.
- [agentfit](https://github.com/MukundaKatta/agentfit) - Token-aware message truncation.

## Background reading

- [OWASP LLM Top 10: LLM01 Prompt Injection](https://owasp.org/www-project-top-10-for-large-language-model-applications/) - The community baseline.
- [Simon Willison: Prompt injection](https://simonwillison.net/series/prompt-injection/) - Long-running blog series with field reports.
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) - Government view on LLM risk categories.

## Contributing

Send a pull request. Each entry should:
1. Already exist (no vaporware or roadmaps).
2. Be free or have a meaningful free tier.
3. Have a one-line description of what makes it useful, not just a name.

Sort within each section alphabetically, except where the order is meaningful.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the maintainer has waived all copyright and related rights to this list.
