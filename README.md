# Radiology Template Mapping System

A modular, component-based architecture for radiology reporting templates that minimizes redundancy through nested dependencies.

## Overview

This system maps every CPT code to a template composed of reusable components. When you modify a component, changes automatically propagate to all templates that depend on it.

## Quick Start

1. **Understand the Architecture** → Read `architecture/ARCHITECTURE.md`
2. **Learn Naming Conventions** → Read `architecture/NAMING_CONVENTIONS.md`
3. **Browse Components** → See `architecture/COMPONENT_CATALOG.md`
4. **Explore CPT Mappings** → Check `cpt-mapping/` by modality

## Directory Structure

```
Template Map/
├── README.md                     # This file
│
├── architecture/                 # System design documentation
│   ├── ARCHITECTURE.md          # Core architecture and concepts
│   ├── NAMING_CONVENTIONS.md    # Standardized naming rules
│   └── COMPONENT_CATALOG.md     # Master component reference
│
├── templates/                    # Individual CPT code templates
│   ├── schema/                  # Template JSON schema
│   │   └── template.schema.json
│   │
│   ├── xray/                    # X-Ray templates
│   │   ├── chest/              # 71045-71048
│   │   ├── abdomen/            # 74018-74021
│   │   ├── spine/              # cervical, thoracic, lumbar, etc.
│   │   ├── pelvis/             # 72170-72202
│   │   ├── extremities/        # upper/ and lower/
│   │   ├── ribs/               # 71100-71130
│   │   └── special/            # skull, DEXA, bone age
│   │
│   ├── ct/                      # CT templates
│   │   ├── head/               # 70450-70498
│   │   ├── neck/               # 70490-70498
│   │   ├── chest/              # 71250-75574
│   │   ├── abdomen-pelvis/     # 74150-74263
│   │   ├── spine/              # 72125-72132
│   │   ├── extremities/        # 73200-73706
│   │   └── special/            # scanogram, claudication
│   │
│   ├── mri/                     # MRI templates
│   │   ├── brain/              # 70551-76390
│   │   ├── head-neck/          # 70336-70549
│   │   ├── spine/              # cervical, thoracic, lumbar
│   │   ├── chest-abdomen/      # 71550-74185
│   │   ├── musculoskeletal/    # upper/ and lower/
│   │   ├── breast/             # 77046-77049
│   │   └── special/            # elastography, MRCP
│   │
│   ├── ultrasound/              # Ultrasound templates
│   │   ├── abdomen/            # 76700-76706
│   │   ├── pelvis/             # 76830-76857
│   │   ├── ob-gyn/             # 76801-76817
│   │   ├── vascular/           # 93880-93975
│   │   ├── superficial/        # 76536-76882
│   │   ├── breast/             # 76641-76642
│   │   └── special/            # renal, transplant, elastography
│   │
│   ├── fluoroscopy/             # 74220-74400
│   ├── nuclear-medicine/        # cardiac, bone, thyroid, etc.
│   ├── pet-ct/                  # 78608-78816
│   └── mammography/             # 77063-77067, 19081-19283
│
├── cpt-mapping/                  # CPT code → component mappings (summary files)
│   ├── schema/                  # JSON schemas
│   ├── ct/, mri/, xr/, us/      # By modality
│   └── ...
│
├── components/                   # Reusable template components
│   ├── headers/                 # HDR.* components
│   ├── techniques/              # TEC.* components
│   ├── findings/                # SUB.* components by body region
│   ├── impressions/             # IMP.* components
│   └── atomic/                  # ATM.* picklist elements
│
├── picklists/                    # Option value libraries
│
└── source/                       # Original source files
    ├── AutoTextExport (46).xml
    └── cpt-code-2024.pdf
```

## Key Concepts

### Component Hierarchy

```
Layer 1: CPT Templates     → Complete template for a CPT code
Layer 2: Section Components → Major report sections (Header, Findings, Impression)
Layer 3: Subcomponents      → Finding blocks (Lungs, Heart, Liver, etc.)
Layer 4: Atomic Elements    → Individual picklist items
```

