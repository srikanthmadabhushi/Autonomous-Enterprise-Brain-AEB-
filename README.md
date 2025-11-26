# Autonomous-Enterprise-Brain-AEB-
AI-Orchestrated Decision Engine for ServiceNow
> Part of **SN AI Innovation Lab** by **Srikanth Madabhushi**  
> A simulation of an AI “brain” that watches enterprise signals, takes decisions, logs actions, learns patterns, and surfaces insights – built fully on a ServiceNow Developer Instance.

---

## 🔥 1. What is this project?

**Autonomous Enterprise Brain (AEB)** is a ServiceNow application that behaves like a **central AI decision engine** for the enterprise.

Instead of handling Incidents, HR cases, CSM cases, etc. separately, AEB:

1. **Listens** to important events (signals) from IT operations and other domains  
2. **Decides** what to do using AI-style logic (simulated via Script Includes & Business Rules)  
3. **Executes / Logs actions** taken on those signals  
4. **Tracks approvals, audits, knowledge, and patterns** over time  
5. **Presents a Command Center & Insight Dashboard** to review everything

It is designed as a **concept / prototype** to show how an enterprise could build an **AI Brain on top of ServiceNow**, even using a free **Developer Instance**.

---

## 🧠 2. Key Concepts

AEB is built around a simple but powerful idea:

> **Signal → Decision → Action → Insight**

- **Signals** = important events (e.g., critical Incidents, HR or CSM-like issues)  
- **Decisions** = what the AI Brain thinks should happen  
- **Actions** = what actually gets done (or is proposed to be done)  
- **Insights** = what the system learns over time (knowledge graph, patterns, audits, etc.)

---

## ⚙ 3. Main Features (Phases Summary)

### Phase 1 – Core Brain (Signal → Decision → Action Log)
- Custom app: **SN AI Innovation Lab**
- Core tables:
  - `u_aeb_enterprise_signal` – stores incoming signals
  - `u_aeb_decision` – stores AI decisions for each signal
  - `u_aeb_action_log_table` – stores action logs linked to decisions
- Integration with **Incident**:
  - When a **Priority 1** Incident is created, AEB automatically:
    - Creates an **AEB Enterprise Signal**
    - Runs the **AEB_Engine** Script Include
    - Creates a related **AEB Decision**
    - Creates a related **Action Log**

### Phase 2 – AEB Command Center (Dashboard v1)
- Navigation modules under **AI Innovation Lab**:
  - AEB Enterprise Signals
  - AEB Decisions
  - AEB Action Logs
- Command Center dashboard (new UI) with:
  - **Data Visualization** – Decisions by Severity
  - **List – Simple** – Latest Signals

### Phase 3 – Multi-Domain Signals (IT + “HR/CSM-style”)
- Extended the Signal model to support **different source types** using `source_type` choice:
  - `incident`
  - `hr_case` (simulated)
  - `cs_case` (simulated)
- Business Rules route different sources into `u_aeb_enterprise_signal`  
- AEB_Engine can behave differently based on:
  - Priority
  - Source type
  - Risk text

### Phase 4 – Governance & Manual Action Trigger
- Added UI Action(s) on **AEB Decision**:
  - Example: **Generate Action Log**
- Governance concept:
  - Decisions can be approved/rejected (via `approved` + `approver` fields)
  - Only approved decisions may trigger further actions

### Phase 5 – Decision Audit Trail (AEB Decision Audits)
- Additional table to track **audit records** for decisions over time  
- Business Rule(s) create audit entries when:
  - A decision changes status / approval
  - Important fields change (severity, explanation, etc.)

### Phase 6 – Advanced Action Controls
- Additional logic in Action Logs to:
  - Track status (`pending`, `completed`, `failed`)
  - Allow AEB to re-run actions or log manual interventions

### Phase 7 – Extended Governance & Review (Approvals + UI)
- UI Actions + Business Rules to:
  - Approve / Reject decisions
  - Capture reviewer comments
  - Log review operations as audits

### Phase 8 – AEB Knowledge Graph
- Table: `u_aeb_knowledge_graph`
  - `u_signal` – reference to signal
  - `u_decision` – reference to decision
  - `u_insight` – textual insight (e.g., “Network Issue – VPN pattern detected”)
  - `u_tags` – comma-separated tags
  - `u_source` – where this insight came from (BR, pattern engine, etc.)
