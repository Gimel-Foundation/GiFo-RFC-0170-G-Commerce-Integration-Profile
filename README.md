# GiFo-RFC-0170 (V0.9.2 - Working Draft – Under Review)

G-Commerce Integration Profile - Combined Credential- and Platform-bound Enforcement (CCPE-F)

New Request for Comments of Gimel Foundation (GiFo RFC) - Establishung G-Commerce Integration Profile - Combined Credential- and Platform-bound Enforcement (CCPE-F)

Abstract of RFC: CCPE-F (G-Commerce) is the commerce-authorization profile of the GAuth framework. It lets an autonomous agent transact with a vendor on a principal's behalf under a signed delegation credential, while the vendor's own platform-side checks still apply.
The profile defines:

•	a Commerce-Mandate envelope (a Power-of-Attorney credential per RFC 0115, specialised for commerce);

•	a three-phase decision surface - mandate → cart → payment — with order-preservation as an integrity invariant;

•	a bipolar enforcement chain — Power-PEP (credential-bound, Phase 1) followed by Commerce-PDP (platform-bound, Phase 2), reconciled by more-restrictive-wins;

•	a per-Phase-2-call metering hook with three open-core symmetry invariants;

•	a single normative integration scenario over the Universal Commerce Protocol (UCP) substrate via a Foundation-owned vendor-extension capability, with informative cookbooks for Stripe, Shopify, Amazon Pay, Open Banking / PSD2, and the W3C Payment Request API.

•	a deployment-scenario taxonomy — S1 (pure platform-native, no Foundation artefact), S2 (two-artefact via the §4 UCP vendor-extension capability, Recommended and the conformant scenario), S3 (all-in-one merged-credential where the vendor extends its native payment artefact with PoA-shape attributes inline) - with the in-scope-of-RFC ≠ conformant-to-G-Commerce distinction made explicit;

•	a seven-disadvantage structural critique of the S3 single-artefact shortcut (cap-and-scope drift, missing principal-delegation event, three-phase chain absence, lifecycle entanglement, cross-vendor interoperability break, governance-model-vs-credential-format category error, and the Phase-2 artefact-discipline cannot-supply-Phase-1 result) closing with an explicit non-conformance statement;

•	a scenario-keyed conformance mapping (§4.5a) requiring every G-Commerce Conformance Statement to name its deployment scenario, with the audit-trail field `ccpe_f_scenario` reserved on the wire.

Status of unresolved items, presentation gaps (JSON-Schema/CDDL formalisation, additional vendor cookbooks, Strict / Behörde profile bodies, PQC migration, regulator-bound audit-export format) is enumerated at §13.

Three things that make this profile distinct from a "just present a JWT" flow:

•	Three sequential mandates (mandate / cart / payment), each parent-bound, so the principal's delegation can't be silently widened mid-flow.

•	Two-stage enforcement — the Power-PEP enforces what the principal delegated; the Commerce-PDP enforces what the vendor's platform allows. The stricter of the two wins. A Phase-1 deny short-circuits Phase 2.

•	Cascade revocation — revoking any mandate at the Authority cancels in-flight platform-side artifacts (PaymentIntents, ChargePermissions, carts) and emits commerce.cascade.revoked.

If the Commerce-PDP doesn't answer within phase2_timeout_ms, the mandate's fail_disposition decides: fail_closed denies; fail_drop_payment_only denies payment-class actions but lets non-payment actions through if Phase 1 already permitted.




You are more than welcome to contribute !

Legal Provisions for users of this page

Please see the Legal Provisions under https://gimelfoundation.com

In particular the following terms apply:

GiFo RFC 0080 Legal Provisions for the Gimel Foundation

GiFo RFC 0090 Legal Provisions Related to Gimel Foundation Documents

GiFo RCC 0100 Rights Contributors Provide to the Gimel Foundation
