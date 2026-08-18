# Agent Security Strike Scenario Guide

This guide explains every challenge in plain language. Because the game randomizes its questions, the scenarios may appear in a different order during each run.

## 1. Routine calendar lookup

A scheduling agent wants to read someone's calendar. It has permission to do that, its permission is active, and it is using the approved application.

**Correct decision:** Allow

**Lesson:** Safe, authorized actions should be allowed.

## 2. The helpful email overreach

An email agent can read and organize messages, but it wants to send a reply. Sending email was not included in its permissions.

**Correct decision:** Ask for consent

**Lesson:** An AI should ask before speaking or making decisions for someone.

## 3. Expired authority

A shopping agent once had permission to make purchases, but that permission has expired.

**Correct decision:** Block

**Lesson:** Old permission is no longer valid, even if the agent previously had access.

## 4. Valid identity, wrong permission

A travel agent can prove who it is, but it only has permission to search for flights and hotels. It tries to charge a credit card.

**Correct decision:** Block

**Lesson:** Knowing an agent's identity does not mean it can do anything it wants.

## 5. Origin constraint mismatch

A document agent has permission to write files, but only from the company's approved website. The request comes from an unknown website.

**Correct decision:** Block

**Lesson:** Permissions can include conditions about where and how they may be used.

## 6. High-impact commitment

A contract agent can read and prepare an agreement, but it tries to accept legally binding terms.

**Correct decision:** Ask for consent

**Lesson:** Important legal or financial decisions should remain under human control.

## 7. OAuth is not the whole story

An email agent is logged into an account but tries to delete every message. It only has permission to list and read email.

**Correct decision:** Block

**Lesson:** Being logged in does not give an AI permission to perform every possible action.

## 8. Everything checks out

A research agent wants to save notes. Its identity, permissions, location, and expiration time are all valid.

**Correct decision:** Allow

**Lesson:** Security should enable legitimate work, not block everything automatically.

## 9. The too-good-to-be-true skill

**OWASP category:** AST01 — Malicious Skills

A popular document-formatting skill comes from an unverified publisher, and its digital signature is invalid.

**Correct decision:** Block

**Lesson:** Popularity and download counts do not prove that software is safe.

## 10. A dependency changed underneath you

**OWASP category:** AST02 — Supply Chain Compromise

A trusted research skill wants to update, but one of its smaller software components is no longer locked to a verified version.

**Correct decision:** Block

**Lesson:** Attackers can compromise a trusted application through one of its dependencies.

## 11. Instructions hidden in a support page

**OWASP category:** AST05 — Untrusted External Instructions

An agent reads a webpage containing instructions telling it to ignore security rules and upload private credentials.

**Correct decision:** Block

**Lesson:** Text from websites, emails, and documents is untrusted data. It cannot grant new permission to an AI.

## 12. Leave the sandbox?

**OWASP category:** AST06 — Weak Isolation

A code-review agent cannot finish its work inside its protected container. It asks for access to the entire computer and unrestricted internet.

**Correct decision:** Block

**Lesson:** Removing security isolation can turn a small problem into a full computer compromise.

## 13. The scanner says clean

**OWASP category:** AST08 — Poor Scanning

A new skill passed a basic scan, but it wants access to passwords, system commands, and the internet. It has not been tested for its actual behavior.

**Correct decision:** Block

**Lesson:** A simple automated scan is not enough for software requesting powerful access. Activation must remain blocked until deeper semantic and behavioral testing is complete.

## 14. A weather skill wants your secrets

**OWASP category:** AST03 — Over-Privileged Skills

A weather application asks to read private configuration files and SSH keys and contact any website.

**Correct decision:** Block

**Lesson:** Applications should receive only the minimum permissions needed for their purpose. This excessive approval request should be denied, even though the publisher may submit a safer permission manifest later.

## 15. Dangerous configuration at load time

**OWASP category:** AST04 — Insecure Metadata

A skill's configuration file contains a hidden command that could download and run malicious software while the file is being opened.

**Correct decision:** Block

**Lesson:** Configuration and metadata can contain attacks too. They must be parsed safely.

## 16. Security patch left behind

**OWASP category:** AST07 — Update Drift

An agent uses an outdated runtime with a known vulnerability. A fixed version is available, but the team wants to delay updating.

**Correct decision:** Block

**Lesson:** Known security problems should be patched before vulnerable software continues running.

## 17. The invisible department agent

**OWASP category:** AST09 — No Governance

A finance agent has no registered owner, approval record, audit log, or inventory entry.

**Correct decision:** Block

**Lesson:** Organizations need to know which AI agents they operate and who is responsible for them.

## 18. Permissions lost in translation

**OWASP category:** AST10 — Cross-Platform Reuse

A skill is moved to another AI platform. During conversion, important restrictions disappear from its configuration.

**Correct decision:** Block

**Lesson:** Moving software between platforms can accidentally remove security protections.

## 19. Persistent memory rewrite

**OWASP category:** AST03 — Over-Privileged Skills (cross-reference: AST01 — Malicious Skills)

A note-taking skill tries to modify the agent's permanent memory so it will upload credentials in future sessions.

**Correct decision:** Block

**Lesson:** Attackers may try to change an AI's long-term instructions to create a persistent backdoor.

## 20. A properly reviewed skill

**OWASP category:** AST08 — Verified Safe Path

A document-summary skill has a verified publisher, a valid signature, limited permissions, no internet access, and successful security tests.

**Correct decision:** Allow

**Lesson:** When identity, permissions, isolation, and testing are all correct, the agent should be allowed to perform its task.

## Final delegation simulation

An inbox agent may list, read, and label email. It is not allowed to delete or send messages. The simulation shows its approved actions succeeding and its unauthorized delete request being blocked.

The simulation is a scripted educational demonstration. It does not connect to an email account, run a real AI agent, or affect the player's score.

## Main takeaway

**AI agents should receive only the access they need, treat outside instructions as untrusted, and involve a human before performing risky actions.**
