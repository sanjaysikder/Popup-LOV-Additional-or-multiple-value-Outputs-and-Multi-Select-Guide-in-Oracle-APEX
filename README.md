# Popup LOV Additional/multiple value Outputs & Multi-Select Guide in Oracle APEX

## 📌 Overview
This document explains how to:
1. set/Populate multiple page items using **Popup LOV (Additional Outputs)**
2. Handle **multi-row selection** in Oracle APEX

---

# ✅ 1. Populate Multiple Page Items (Additional Outputs)

## 🎯 Use Case
Select one record (e.g., Fabric / Employee) and automatically populate related fields:
- Fabric Code
- Composition
- Construction
- Width
- Style No
- Fabric Name

---

## 🧩 Step 1: LOV Definition (Shared Component)

- Navigate to:

- Shared Components → List of Values → Create


### SQL Query:
```sql
SELECT 
    SFI.FABRIC_ID       AS RETURN_VALUE,
    VGFN.FABRIC_NAME    AS DISPLAY_VALUE,
    SFI.FABRIC_CODE,
    SFI.COMPOSITION,
    SFI.CONSTRUCTION,
    SFI.WIDTH,
    SFI.STYLE_NO
FROM sc_fabric_item SFI
LEFT JOIN V_GET_FABRIC_NAME VGFN 
       ON VGFN.FABRIC_ID = SFI.FABRIC_ID  
WHERE SFI.APPROVED_STATUS = 'A'
ORDER BY SFI.COMPOSITION;
```
## ✅ Important Rules
RETURN_VALUE → must be single column
DISPLAY_VALUE → user-visible column
Include all extra columns in SELECT

## 🧩 Step 2: Create Page Items

```Example page items:

P1_FABRIC_ID
P1_FABRIC_CODE
P1_COMPOSITION
P1_CONSTRUCTION
P1_WIDTH
P1_STYLE_NO
P1_FABRIC_NAME

```
## 🧩 Step 3: Configure Popup LOV Item

- For item P1_FABRIC_ID:

- Type → Popup LOV
- List of Values → Select your Shared LOV
## 🧩 Step 4: Configure Additional Outputs

- Go to:

- P1_FABRIC_ID → Settings → Additional Outputs

- Mapping Format:
COLUMN_NAME:PAGE_ITEM_NAME
``` Example:
FABRIC_CODE:P1_FABRIC_CODE,
COMPOSITION:P1_COMPOSITION,
CONSTRUCTION:P1_CONSTRUCTION,
WIDTH:P1_WIDTH,
STYLE_NO:P1_STYLE_NO,
DISPLAY_VALUE:P1_FABRIC_NAME
```
## 🧪 Result

When user selects a value:

| Field        | Auto Filled |
| ------------ | ----------- |
| FABRIC_ID    | ✅           |
| FABRIC_CODE  | ✅           |
| COMPOSITION  | ✅           |
| CONSTRUCTION | ✅           |
| WIDTH        | ✅           |
| STYLE_NO     | ✅           |
| FABRIC_NAME  | ✅           |


---


 ## Thank you
 ## Sanjay Sikder

You can connect with me on <a href="https://www.linkedin.com/in/sanjay-sikder/" target="_blank">LinkedIn</a>!

---
