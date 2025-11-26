# 🧠 Autonomous Enterprise Brain (AEB)
### AI-Orchestrated Enterprise Signal, Decision & Insight Engine  
**Built on ServiceNow – End-to-End Multi-Phase Architecture**

---

## 📌 Project Overview
The **Autonomous Enterprise Brain (AEB)** is an enterprise-grade, AI-driven orchestration engine built on ServiceNow.  
It intelligently **detects events**, **generates decisions**, **logs actions**, **creates insights**, **builds patterns**, and **visualizes knowledge** through dashboards.

This project demonstrates **complete enterprise automation**, covering:

- Multi-domain signals (ITSM, HR, CSM)
- AI-based decision generation  
- Knowledge graph creation  
- Pattern identification  
- Action orchestration  
- Custom UI Actions & Business Rules  
- Cross-table automation  
- Dashboard visualization  
- Governance layers  
- Full phased development

This is a **12-phase, real-world, end-to-end ServiceNow AI system** suitable for:

✅ Interviews  
✅ Portfolio projects  
✅ Client demos  
✅ Innovation lab work  
✅ Showcasing ServiceNow AI & automation expertise  

---

# 🏗️ Architecture Summary

```text
Incident / HR Case / CSM Case
        ↓
AEB Enterprise Signal
        ↓
AEB Decision Engine (Script Include)
        ↓
AEB Action Log
        ↓
AEB Governance (Approve / Reject)
        ↓
AEB Knowledge Graph
        ↓
AEB Insight Engine
        ↓
AEB Pattern Engine
        ↓
AEB Dashboards (Signals, Decisions, Insights)

```
---

## 🧩 Technical Components
**1. Custom Tables**
Table	Purpose
u_aeb_enterprise_signal	Stores incoming ITSM/HR/CSM signals
u_aeb_decision	AI-generated decisions
u_aeb_action_log_table	Logs actions generated
u_aeb_knowledge_graph	Stores insights + linked signals/decisions
u_aeb_insight	Insight records
u_aeb_pattern	Pattern analysis output
Additional tables (Phase-based)	For governance / approvals

**2. Script Includes**

AEB_Engine – Core AI logic

AEB_Insight_Engine – Insight generator

AEB_Pattern_Engine – Pattern identifier

**3. Business Rules**

Auto-create Signals from critical incidents

Auto-run AEB Engine on Signal insert

Auto-create Action Log

Auto-generate Knowledge Graph

Auto-generate Patterns

Approval BRs

Insight BRs

**4. UI Actions**

Generate Action Log button on Decision table

Approve Decision

Reject Decision

Generate Insight

**5. Dashboards**

AEB Command Center (Signals + Decisions)

AEB Insights Dashboard

AEB Pattern Dashboard

## 🚀 Complete Phase Breakdown**

**Phase 1 — AEB Data Model Setup**

Tables:

AEB Signal

AEB Decision

AEB Action Log

**Phase 2 — AEB Command Center (UI Layer)**
Dashboard

List widgets

Chart widgets

**Phase 3 — Multi-Domain Signal Integration**
ITSM → Signals

HR → Signals

CSM → Signals

**Phase 4 — Action Log UI Action**
Button: Generate Action Log

Script to populate action table

**Phase 5 — Governance Layer**
Approve / Reject

Decision status updates

**Phase 6 — AEB Insight Engine**
Insight auto-generation

Insight table

**Phase 7 — AEB Audit & Compliance**
AEB Decision Audit

Audit BRs

**Phase 8 — AEB Knowledge Graph**
Graph linking signals → decisions → insights

Knowledge Graph table

**Phase 9 — AEB Insight Dashboard**
Insight list

Insight visualizations

**Phase 10 — Pattern Engine**
Pattern detection model

Pattern table auto creation

Frequency counter

**Phase 11 — AEB Pattern Dashboard**
Trend summary

Heatmap / occurrence chart

**Phase 12 — AEB Final Command Center**
Unified dashboard

Signals + Decisions + Patterns + Insights

This represents a full enterprise-grade product.

## 🧪 Testing Steps
▪ Test 1: Create critical incident → Signal created
▪ Test 2: Open Signal → Decision created
▪ Test 3: Click “Generate Action Log” → Action created
▪ Test 4: Approve Decision → Governance updates
▪ Test 5: Create similar incidents → Pattern created
▪ Test 6: Create CSM/HR cases → Multi-domain signals
▪ Test 7: Dashboard loads data

## 📄 How to Run the Project (Developer Setup)
1. Install in any PDI
2. Create required tables
3. Add Script Includes
4. Add Business Rules
5. Add UI Actions
6. Create dashboards

Everything works entirely inside a demo instance.

## 🧠 Skills Demonstrated

✔ ServiceNow Development
✔ AI/ML Style Rule Engine Design
✔ Data Modeling
✔ Business Rules (Scripting)
✔ Script Includes (Reusable engine pattern)
✔ UI Actions
✔ Dashboards
✔ Pattern recognition logic
✔ Insight engines
✔ Multi-domain signal integration
✔ Governance & workflow design

## 🏁 Final Notes

This is a complete enterprise-level AI automation product, built from scratch, showcasing:

Architecture thinking

AI workflow design

ServiceNow backend expertise

Full-stack platform development

End-to-end implementation capability

## 🔗 Author

Srikanth Madabhushi
AI Automation & Workflow Engineer
MS in Artificial Intelligence
Portfolio: https://SrikanthMadabhushi.github.io
