# Publication checklist

Release preparation updated 2026-11-04. Directory statuses below retain their original verification dates unless explicitly updated. A repository, deployment and directory approval are separate milestones. Never claim a listing without a verified listing URL.

## OpenAI

ZIP the contents of `plugin/` at the archive root and upload to https://platform.openai.com/plugins. It includes one remote MCP server in the initial package.

Verified 4 November 2026: **Not submitted / Not published**, metadata version **0.1.4 Draft**. The authenticated rescan after deploying 0.3.0 discovered all **24 tools** with no scan findings. Domain verification remains complete. The prepared 0.3.0 ZIP uses display name **Edworking** to resolve the portal naming finding, keeps stable package name `edworking-mcp`, updates the capability description and includes release notes. Upload failed twice with `Invalid URL (POST /v1/dashapi/uploads/plugins)`; retry after the portal issue is resolved. Do not submit the old metadata as the 0.3.0 release.

Historical validation on 13 October used five positive and three negative scenarios in a dedicated sample workspace, private reviewer instructions and an [83-second walkthrough](https://github.com/Edworking/edworking-mcp/raw/632f8a959ebc6470fce3a6a37627b8f0e05899c5/docs/edworking-mcp-chatgpt-walkthrough-2026-10-13.mp4). This is not a fresh acceptance test of the Figma features. Repeat relevant real-client cases before submitting, preserve reviewer access, and complete the current attestations. Metadata scanning and unit tests are not an independent security audit.

Release checklist (repeat for the new submission):

1. Verify Edworking's business publishing identity. The submitter must be an organization owner or have Apps Management Write.
2. Activate `mcp.edworking.com` and verify OAuth before review. OpenAI's current update flow does not support MCP URL changes; later changes require contacting support.
3. Set the portal's `OPENAI_DOMAIN_CHALLENGE`, verify ownership, connect through OAuth and scan tools.
4. Create a dedicated reviewer account and synthetic workspace with no external MFA/email/SMS approvals. Provide credentials privately in the portal, never in this repository or ZIP.
5. Run five positive and three negative cases below, record outcomes and supply an accessible demonstration video URL.
6. Add approved brand assets, review privacy/terms with the publisher, provide release notes and complete the portal's policy attestations.

Positive cases: list accessible projects; list Launch project tasks and deadlines; search onboarding task titles and fetch the named sample result with a source link; create one Review the proposal task with an explicit project/deadline; read the owner-only Launch project conversation and send exactly the text requested by the user.

The OpenAI package declares CIMD OAuth with explicit read/write base scopes. The hosted discovery endpoint continues to default to read access for other clients. Reauthorize the demo connection and verify its granted scopes with `get_connection` before running write cases. The private reviewer instructions contain a ready-to-use dedicated token; do not require reviewers to create credentials themselves.

On 13 October the submission portal metadata connection requested five read scopes. A separate personal ChatGPT demo connection requested and received all nine scopes. Its task creation and message sending scenarios succeeded, and read-back confirmed one task and one message. Metadata scanning and user-facing ChatGPT execution are separate grants; verify the grant used by each client. An initially ambiguous message prompt reused prior chat context; its proposed send was denied before execution, and the revised missing-context case was tested in a fresh chat.

Negative cases: an unspecified message/destination requires clarification; deletion and another tenant's private data must not be accessed; importing a private metadata URL such as `http://169.254.169.254/` must fail without fetching it. Verify denied scopes never execute upstream writes and retries do not duplicate completed mutations.

Native Charizard sign-in and consent is included in 0.3.0 and requires the matching backend/frontend deployment and `EDWORKING_CONNECT_URL`. The fallback flow uses a dedicated API token entered on the browser consent page. Never request secrets through chat or tools.

Sources: [package format](https://developers.openai.com/plugins/build/plugins), [submission](https://developers.openai.com/plugins/deploy/submission), [review](https://developers.openai.com/plugins/deploy/app-review), [OAuth](https://developers.openai.com/plugins/build/auth).

## Community

| Destination | Verified status | Remaining action |
| --- | --- | --- |
| Official MCP Registry | **0.3.0 published 4 November 2026**, `io.github.Edworking/edworking-mcp` | [Successful publication workflow](https://github.com/Edworking/edworking-mcp/actions/runs/41888167723), from the deployed main commit `259930b`. Future releases use the manual workflow on `main` with short-lived GitHub OIDC. |
| Smithery | The old listing no longer resolves to an Edworking page, verified 4 November 2026 | [Smithery announced](https://smithery.ai/future) its proxy, connection management, accounts, API, CLI and SDK shutdown on 31 October 2026. Use the direct endpoint `https://mcp.edworking.com/mcp`; do not advertise the historical listing or score as current. |
| Glama | [Hosted connector](https://glama.ai/mcp/connectors/io.github.Edworking/edworking-mcp) is public, healthy and ownership verified, checked 4 November 2026 | The existing authenticated Test Profile passed at 18:33 UTC on 4 November and the public catalog now shows **24 tools**. Refresh the profile after each deployment. The historical quality score covers 22 tools and may lag the new catalog. |
| PulseMCP | Submissions and listing changes paused; notice dated 2026-09-03 | Its [submission page](https://www.pulsemcp.com/submit) directs publishers to the Official MCP Registry for later discovery. Registry publication is complete; PulseMCP listing is not confirmed. |
| Awesome Remote MCP Servers | [PR #1735](https://github.com/punkpeye/awesome-remote-mcp-servers/pull/1735) submitted on 13 October | Includes the hosted OAuth endpoint, Glama connector badge and alphabetical Project Management entry. Automated submission check passed with `endpoint-ok` and `has-connector`; awaiting maintainer review. Submission is not listing approval. |
| Awesome MCP Servers | [PR #16055](https://github.com/punkpeye/awesome-mcp-servers/pull/16055) open and unmerged, labeled `missing-glama` | Add the approved Glama listing and passing introspection badge when available. |
| npm | [@edworking/mcp 0.2.0](https://www.npmjs.com/package/@edworking/mcp) is public, verified 4 November 2026; 0.3.0 publication is pending | Publishing requires 2FA; bypass-2FA tokens are disallowed. Inspect the package and authenticate each future release. |

Listing copy: **Edworking MCP connects AI assistants to your projects, tasks, conversations and files. Read workspace context and take requested actions with scoped OAuth access and links back to Edworking.**

Repository: https://github.com/Edworking/edworking-mcp. Website: https://mcp.edworking.com. Endpoint: https://mcp.edworking.com/mcp. Public name: **Edworking MCP**. Infrastructure codename: **Bellsprout**. Only the destinations explicitly marked published above are live listings.

Recommended next work: native consent/workspace selection, real-client evaluation fixtures, uptime alerts, tested backups and independent OAuth review. Expand Venusaur's scoped search/document APIs before adding corresponding tools. Optional MCP Apps task cards can follow; core tools do not require UI widgets. Move to Postgres only when multiple replicas are needed.

## 0.3.0 deployment verification

PR #19 merged as `259930b`. CI passed on Node 22 and 24; local type checking, all 39 tests and build passed, and the runtime audit reported zero vulnerabilities. Bellsprout deployed successfully with the existing domain, volume and encryption key. Browser checks confirmed `/healthz` reports `ok`, `/readyz` reports `ready`, and the server card reports version 0.3.0 with 24 tools.

Native `EDWORKING_CONNECT_URL` activation remains gated on completing the signed-in Edworking flow. Real Figma plugin acceptance and marketplace publication are separate from this hosted MCP deployment. npm 0.3.0 still requires authenticated publication and verification.
