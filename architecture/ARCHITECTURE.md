# Template Map Architecture

## Overview

The Template Map is a modular, component-based system for radiology reporting templates. It enables consistent, efficient report generation through reusable components and standardized picklists.

## Core Principles

1. **Component Reuse** - Components are shared across multiple templates, reducing redundancy
2. **Dependency Tracking** - Changes to a component automatically affect all templates using it
3. **CPT-Driven** - Every exam maps to a CPT code which maps to a template
4. **Structured Reporting** - Picklists ensure consistent language and reduce variation

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                         TEMPLATE                                     │
│  Complete report structure for a CPT code                           │
│  Example: 71046 (XR Chest 2 Views)                                  │
└─────────────────────────────────────────────────────────────────────┘
                                │
        ┌───────────────────────┼───────────────────────┐
        │                       │                       │
        ▼                       ▼                       ▼
┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│    HEADER     │     │   FINDINGS    │     │  IMPRESSION   │
│  Merge Fields │     │  Components   │     │  AI/Default   │
└───────────────┘     └───────────────┘     └───────────────┘
                              │
                ┌─────────────┼─────────────┐
                │             │             │
                ▼             ▼             ▼
        ┌───────────┐ ┌───────────┐ ┌───────────┐
        │ Component │ │ Component │ │ Component │
        │ CR-lungs  │ │ CR-heart  │ │ CR-bones  │
        └───────────┘ └───────────┘ └───────────┘
                │
        ┌───────┼───────┐
        │       │       │
        ▼       ▼       ▼
    ┌───────┬───────┬───────┐
    │Picklist│Picklist│Picklist│
    │Options│Options│Options│
    └───────┴───────┴───────┘
```

---

## Template Structure

Every template follows this universal structure:

### Header Section
| Field | Type | Source |
|-------|------|--------|
| EXAM | Merge Field | PACS: Procedures |
| DEMOGRAPHICS | Merge Fields | EMR: Patient Name, Age, Sex |
| CLINICAL HISTORY | Merge Field | EMR: PMHx/Indication |

### Technique Section
| Field | Type | Description |
|-------|------|-------------|
| TECHNIQUE | Picklist | Study-specific options (views, contrast, protocol) |

### Comparison Section
| Field | Type | Source |
|-------|------|--------|
| COMPARISON | Hybrid | Merge field (Prior Studies) + Picklist (None, Prior from date) |

### Findings Section
Contains one or more **Components**, each with multiple **Picklists**:

```
FINDINGS:
├── Component: Support Devices
│   ├── Picklist: ETT
│   ├── Picklist: NGT
│   └── Picklist: Central Line
├── Component: Lungs and Pleura
│   ├── Picklist: Lung opacities
│   └── Picklist: Pleural effusion
└── Component: Heart and Mediastinum
    ├── Picklist: Cardiac size
    └── Picklist: Mediastinal contours
