# ServiceNow Digital Twin Intelligence

A fully autonomous, AI-powered Digital Twin Engine built on the ServiceNow platform.  
It models systems as digital twins, evaluates health, detects anomalies, maps dependencies, propagates risk, generates insights, and recommends remediation actions.

---

## 1. Overview

**ServiceNow Digital Twin Intelligence** provides:

- Digital representation of enterprise systems  
- Continuous anomaly and health scoring  
- Parent–child dependency modeling  
- Propagated risk scoring  
- AI-based insights & recommendations  
- Auto-remediation logic  
- Dashboards for health, risk, and anomaly trends  
- A GenAI assistant ("Ask the Twin")  

This project demonstrates advanced Now Platform engineering, AIOps patterns, GlideScript, UI Actions, Script Includes, Flow Designer automation, and GenAI integration.

---

## 2. Architecture

Digital Twin Core
├─ Twin Data Model
├─ Sync Engine
├─ Anomaly Engine
├─ Health Score Engine
├─ Insights Engine
├─ Recommendations Engine
├─ Remediation Engine
├─ Dependency Mapping
└─ Risk Propagation

Experience Layer
├─ Dashboards (Health, Anomaly, Risk)
└─ Twin Assistant (GenAI)

yaml
Copy code

---

## 3. Data Model

### 3.1 Digital Twin Table  
**x_1856403_digital_digital_twin**

| Field | Description |
|-------|-------------|
| name | Twin name |
| twin_anomaly_score | Auto-calculated anomaly value |
| health_score | Overall health score |
| twin_insights | AI-generated insights |
| twin_recommendation | Recommended actions |
| twin_risk_score | Calculated risk score |
| twin_risk_level | Low / Medium / High / Critical |
| remediation_status | Pending / Successful / Failed |
| twin_remediation_actions | Actions executed |
| last_updated | Timestamp |

---

### 3.2 Dependencies Table  
**x_1856403_digital_digital_twin_dependencies**

| Field | Description |
|-------|-------------|
| parent_twin | Parent system |
| child_twin | Child system |
| impact_weight | Influence weight on parent |

---

### 3.3 Logs Table  
**x_1856403_digital_twin_logs**

Stores anomaly events, insights, remediation logs, and risk updates.

---

## 4. Key Features

### 4.1 Anomaly Detection Engine  
Automatically calculates anomalies on update.

### 4.2 Health Score Engine  
Health = inverse-anomaly + weighted factors.

### 4.3 Insights Engine  
Generates explanations appended to `twin_insights`.

### 4.4 Recommendation Engine  
Suggests corrective actions.

### 4.5 Remediation Engine  
Tracks:  
- `remediation_status`  
- `last_remediation_timestamp`  
- `twin_remediation_actions`

### 4.6 Dependency Impact Engine  
Propagates child degradation upward to parent.

### 4.7 Risk Engine  
Combines anomaly + health → risk level.

### 4.8 GenAI Assistant ("Ask the Twin")  
UI Action + GlideAjax + Script Include.

### 4.9 Dashboards  
- Twin Health Dashboard  
- Anomaly Dashboard  
- Risk Dashboard  

---

## 5. Script Example (Dependency Engine)

```javascript
var dep = new GlideRecord('x_1856403_digital_digital_twin_dependencies');
dep.addQuery('parent_twin', twinRecord.sys_id);
dep.query();

while (dep.next()) {
    var child = new GlideRecord('x_1856403_digital_digital_twin');
    if (child.get(dep.child_twin)) {
        var weight = parseInt(dep.impact_weight || 10);
        var propagated = Math.floor((100 - child.health_score) * (weight / 100));
        twinRecord.health_score = Math.max(0, twinRecord.health_score - propagated);
    }
}
```
## 6. Dashboards

Upload your screenshots into the `/assets/` folder after cloning the repository.

Example placeholders:

![Twin Health Dashboard](assets/dashboard_health.png)  
![Anomaly Dashboard](assets/dashboard_anomaly.png)  
![Risk Dashboard](assets/dashboard_risk.png)  
![Ask the Twin](assets/ask_twin.png)

---

## 7. Installation

### Step 1 — Clone the repository

git clone https://github.com/srikanthmadabhushi/ServiceNow-Digital-Twin-Intelligence

markdown
Copy code

### Step 2 — Import the required components

Install the following into your ServiceNow instance:

- Script Includes  
- Business Rules  
- Client Scripts  
- UI Actions  
- Flow Designer Flows  
- Custom Tables  
- Dashboards  

### Step 3 — Add screenshots

Place all screenshots in:

/assets/

yaml
Copy code

GitHub will automatically render them in the README.

---

## 8. How It Works

1. A digital twin receives new data or an update.  
2. The Anomaly Engine recalculates `twin_anomaly_score`.  
3. The Health Engine recalculates `health_score`.  
4. The Dependency Engine propagates child impact to the parent.  
5. The Risk Engine updates the parent’s `twin_risk_score` and `twin_risk_level`.  
6. The Insights Engine appends explanations into `twin_insights`.  
7. The Recommendation Engine generates actionable remediation items.  
8. Dashboards automatically refresh with new metrics.  
9. The GenAI Twin Assistant can explain anomalies, risks, or actions.

This end-to-end automation forms a complete **Digital Twin Operational Loop**.

---

## 9. Future Enhancements

The roadmap includes:

- Real-time event streaming for live updates  
- Automated CMDB integration  
- Predictive anomaly forecasting (ML model)  
- Phase 16: Digital Twin Command Center  
- Autonomous change execution based on recommendations  
- Multi-system orchestration  
- Full enterprise topology visualization  

---

## 10. Author

**Srikanth Madabhushi**  
ServiceNow & AI Engineer  

Portfolio:  
https://SrikanthMadabhushi.github.io
