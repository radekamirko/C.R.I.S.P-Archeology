# Architecture Map

**Owner:**  
**Review date:**  
**Status:** ❓ Draft / ✅ Validated

---

## System diagram

```
[Component A] ──── (trigger: event/schedule/request) ───► [Component B]
      │                                                          │
      ▼                                                          ▼
[External: Stripe]                                     [Database: Postgres]
```

*Replace with actual components. Use ❓ on arrows you're unsure about.*

---

## Component register

### [Component Name]
- **Responsibility:** What it owns. One sentence.
- **What breaks if it dies:** The honest answer.
- **Owned by:** Team / person / contractor (if known)
- **Status:** ✅ Active / ❓ Unknown / ⚠️ Appears abandoned

### [External: Service Name]
- **Type:** Third-party API / payment processor / auth provider / etc.
- **What data it provides/receives:**
- **Direction:** Inbound / Outbound / Both
- **Trigger:** Event / Schedule / Webhook / Manual
- **Format:** JSON / CSV / etc.
- **Risk if unavailable:**