```

### Impression Section
| Field | Type | Description |
|-------|------|-------------|
| IMPRESSION | AI Field | AI-generated based on findings, default: "Normal exam." |

---

## Data Files

### template-map.json
Master file containing all template definitions:

```json
{
  "modalities": {
    "xray": {
      "display_name": "X-Ray / Radiography",
      "regions": {
        "chest": {
          "display_name": "Chest",
          "templates": {
            "xr-chest-2view": {
              "primary_cpt": "71046",
              "description": "XR Chest, 2 views",
              "component_templates": ["CR-lungsandpleura", "CR-heartmediastinum", "CR-bones"]
            }
          }
        }
      }
    }
  }
}
```

### component-map.json
Master file containing all component definitions:

```json
{
  "xray": {
    "display_name": "X-Ray / Radiography",
    "chest": {
      "display_name": "Chest Radiograph",
      "component_templates": {
        "CR-lungsandpleura": {
          "id": "CR-lungsandpleura",
          "display_name": "Lungs and Pleura",
          "routes_to": ["xr-chest-portable", "xr-chest-2view"],
          "picklists": {
            "lung_opacities": {
              "display_name": "Lung Opacities",
              "multiselect": true,
              "options": [...]
            }
          }
        }
      }
    }
  }
}
```

---

## Component Naming

Components use a prefix indicating modality:

| Prefix | Modality | Example |
|--------|----------|---------|
| CR- | Chest Radiograph | CR-lungsandpleura |
| AR- | Abdominal Radiograph | AR-bowelgas |
| CT- | Computed Tomography | CT-liver |
| US- | Ultrasound | US-gallbladder |
| MR- | MRI | MR-spine-lumbar |
| NM- | Nuclear Medicine | NM-hida |

---

## Picklist Option States

Each option has a clinical state for categorization and display:

| State | Color | Use Case |
|-------|-------|----------|
| `absent` | Gray | Device/structure not present |
| `normal` | Green | Normal/unremarkable finding |
| `abnormal` | Yellow | Abnormal finding |
| `critical` | Red | Critical finding requiring immediate action |
| `chronic` | Purple | Chronic/stable finding |
| `benign` | Teal | Definitively benign |
| `surgical` | Blue | Post-surgical state |

---

## Dependency Tracking

Components track which templates use them via `routes_to`:

```json
{
  "CR-lungsandpleura": {
    "routes_to": [
      "xr-chest-portable",
      "xr-chest-2view",
      "xr-chest-3plus"
    ]
  }
}
```

When a component is modified, all templates in `routes_to` are affected.

---

## Example: Chest X-Ray Template

```
Template: xr-chest-2view (CPT 71046)
├── HEADER
│   ├── EXAM: {{Procedures}}
│   ├── DEMOGRAPHICS: {{Patient Name}}, {{Age}}, {{Sex}}
│   └── CLINICAL HISTORY: {{PMHx}}
│
├── TECHNIQUE: [Picklist: 2-view technique options]
│
├── COMPARISON: {{Prior Studies}} + [Picklist: comparison options]
│
├── FINDINGS
│   ├── Component: CR-devices (Lines and Tubes)
│   │   ├── Picklist: ETT
│   │   ├── Picklist: NGT
│   │   ├── Picklist: Central Line
│   │   └── Picklist: Chest Tube
│   │
│   ├── Component: CR-lungsandpleura (Lungs and Pleura)
│   │   ├── Picklist: Lung opacities
│   │   ├── Picklist: Pleural effusion
│   │   └── Picklist: Pneumothorax
│   │
│   ├── Component: CR-heartmediastinum (Heart and Mediastinum)
│   │   ├── Picklist: Cardiac size
│   │   └── Picklist: Mediastinal contours
│   │
│   └── Component: CR-bones (Bones and Soft Tissues)
│       ├── Picklist: Rib findings
│       └── Picklist: Soft tissue findings
│
└── IMPRESSION: [AI Generated] Default: "No acute cardiopulmonary abnormality."
```

---

## Integration Points

### EMR/PACS Integration (HL7)
Merge fields populated from:
- Procedure information
- Patient demographics
- Clinical history
- Prior study references

### AI Integration
- Impression field designed for AI population
- AI analyzes selected findings and generates structured impression
- Fallback to default text when AI unavailable

---

## File Organization

```
Template Map/
├── template-map.json        # Template definitions
├── component-map.json       # Component/picklist definitions
├── index.html               # Web application
│
├── templates/               # Individual template files (detailed structure)
│   ├── xray/chest/
│   ├── ct/abdomen-pelvis/
│   └── ...
│
└── components/              # Individual component files (detailed structure)
    ├── headers/
    ├── findings/
    └── atomic/
```

---

## Editing Workflow

1. **Select Template** - Choose from left panel tree
2. **View Structure** - See complete template structure in center panel
3. **Edit Component** - Click component to edit picklists in right panel
4. **Add/Remove** - Add new picklists, options, or components
5. **Save** - Click "Save All" to persist changes to JSON files
