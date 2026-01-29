# Radiology Template Mapping System Architecture

## Overview

This document defines the architecture for a modular, component-based radiology reporting template system. The system minimizes redundancy through nested template dependencies, enabling changes to propagate automatically across all dependent templates.

## Core Principles

1. **Single Source of Truth** - Each component exists once and is referenced by multiple templates
2. **Hierarchical Composition** - Templates are composed of reusable components in a tree structure
3. **CPT Code Driven** - Every reportable exam maps to a CPT code which maps to a template
4. **Inheritance** - Components can inherit from base components with modifications

---

## Architecture Layers

```
┌─────────────────────────────────────────────────────────────────────┐
│                    LAYER 1: CPT CODE TEMPLATES                       │
│  One template per CPT code variant (contrast, gender, technique)     │
│  Example: 71046 (XR Chest 2 Views)                                   │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                    LAYER 2: SECTION COMPONENTS                       │
│  Major report sections that compose into complete templates          │
│  Examples: Header, Findings, Impression                              │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                    LAYER 3: SUBCOMPONENTS                            │
│  Reusable finding blocks within sections                             │
│  Examples: Lungs & Pleura, Heart & Mediastinum                       │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                    LAYER 4: ATOMIC ELEMENTS                          │
│  Smallest reusable units with option picklists                       │
│  Examples: Lung opacity options, Cardiac silhouette options          │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Naming Convention

### Template Naming Pattern
```
[Region] [Modality] [BodyPart] [Contrast] [Variant] ([CPT Code])
```

### Component Naming Pattern
```
[Type].[Region].[Modality].[BodyPart].[ComponentName]
```

**Type Prefixes:**
- `CPT.` - CPT code-mapped complete template
- `HDR.` - Header component
- `FND.` - Findings section component
- `SUB.` - Subcomponent within findings
- `ATM.` - Atomic element with picklist options
- `IMP.` - Impression component
- `TEC.` - Technique component

---

## Component Dependencies Example: Chest X-Ray

```
CPT.71046 (XR Chest 2 Views)
├── HDR.chest.xr.standard
│   ├── ATM.exam_info
│   ├── ATM.date_time
│   ├── ATM.indication
│   └── ATM.comparison
├── TEC.chest.xr.2view
├── FND.chest.xr.standard
│   ├── SUB.chest.xr.exam_quality
│   ├── SUB.chest.xr.support_devices
│   ├── SUB.chest.xr.lungs_pleura
│   │   ├── ATM.lungs.opacities
│   │   ├── ATM.lungs.volumes
│   │   ├── ATM.pleura.effusion
│   │   └── ATM.pleura.pneumothorax
│   ├── SUB.chest.xr.heart_mediastinum
│   │   ├── ATM.heart.size
│   │   ├── ATM.heart.contour
│   │   └── ATM.mediastinum.width
│   ├── SUB.chest.xr.bones_soft_tissue
│   │   ├── ATM.bones.ribs
│   │   ├── ATM.bones.spine
│   │   └── ATM.soft_tissue.general
│   └── SUB.chest.xr.upper_abdomen
│       ├── ATM.upper_abd.liver
│       └── ATM.upper_abd.stomach
└── IMP.chest.xr.standard
```

---

## Modality Categories

### X-Ray (XR)
| Category | Body Regions |
|----------|-------------|
| Chest | Chest, Ribs, Sternum |
| MSK | Extremities, Spine, Pelvis, Joints |
| Abdomen | KUB, Obstruction Series |
| Head/Neck | Skull, Facial Bones, Sinuses |

### CT
| Category | Body Regions |
|----------|-------------|
| Neuro | Brain, Orbits, Face, Sinuses |
| Chest | Chest, High-Res, Lung Screening |
| Abdomen/Pelvis | Abd, Pel, Abd/Pel combinations |
| Angiography | CTA Head, Neck, Chest, Abd, Runoff |
| MSK | Spine, Extremities |

### MRI
| Category | Body Regions |
|----------|-------------|
| Neuro | Brain, Spine, Orbits |
| Body | Abdomen, Pelvis, Breast, Chest |
| MSK | Joints, Extremities |
| Angiography | MRA Head, Neck, Abd, Extremities |

### Ultrasound (US)
| Category | Body Regions |
|----------|-------------|
| Abdomen | Complete, Limited, RUQ |
| Pelvis | OB, GYN, Prostate |
| Vascular | Carotid, Venous, Arterial |
| Small Parts | Thyroid, Breast, Scrotum |

### Nuclear Medicine / PET
| Category | Body Regions |
|----------|-------------|
| Cardiac | MUGA, Myocardial Perfusion |
| Bone | Bone Scan, 3-Phase |
| Oncology | PET/CT Whole Body |
| Organ Specific | Thyroid, Hepatobiliary, Renal |

### Fluoroscopy
| Category | Body Regions |
|----------|-------------|
| GI | UGI, SBFT, Barium Enema |
| GU | IVP, Cystogram |

### Mammography
| Category | Variants |
|----------|----------|
| Screening | 2D, 3D |
| Diagnostic | Bilateral, Unilateral |
| Interventional | Biopsy, Localization |

---

## Template Variants

Templates may have variants based on:

1. **Contrast Administration**
   - Without contrast
   - With contrast
   - With and without contrast

2. **Patient Demographics**
   - Male
   - Female
   - Pediatric

3. **Clinical Context**
   - Routine/Outpatient
   - Emergency
   - Trauma
   - ICU/Inpatient
   - Screening

4. **Reporting Style**
   - Structured (picklists)
   - Free text
   - Hybrid

5. **Specific Protocols**
   - PE protocol
   - Dissection protocol
   - LI-RADS
   - Lung-RADS
   - TI-RADS

---

## File Structure

```
Template Map/
├── architecture/
│   ├── ARCHITECTURE.md           # This file
│   ├── NAMING_CONVENTIONS.md     # Detailed naming rules
│   └── COMPONENT_CATALOG.md      # Master list of all components
│
├── cpt-mapping/
│   ├── ct/
│   │   ├── ct_neuro.json
│   │   ├── ct_chest.json
│   │   ├── ct_abdomen.json
│   │   └── ct_msk.json
│   ├── mri/
│   │   ├── mri_neuro.json
│   │   ├── mri_body.json
│   │   └── mri_msk.json
│   ├── xr/
│   │   ├── xr_chest.json
│   │   ├── xr_msk.json
│   │   └── xr_abdomen.json
│   ├── us/
│   │   ├── us_abdomen.json
│   │   ├── us_pelvis.json
│   │   └── us_vascular.json
│   ├── nuclear/
│   │   ├── nuclear_cardiac.json
│   │   ├── nuclear_bone.json
│   │   └── pet_ct.json
│   ├── fluoro/
│   │   └── fluoro_gi.json
│   └── mammo/
│       └── mammo.json
│
├── components/
│   ├── headers/
│   │   ├── HDR.standard.json
│   │   ├── HDR.emergency.json
│   │   └── HDR.icu.json
│   ├── techniques/
│   │   ├── TEC.ct.contrast.json
│   │   ├── TEC.mri.contrast.json
│   │   └── TEC.xr.views.json
│   ├── findings/
│   │   ├── chest/
│   │   ├── abdomen/
│   │   ├── neuro/
│   │   ├── msk/
│   │   └── vascular/
│   ├── impressions/
│   │   ├── IMP.normal.json
│   │   ├── IMP.abnormal.json
│   │   └── IMP.critical.json
│   └── atomic/
│       ├── ATM.lungs.json
│       ├── ATM.heart.json
│       ├── ATM.liver.json
│       └── ...
│
├── picklists/
│   ├── lungs_opacities.json
│   ├── cardiac_size.json
│   ├── liver_lesions.json
│   └── ...
│
└── source/
    ├── AutoTextExport (46).xml   # Original template export
    └── cpt-code-2024.pdf         # CPT code reference
