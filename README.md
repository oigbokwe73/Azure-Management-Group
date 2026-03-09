# Azure-Management-Group
Here is the **updated Mermaid org-style diagram** with the **Resource Group naming simplified** to exactly what you requested:

**Resource Groups**

* `rg-pcdm-dev`
* `rg-pcdm-sys`
* `rg-pcdm-uat`
* `rg-pcdm-prod`

Managed identities remain **under the resource group**.

---

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
D --> D1[Resource Group<br>rg-pcdm-dev]
D1 --> D2["• mi-pcdm-dev-policy<br>RBAC: Tag Contributor"]
D1 --> D3["• mi-pcdm-dev-logging<br>RBAC: Log Analytics Contributor"]

%% SYS
E --> E1[Resource Group<br>rg-pcdm-sys]
E1 --> E2["• mi-pcdm-sys-policy<br>RBAC: Tag Contributor"]
E1 --> E3["• mi-pcdm-sys-logging<br>RBAC: Log Analytics Contributor"]

%% UAT
F --> F1[Resource Group<br>rg-pcdm-uat]
F1 --> F2["• mi-pcdm-uat-policy<br>RBAC: Tag Contributor"]
F1 --> F3["• mi-pcdm-uat-logging<br>RBAC: Log Analytics Contributor"]

%% PROD
G --> G1[Resource Group<br>rg-pcdm-prod]
G1 --> G2["• mi-pcdm-prod-policy<br>RBAC: Tag Contributor"]
G1 --> G3["• mi-pcdm-prod-logging<br>RBAC: Log Analytics Contributor"]

%% Styling
classDef mg fill:#e6f2ff,stroke:#1f78d1,stroke-width:2px;
classDef sub fill:#eefbea,stroke:#2e8b57,stroke-width:2px;
classDef rg fill:#e8f5e9,stroke:#2e7d32,stroke-width:1.5px;
classDef mi fill:#fff4e6,stroke:#f39c12,stroke-width:1.5px;

class A,B mg;
class C,D,E,F,G sub;
class D1,E1,F1,G1 rg;
class D2,D3,E2,E3,F2,F3,G2,G3 mi;
```

---

# Final Naming Standard

### Subscriptions

```
sub-pcdm-dev
sub-pcdm-sys
sub-pcdm-uat
sub-pcdm-prod
```

### Resource Groups

```
rg-pcdm-dev
rg-pcdm-sys
rg-pcdm-uat
rg-pcdm-prod
```

### Managed Identities

```
mi-pcdm-dev-policy
mi-pcdm-dev-logging

mi-pcdm-sys-policy
mi-pcdm-sys-logging

mi-pcdm-uat-policy
mi-pcdm-uat-logging

mi-pcdm-prod-policy
mi-pcdm-prod-logging
```

---

💡 **Architecture Intent**

This structure gives you a **clean Azure governance layout**:

```
Management Group
   → Subscription (environment isolation)
      → Resource Group (identity container)
         → Managed Identity (RBAC automation)
```

Used for:

* **Azure Policy remediation**
* **Tag governance**
* **Diagnostic logging**

---

If you'd like, I can also show you a **much cleaner enterprise diagram** that compresses this entire layout into a **single repeating pattern block** like this (very common in Azure architecture docs):

```
sub-pcdm-[env]
   └ rg-pcdm-[env]
        ├ mi-pcdm-[env]-policy
        └ mi-pcdm-[env]-logging
```

It makes the diagram **50–60% smaller and easier for architecture boards to read**.