- Business Rule creates Knowledge Graph entries for certain decisions / signals

### Phase 9 – Insight Generation Enhancements
- Additional logic to turn combinations of signals + decisions into:
  - Reusable insights
  - Suggestions for future automation or playbooks

### Phase 10 – AEB Pattern Detection
- Table: `u_aeb_pattern`
  - `u_pattern_name` – pattern details
  - `u_occurrence_count` – how many times it appeared
  - `u_last_seen` – last occurrence date/time
- Logic to group similar incidents (e.g., “VPN Network Issue”, “VPN Network Issue 1/2”)  
- On repeated signals, AEB logs or updates a pattern record.

### Phase 11 – Extended Reviews & Governance (Decision + Pattern + Knowledge)
- Combined governance over:
  - Decisions
  - Patterns
  - Knowledge Graph entries

### Phase 12 – AEB Insight Dashboard
- Dashboard elements (using **Data Visualization** + **List – Simple**) to show:
  - Knowledge Graph insights
  - Patterns and occurrence counts
  - High-risk signals and unresolved decisions

> ✅ Not every dashboard widget is visible in all PDI configurations (due to new Platform Analytics).  
> This project uses the **new Data Visualization + List – Simple** widgets instead of classic “Report” widgets.

---

## 🧩 4. Data Model

### 4.1 Core Tables

#### `u_aeb_enterprise_signal` – AEB Enterprise Signal
Represents an “interesting event” the AI Brain should look at.

Key fields:
- `u_source_type` (Choice) – `incident`, `hr_case`, `cs_case`, `other`
- `u_source_sys_id` (String) – sys_id of the source record
- `u_priority` (Integer)
- `u_short_description` (String)
- `u_detected_risk` (String)
- `u_current_state` (String / Choice)
- (optional) `u_context_json` (String) – additional context

#### `u_aeb_decision` – AEB Decision
Represents what the AI Brain decided for a Signal.

Key fields:
- `u_signal` (Reference → `u_aeb_enterprise_signal`)
- `u_decision_outcome` (String)
- `u_severity` (Choice: low, medium, high, critical)
- `u_explanation` (String)
- `u_approved` (Choice or Boolean)
- `u_approver` (Reference → `sys_user`)

#### `u_aeb_action_log_table` – AEB Action Log
Represents a proposed or executed action.

Key fields:
- `u_decision` (Reference → `u_aeb_decision`)
- `u_action_type` (String)
- `u_status` (Choice: pending, completed, failed)
- `u_details` (String)

---

### 4.2 Advanced Tables (Knowledge & Patterns)

#### `u_aeb_knowledge_graph`
- `u_signal` (Reference → `u_aeb_enterprise_signal`)
- `u_decision` (Reference → `u_aeb_decision`)
- `u_insight` (String)
- `u_tags` (String)
- `u_source` (String)

#### `u_aeb_pattern`
- `u_pattern_name` (String)
- `u_occurrence_count` (Integer)
- `u_last_seen` (Date/Time)

*(plus audit-related tables, depending on final implementation in the instance)*

---

## 🧮 5. AEB_Engine – AI Logic (Simulated)

The core decision logic lives inside a Script Include:

```javascript
var AEB_Engine = Class.create();
AEB_Engine.prototype = {
    initialize: function() {},

    // input is a GlideRecord on u_aeb_enterprise_signal
    getDecisionForSignal: function(signalGr) {
        var result = {};

        var priority = signalGr.getValue('u_priority'); // adjust field names as needed
        var sourceType = signalGr.getValue('u_source_type') || 'incident';

        // Simple rule-based "AI" for demo purposes
        if (priority == '1' || priority == '2') {
            result.decision_outcome = 'Auto-assign to AI Ops Squad';
            result.severity = 'critical';
            result.explanation = 'High priority ' + sourceType +
                ' signal detected. Routing to AI Ops Squad.';
        } else {
            result.decision_outcome = 'Monitor only';
            result.severity = 'medium';
            result.explanation = 'Non-critical ' + sourceType +
                ' signal. Logging for trend and pattern analysis.';
        }

        return result;
    },

    type: 'AEB_Engine'
};