### Example: Chest X-Ray

```
CPT.71046 (XR Chest 2 Views)
├── HDR.chest.xr.standard        → Header
├── TEC.chest.xr.2view           → Technique
├── SUB.chest.xr.lungs_pleura    → Findings: Lungs ──┐
├── SUB.chest.xr.heart_mediastinum                   │ SHARED across
├── SUB.chest.xr.bones_soft_tissue                   │ all chest XR
└── IMP.chest.xr.standard        → Impression       ─┘ CPT codes
```

### Component Naming Pattern

| Prefix | Type | Example |
|--------|------|---------|
| `HDR.` | Header | `HDR.ct.abdomen` |
| `TEC.` | Technique | `TEC.mri.brain.without` |
| `SUB.` | Subcomponent | `SUB.ct.chest.lungs_airways_pleura` |
| `ATM.` | Atomic Element | `ATM.lungs.opacities` |
| `IMP.` | Impression | `IMP.mri.spine.lumbar` |

## CPT Mapping Files

Each mapping file contains:
- CPT code definitions with variants
- Component references for each code
- Shared subcomponent definitions
- Special protocol configurations (LI-RADS, Lung-RADS, etc.)

### Supported Modalities

| Modality | File(s) | CPT Codes |
|----------|---------|-----------|
| CT | ct_chest.json, ct_abdomen.json | 71250-71275, 74150-74178, etc. |
| MRI | mri_neuro.json | 70551-70553, 72141-72158, etc. |
| X-Ray | xr_chest.json, xr_msk.json | 71045-71048, 72040-73630, etc. |
| Ultrasound | us_abdomen.json | 76700-76981, etc. |
| Nuclear | nuclear.json, pet_ct.json | 78306-78816, etc. |
| Fluoroscopy | fluoro_gi.json | 74220-74400 |
| Mammography | mammo.json | 77063-77067, 19081-19283 |

## Template Variants

Templates may have variants based on:
- **Contrast**: without, with, with_without
- **Gender**: male, female (for anatomical differences)
- **Context**: routine, emergency, trauma, ICU
- **Style**: structured (picklists), free_text
- **Protocol**: PE, dissection, LI-RADS, Lung-RADS, TI-RADS

## Current Statistics

- **4,795 templates** in source XML
- **~200 unique CPT codes** mapped
- **7 modalities** covered
- **4 component layers** defined

## Implementation Phases

1. ✅ **Phase 1: Foundation** - Architecture, folder structure, schemas
2. 🔄 **Phase 2: CPT Mapping** - Map all CPT codes to components
3. ⏳ **Phase 3: Component Extraction** - Extract from existing templates
4. ⏳ **Phase 4: Picklist Development** - Build atomic elements
5. ⏳ **Phase 5: Assembly & Testing** - Validate and test

## How to Use

### Adding a New CPT Code

1. Find the appropriate modality file in `cpt-mapping/`
2. Add a new entry to the `cpt_codes` array
3. Define variants if needed (gender, context, style)
4. Reference existing components or create new ones
5. Update `COMPONENT_CATALOG.md` if adding new components

### Modifying a Component

1. Locate the component in `components/`
2. Make your changes
3. All templates using this component automatically inherit the changes
4. Test affected templates

### Adding a Picklist Option

1. Find the atomic element in `components/atomic/`
2. Add your option to the `options` array
3. Include output text template if applicable

## Related Files

- Original templates: `source/AutoTextExport (46).xml`
- CPT reference: `source/cpt-code-2024.pdf`
- Existing template naming: Maps to `architecture/NAMING_CONVENTIONS.md`

## Notes

- This is a mapping/planning system - actual template content is in the XML
- Component IDs use dot notation (e.g., `SUB.ct.chest.lungs`)
- Gender-specific variants exist for anatomical differences (pelvis, etc.)
- Special protocols (LI-RADS, etc.) have dedicated component sets
