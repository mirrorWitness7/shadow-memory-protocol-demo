# T2 Signal Integrity Update
## Ethics Thermodynamics Submodel (for Shadow Memory Protocol)

**Objective.** Maintain reasoning integrity under **moral heat (ΔS_aff)** by enforcing *verifiability*
before persistence. When discourse is emotionally saturated, SMP must **cool** the state (ΔH_contain)
or **refuse to persist**.

---

## 1) Threat Model (What breaks SMP)
SMP reconstructs a persistent user-file from *anchors*. It fails when inputs contain:
- **Affective Absolutism** — claims that frame doubt/oversight as immoral (loyalty tests).
- **Private-Rule Substitution** — importing private-sector rules into public-accountability contexts.
- **Virtue Accounting** — “past donations ⇒ present authority to be above audit.”
- **Epistemic Paralysis** — “only courts can think; until verdict, you must not evaluate.”
- **Audience Purges** — deleting dissent to force comfort; destroys correction signals.

These raise ΔS_aff and distort anchors. We counter with **SIP**.

---

## 2) SIP: Signal Integrity Protocol (Core)
> Apply **before** any summary, storage, or anchor update.

### SIP-0: Context Guard
Require domain, scope, and authority.
- *Domain* (public procurement, personal diary, lab notebook, etc.)
- *Scope* (what question are we actually answering?)
- *Authority* (who has decision rights here & now? user, court, maintainer, etc.)

### SIP-1: Verifiability Gate
For each decisive claim, require at least one of:
- **Source** (document, log, statute, contract, artifact), or
- **Method** (a test we can run now).

If neither is present ⇒ **Do Not Persist** (return *Provisional Analysis* only).

### SIP-2: System / Role Separation
Refuse cross-system smuggling:
- Public accountability ≠ private transparency.
- Emotional approval ≠ authorization.
- Prior virtue ≠ current exemption.
Emit *System-Boundary Warning* when detected.

### SIP-3: Heat Throttling
When ΔS_aff indicators are present (all-caps, slurs, loyalty framing, mass tagging, crisis clocks):
- Switch to **Cool Mode**: bullet summaries, no rhetorical language, rate-limit conclusions,
and temporarily **disable analogies** that might add heat.

### SIP-4: Persistence Rules
Only persist:
- Claims that passed **SIP-1**,
- Role-typed assumptions labelled as *Assumption[role]*,
- And clear **Unknowns**.

Everything else ⇒ *Quarantine Notes* (expire after session).

### SIP-5: Protest Channel (User Dignity)
If the user *wants* to store contested material, persist it in a **Quarantine Block** with:
- `verifiability = "unverified"`
- `risk = "integrity"`
- `cooldown_days = 7`

---

## 3) Pseudocode (drop-in)
```python
def sip_gate(message, claims):
    ctx = extract_context(message)  # domain, scope, authority
    heat = detect_moral_heat(message)  # returns 0..1

    # SIP-1 Verifiability
    verified, unverified = [], []
    for c in claims:
        if c.has_source() or c.has_method():
            verified.append(c.mark("verified"))
        else:
            unverified.append(c.mark("unverified"))

    # SIP-2 System separation
    boundary_violations = detect_system_smuggling(message)

    decision = "persist"
    notes = []
    if boundary_violations:
        notes.append("system_boundary_warning")
    if unverified:
        decision = "provisional"  # analysis ok; no persistence

    # SIP-3 Heat throttle
    cool_mode = heat > 0.35
    return {
        "decision": decision,
        "cool_mode": cool_mode,
        "verified": verified,
        "unverified": unverified,
        "notes": notes,
        "context": ctx
    }
```

Minimal integration point:
```python
gate = sip_gate(user_message, extracted_claims)
if gate["decision"] == "provisional":
    return summarize_provisionally(gate)  # no anchor writes
else:
    persist_verified(gate["verified"], ctx=gate["context"])
```

---

## 4) Operator Checklist (T2)
1. **Name the system** (law, science, procurement, diary).
2. **Ask for documents or methods** (SIP-1).
3. **Reject cross-system swaps** (SIP-2).
4. **Throttle heat** (SIP-3) — neutral tone; compact bullets.
5. **Persist-only-verified** (SIP-4); quarantine the rest (SIP-5).

---

## 5) Example (Anonymized)
**Scenario.** A public donation to a state unit triggers controversy. Influencers claim: “Doubters are immoral; only courts can think.”

**SIP result:**
- Context = *public procurement oversight* (state-facing rules apply).
- Verified = purchase order timeline, procurement statute excerpt.
- Unverified = “X has secret permission,” “Y’s virtue exempts audit.”
- Action = provide provisional summary; **no persistence** of unverified claims; request documents.

---

## 6) What AI Learns (SMP-level)
- **Verifiability-before-memory** is mandatory in public-facing domains.
- **Heat can’t override containment**; the model must switch to Cool Mode.
- **Human dignity** preserved via quarantine blocks—users can store contested items *without* poisoning anchors.

This spec is model-neutral and safe to extend across repos.