```

---

## JSON Schema for CPT Mapping

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "CPT Template Mapping",
  "type": "object",
  "properties": {
    "cpt_code": {
      "type": "string",
      "description": "CPT code (e.g., '71046')"
    },
    "procedure_name": {
      "type": "string",
      "description": "Official procedure name"
    },
    "modality": {
      "type": "string",
      "enum": ["XR", "CT", "MRI", "US", "NM", "PET", "FLUORO", "MAMMO"]
    },
    "body_region": {
      "type": "string",
      "description": "Primary body region"
    },
    "contrast": {
      "type": "string",
      "enum": ["without", "with", "with_without", "na"]
    },
    "variants": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "variant_id": { "type": "string" },
          "description": { "type": "string" },
          "components": {
            "type": "array",
            "items": { "type": "string" }
          }
        }
      }
    },
    "components": {
      "type": "object",
      "properties": {
        "header": { "type": "string" },
        "technique": { "type": "string" },
        "findings": {
          "type": "array",
          "items": { "type": "string" }
        },
        "impression": { "type": "string" }
      }
    }
  }
}
```

---

## Implementation Phases

### Phase 1: Foundation
- Create folder structure
- Define all CPT codes and their basic mappings
- Identify all unique body regions and modalities

### Phase 2: Component Extraction
- Analyze existing 4,795 templates
- Extract common components
- Define component hierarchy

### Phase 3: Picklist Development
- Create atomic elements with option values
- Define normal/abnormal pathways
- Build conditional logic rules

### Phase 4: Assembly & Testing
- Combine components into complete templates
- Validate against existing templates
- Test template generation

### Phase 5: Migration
- Replace redundant templates with component references
- Update XML export format
- Deploy to production system

---

## Component Reuse Matrix

This matrix shows which subcomponents are shared across modalities:

| Subcomponent | XR Chest | CT Chest | CTA Chest | MRI Chest |
|--------------|----------|----------|-----------|-----------|
| Lungs & Pleura | ✓ | ✓ | ✓ | ✓ |
| Heart & Mediastinum | ✓ | ✓ | ✓ | ✓ |
| Bones | ✓ | ✓ | ✓ | ✓ |
| Soft Tissue | ✓ | ✓ | ✓ | ✓ |
| Upper Abdomen | ✓ | ✓ | ✓ | ✓ |
| Pulmonary Arteries | - | - | ✓ | - |
| Aorta/Great Vessels | - | ✓ | ✓ | ✓ |
| Coronary Arteries | - | ✓* | - | - |

*CTA Coronary specific

---

## Dependency Tracking

When a component is modified, the system must identify all dependent templates:

```
Component Modified: SUB.chest.xr.lungs_pleura
├── Affected Templates:
│   ├── CPT.71045 (XR Chest 1 View) - 6 variants
│   ├── CPT.71046 (XR Chest 2 Views) - 4 variants
│   ├── CPT.71047 (XR Chest w/ Apical Lordotic) - 2 variants
│   └── CPT.71048 (XR Chest w/ Oblique) - 2 variants
└── Total Templates Affected: 14
```

---

## Next Steps

1. Review this architecture document
2. Create initial CPT mapping files starting with:
   - X-Ray Chest (most common, good baseline)
   - CT Abdomen/Pelvis (complex, multi-variant)
   - MRI Brain (standardized, high volume)
3. Extract component definitions from existing XML
4. Build picklist option libraries
