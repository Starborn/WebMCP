28 February 2026   *feel free to discuss, repost  

FROM PDM W3C AI KR CG TO ALL  *Shared on w3c webMCP  and AI KR CG public mailing lists 
Posted  https://lists.w3.org/Archives/Public/public-aikr/2026Feb/0015.html  

As of Feb 28, WebMCP is a draft specification with empty security and accessibility sections.

It is not a W3C Standard. Commercial products and services are already availableWebMCP is a proposed browser API being incubated by the W3C Web Machine Learning Community Group. It allows websites to expose JavaScript functions as structured tools that AI agents can discover and invoke. Chrome 146 ships an early preview behind a feature flag. The draft is dated 27 February 2026.The spec itself states: "It is not a W3C Standard nor is it on the W3C Standards Track."(Source: https://webmachinelearning.github.io/webmcp/)Security and Privacy?The specification's Security and Privacy section is empty.
It contains only a TODO comment linking to a separate document.

The Accessibility section is completely empty -- no text at all. All four core API method definitions say "TODO: fill this out."This means there is currently no normative guidance on how browsers should handle prompt injection through tool descriptions, how users should be informed when tools are registered on a page, how cross-origin tool data should be isolated, what consent model should govern agent-to-tool interaction, or how WebMCP tools relate to the existing accessibility tree.(Source: https://github.com/webmachinelearning/webmcp/blob/main/index.bs)

Already on the Market?Multiple commercial ventures have launched products and services around WebMCP within days of the Chrome preview. These include paid "Agent Readiness" assessments, enterprise security scanners, CLI audit tools, CMS plugins, and partner programs -- all built on a specification that has not defined its own security model.Businesses are being told to annotate their forms with WebMCP attributes so AI agents can submit them programmatically. Fear-of-missing-out marketing frames this as "SEO for AI" and warns that companies who do not implement WebMCP will be "skipped by agents."

This is premature. The security implications of exposing website functionality to autonomous agents through a browser API without a defined consent model, permission framework, or threat analysis have not been resolved by the standards body.

Selling security tooling for a threat model that does not yet exist is not responsible engineering.What WebMCP Is NotWebMCP is not the Model Context Protocol (MCP). It does not implement the MCP wire protocol (JSON-RPC 2.0). It is not interoperable with MCP client libraries. It borrows the tool abstraction -- functions with schemas and descriptions -- but implements everything through browser-native mechanisms. The name creates confusion that is being commercially exploited.(See Technical Note 3: https://github.com/Starborn/webmcp/blob/main/WebMCnotMCP.md)What You Should DoIf you are a developer: contribute and experiment with the Chrome preview, but do not deploy WebMCP tools on production sites until the security model is defined.If you are buying services: no commercial product can deliver WebMCP security compliance because the spec has not defined what compliance means.If you are a standards participant: the W3C Web Machine Learning Community Group meets next on 5 March 2026. Comments can also be submitted via the public mailing list (public-webmachinelearning@w3.org) or as GitHub issues (https://github.com/webmachinelearning/webmcp/issues). 

The window for meaningful input is now.ReferencesW3C Draft Spec: https://webmachinelearning.github.io/webmcp/Spec Source (index.bs): https://github.com/webmachinelearning/webmcp/blob/main/index.bsSecurity/Privacy Doc (separate, not in spec): https://github.com/webmachinelearning/webmcp/blob/main/docs/security-privacy-considerations.mdTechnical Notes 1-3: https://github.com/Starborn/webmcp/W3C CG Mailing List: public-webmachinelearning@w3.orgIssue Tracker: https://github.com/webmachinelearning/webmcp/issues. Corrections and discussion welcome.


SEE ALSO SUGGESTED EDITS BELOW SUBMITTED AS PRs and to the web machine learning mailing list

PR 1 -- Clarify MCP analogy in Introduction (line 84)   trying to submit as PR on ghub now!!

Current text (line 84):

    Web pages that use WebMCP can be thought of as Model Context Protocol [[!MCP]] servers that implement tools in client-side script instead of on the backend.

Suggested edit:

    Web pages that use WebMCP can be thought of as analogous to Model Context Protocol [[!MCP]] servers in that they expose callable tools, but WebMCP implements tool discovery, registration, and invocation through browser-native mechanisms rather than the MCP wire protocol.

Source: TN3 (WebMCnotMCP.md) -- "A Suggested Clarification" section. This is the single most important edit.


PR 2 -- Add note to Security section (lines 98-103)

Currently empty except a TODO comment. Add a non-normative note:

    Note: WebMCP's threat model differs from that of backend MCP servers. Security review should address client-side JavaScript execution, browser origin-based trust boundaries, prompt injection via tool descriptions and responses, and silent tool registration, rather than importing assumptions from backend protocol security models.

Source: TN3 "Why This Matters for Standards Review" + TN2 risk sections on prompt injection and consent model gaps.

PR 3 -- Add note to Accessibility section (line 105)

Currently completely empty. Add a non-normative note:

    Note: WebMCP tools introduce a second machine-readable description of page functionality alongside the accessibility tree. Implementations should consider how tool descriptions relate to existing ARIA roles and properties to avoid divergence between the two representations.

Source: TN2 accessibility testing section + existing issue #91 (Redundancy with the accessibility tree) + issue #65 (Accessibility via agentic interfaces).

PR 4 -- Clarify agent definition scope (line 92)    submitted as PR  by starborn on 28 Feb

Current text:

    An <dfn>agent</dfn> is an autonomous assistant that can understand a user's goals and take actions on the user's behalf to achieve them. Today, these are typically implemented by large language model (LLM) based [=AI platforms=], interacting with users via text-based chat interfaces.

Suggested addition after the existing sentence:

    An <dfn>agent</dfn> is an autonomous assistant that can understand a user's goals and take actions on the user's behalf to achieve them. Today, these are typically implemented by large language model (LLM) based [=AI platforms=], interacting with users via text-based chat interfaces. In the context of this specification, agents operate within or in coordination with an active browser session where a human user is present.

Source: TN3 operational mode distinction + the spec's own non-goal of headless browsing scenarios (README).

PR 5 -- Add interoperability note to the MCP bibliography entry (lines 292-298)

After the biblio entry for MCP, add a note to the Introduction or Terminology:

    Note: While WebMCP borrows the tool abstraction from the Model Context Protocol [[!MCP]], it does not implement the MCP wire protocol (JSON-RPC 2.0) and is not interoperable with MCP client libraries at the transport level.

Source: TN3 transport section -- developers expecting protocol-level interoperability will be misled.

    PR 4 (agent definition scope) -- smallest, least controversial, clarifies existing text     DONE
    PR 1 (MCP analogy clarification) -- the core issue, directly addresses TN3     DOING
    PR 5 (interoperability note) -- technical clarification, low friction
    PR 3 (accessibility note) -- fills an empty section, aligns with issue #91
    PR 2 (security note) -- fills an empty section, more substantive
