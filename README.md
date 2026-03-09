# Azure-Management-Group
You want the diagram to also show **Resource Groups under each subscription**, using the **same naming pattern style** and keeping it **compact**.

Pattern:

* **Subscription:** `sub-pcdm-[env]`
* **Resource Group:** `rg-pcdm-[env]-*`
* **Managed Identity:** `mi-pcdm-[env]-policy` / `mi-pcdm-[env]-logging`

Below is the **updated Mermaid org-style diagram**.

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
D --> D1[Resource Groups<br>rg-pcdm-dev-*]
D --> D2[Managed Identities]

D2 --> D3["• mi-pcdm-dev-policy<br>RBAC: Tag Contributor"]
D2 --> D4["• mi-pcdm-dev-logging<br>RBAC: Log Analytics Contributor"]

%% SYS
E --> E1[Resource Groups<br>rg-pcdm-sys-*]
E --> E2[Managed Identities]

E2 --> E3["• mi-pcdm-sys-policy<br>RBAC: Tag Contributor"]
E2 --> E4["• mi-pcdm-sys-logging<br>RBAC: Log Analytics Contributor"]

%% UAT
F --> F1[Resource Groups<br>rg-pcdm-uat-*]
F --> F2[Managed Identities]

F2 --> F3["• mi-pcdm-uat-policy<br>RBAC: Tag Contributor"]
F2 --> F4["• mi-pcdm-uat-logging<br>RBAC: Log Analytics Contributor"]

%% PROD
G --> G1[Resource Groups<br>rg-pcdm-prod-*]
G --> G2[Managed Identities]

G2 --> G3["• mi-pcdm-prod-policy<br>RBAC: Tag Contributor"]
G2 --> G4["• mi-pcdm-prod-logging<br>RBAC: Log Analytics Contributor"]

%% Styling
classDef mg fill:#e6f2ff,stroke:#1f78d1,stroke-width:2px;
classDef sub fill:#eefbea,stroke:#2e8b57,stroke-width:2px;
classDef rg fill:#e8f5e9,stroke:#2e7d32,stroke-width:1.5px;
classDef mi fill:#fff4e6,stroke:#f39c12,stroke-width:1.5px;

class A,B mg;
class C,D,E,F,G sub;
class D1,E1,F1,G1 rg;
class D2,E2,F2,G2 mi;
```

## Naming Standard

### Subscriptions

```
sub-pcdm-dev
sub-pcdm-sys
sub-pcdm-uat
sub-pcdm-prod
```

### Resource Groups

```
rg-pcdm-dev-network
rg-pcdm-dev-app
rg-pcdm-dev-data
rg-pcdm-dev-monitor
```

```
rg-pcdm-prod-network
rg-pcdm-prod-app
rg-pcdm-prod-data
rg-pcdm-prod-monitor
```

### Managed Identities

```
mi-pcdm-dev-policy
mi-pcdm-dev-logging
```

```
mi-pcdm-prod-policy
mi-pcdm-prod-logging
```

## Governance Intent

| Component                               | Purpose                           |
| --------------------------------------- | --------------------------------- |
| **Management Group**                    | Governance + policy inheritance   |
| **Subscription (`sub-pcdm-*`)**         | Environment isolation             |
| **Resource Groups (`rg-pcdm-[env]-*`)** | Workload segmentation             |
| **Managed Identity (`mi-pcdm-*`)**      | Policy remediation + logging RBAC |

---

If you'd like, I can also produce a **very polished Azure Landing Zone architecture diagram** that shows:

```
Management Group
   ├── Policy Initiative
   ├── Subscription Factory
   └── sub-pcdm-[env]
         ├── Resource Groups
         ├── Managed Identity
         ├── Policy Remediation
         └── Log Analytics
```

This version is **much closer to Microsoft's CAF architecture visuals** used in enterprise documentation.
