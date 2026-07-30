Task 2 — WhatsApp Lead-to-Booking Automation (Phase 1: Design + Sandbox Setup)

Track: AI Automation · Mentor: Afnan Shoukat Niche chosen: Dental Clinic — "BrightSmile Dental Clinic"

What this phase covers

This phase focused on designing the full conversation flow for a WhatsApp booking bot before writing any bot logic, and getting the technical pipes connected (Meta WhatsApp Cloud API sandbox → n8n via webhook) so Phase 2 can build directly on top of a working, verified connection.

Files in this folder
assets/flow-diagram.mermaid — full conversation flow: language detection, greeting/intent, FAQ loop, service selection, timing, slot offering, confirmation, no-reply nudges, and human handoff.
messages.md — every bot message written in both English and Arabic (States 1–5, all 3 nudges, and the handoff message), plus a reusable config object.
assets/webhook-test-screenshot.png — proof that a WhatsApp message payload successfully reached the n8n webhook via the Meta Cloud API sandbox.
workflow.json — the exported n8n workflow used for this webhook test.
Why the human handoff step matters

The bot is only ever allowed to operate inside its scripted lane: greetings, service selection, timing, and booking confirmation. The moment a conversation touches something with real consequences — a medical/health question, a complaint, or price negotiation — it hands off to a human instead of improvising. A wrong medical answer could genuinely harm a patient or expose the clinic to liability, an unhandled complaint can lose a customer for good, and an improvised discount undercuts the business. Keeping the bot's authority narrow and routing anything sensitive to a real person is what makes this safe to deploy for a real client.

Bilingual behavior

State 0 checks every incoming message for Arabic script. If Arabic characters are detected, the bot replies in Arabic from that point on; if not, it replies in English. This check runs on every incoming message (not just the first one), so if a user starts in Arabic and later switches to English mid-conversation, the bot detects the switch and replies in the new language going forward — no restart needed.

Sandbox / webhook notes
Meta Cloud API sandbox (Business Manager: "British Smile Dental Clinic") is connected to a local n8n instance, tunneled through a static ngrok domain.
Verification handshake (GET request with hub.challenge) is handled by a dedicated Webhook + IF + Respond to Webhook node chain.
Incoming message delivery (POST) is handled by a second Webhook node on the same path.
Since the Meta app is still unpublished (expected for a sandbox/dev phase), real end-user phone messages aren't yet delivered — but Meta's own dashboard "Send to server" test tool was used to confirm the full pipeline works end-to-end, which is what this phase requires.
Real end-to-end phone delivery will require publishing/verifying the app, which is planned for a later phase alongside the real calendar integration.

