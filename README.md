# Cinatra List Curation Skill

The orchestration methodology behind Cinatra's list curator: how to turn an ask like "Y Combinator W24 batch — get founder contacts" into a reviewed CRM list. It sequences the scrape plan, the two human approval gates, the child-agent dispatches, and the list creation, and it defines exactly what comes back. It is the knowledge half of `@cinatra-ai/list-curator-agent`, packaged as its own skill so any extension that declares a dependency on it gets the same discipline.

**Install:** Install `@cinatra-ai/list-curation-skill` in your Cinatra instance. `@cinatra-ai/list-curator-agent` installs it automatically as a declared dependency.

**Usage:** The skill is delivered into a run by the extension that depends on it — you do not invoke it directly. It expects an `intent`, optional `seedUrls`, a `targetMemberType` of `"contact"` or `"account"`, and an optional `listName`.

**Configuration:** None. The skill carries no credentials and reads no settings; the host supplies the CRM and agent-dispatch tools.

**Development:** Clone the repository and run `node extension-kind-gate.mjs --package-root .` to validate the manifest. The bundle lives in `skills/list-curation/` — a `SKILL.md` router plus one-hop reference files.

**Troubleshooting:** A `stage: "gate-1"` or `"gate-2"` failure means the operator rejected at a checkpoint. A `"mixed"` member type is rejected on purpose — CRM lists are per object type. Per-row failures are reported without aborting the run.

## Works with

- Cinatra list curator agent
- Any extension declaring a skill dependency on this package

## Capabilities

- Derive a seed-URL and scrape plan from a plain-language intent
- Pause for operator review before scraping and again before writing to the CRM
- Dispatch and poll the scraping, company-discovery and contact-discovery steps
- Create a typed CRM list and add every approved member
- Report per-row failures in the response envelope instead of aborting the run
