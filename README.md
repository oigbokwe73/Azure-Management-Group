# Azure-Management-Group
Got it — we will **remove the Contributor role** and keep **one Managed Identity per RBAC role**, limited to:

* **Tag Contributor** → Policy remediation
* **Log Analytics Contributor** → Logging / diagnostics

This keeps the model **least-privilege and cleaner for governance**.

```mermaid
graph TD

A[UPS Proper<br>Root Management Group]

A --> B[UPS Tenant New Subscriptions<br>mg-upstenant-new]

B --> C[sub-pcdm-* Subscription Pattern]

C --> D[sub-pcdm-dev]
C --> E[sub-pcdm-sys]
C --> F[sub-pcdm-uat]
C --> G[sub-pcdm-prod]

%% DEV
D --> D1[Managed Identities]
D1 --> D2["• mi-pcdm-dev-policy<br>RBAC: Tag Contributor<br>Policy Remediation"]
D1 --> D3["• mi-pcdm-dev-logging<br>RBAC: Log Analytics Contributor<br>Diagnostic Logs"]

%% SYS
E --> E1[Managed Identities]
E1 --> E2["• mi-pcdm-sys-policy<br>RBAC: Tag Contributor<br>Policy Remediation"]
E1 --> E3["• mi-pcdm-sys-logging<br>RBAC: Log Analytics Contributor<br>Diagnostic Logs"]

%% UAT
F --> F1[Managed Identities]
F1 --> F2["• mi-pcdm-uat-policy<br>RBAC: Tag Contributor<br>Policy Remediation"]
F1 --> F3["• mi-pcdm-uat-logging<br>RBAC: Log Analytics Contributor<br>Diagnostic Logs"]

%% PROD
G --> G1[Managed Identities]
G1 --> G2["• mi-pcdm-prod-policy<br>RBAC: Tag Contributor<br>Policy Remediation"]
G1 --> G3["• mi-pcdm-prod-logging<br>RBAC: Log Analytics Contributor<br>Diagnostic Logs"]

%% Styling
classDef mg fill:#e6f2ff,stroke:#1f78d1,stroke-width:2px;
classDef sub fill:#eefbea,stroke:#2e8b57,stroke-width:2px;
classDef mi fill:#fff4e6,stroke:#f39c12,stroke-width:1.5px;

class A,B mg;
class C,D,E,F,G sub;
class D1,E1,F1,G1 mi;
```

### Naming Convention

**Subscriptions**

```
sub-pcdm-dev
sub-pcdm-sys
sub-pcdm-uat
sub-pcdm-prod
```

**Managed Identities**

```
mi-pcdm-[env]-policy
mi-pcdm-[env]-logging
```

Examples

```
mi-pcdm-dev-policy
mi-pcdm-dev-logging
mi-pcdm-prod-policy
mi-pcdm-prod-logging
```

### RBAC Mapping

| Managed Identity        | RBAC Role                 | Purpose                          |
| ----------------------- | ------------------------- | -------------------------------- |
| `mi-pcdm-[env]-policy`  | Tag Contributor           | Azure Policy remediation         |
| `mi-pcdm-[env]-logging` | Log Analytics Contributor | Diagnostic logging configuration |

---

If you'd like, I can also produce a **much cleaner Azure CAF governance diagram** that visually shows:

**Management Group → Policy Assignment → DeployIfNotExists → Managed Identity → Remediation → Log Analytics**

which is the **standard diagram used in Microsoft landing zone documentation.**
