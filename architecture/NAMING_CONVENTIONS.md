# Naming Conventions

Standardized naming conventions for all templates, components, and picklists.

---

## General Rules

1. **Use lowercase** with hyphens for template IDs
2. **Use PascalCase prefixes** for component IDs (e.g., CR-, CT-, US-)
3. **Use underscores** for picklist IDs within components
4. **Be descriptive** - names should be self-documenting
5. **Be consistent** - similar items follow the same pattern

---

## Template Naming

### Template ID Pattern
```
{modality}-{body_region}[-{variant}]
```

### Examples
```
xr-chest-portable      # XR Chest portable/1 view
xr-chest-2view         # XR Chest 2 views
ct-head                # CT Head
ct-abdomen-pelvis      # CT Abdomen and Pelvis
mri-brain              # MRI Brain
mri-lspine             # MRI Lumbar Spine
us-abdomen             # US Abdomen
```

---

## Component Naming

### Component ID Pattern
```
{PREFIX}-{description}
```

### Modality Prefixes

| Prefix | Modality | Full Name |
|--------|----------|-----------|
| `CR-` | XR Chest | Chest Radiograph |
| `AR-` | XR Abdomen | Abdominal Radiograph |
| `XR-` | XR General | X-Ray (spine, MSK) |
| `CT-` | CT | Computed Tomography |
| `US-` | Ultrasound | Ultrasound |
| `MR-` | MRI | Magnetic Resonance |
| `NM-` | Nuclear | Nuclear Medicine |

### Component Examples
```
CR-devices             # Chest X-Ray: Lines and tubes
CR-lungsandpleura      # Chest X-Ray: Lungs and pleura
CR-heartmediastinum    # Chest X-Ray: Heart and mediastinum
CR-bones               # Chest X-Ray: Bones

AR-bowelgas            # Abdominal X-Ray: Bowel gas pattern
AR-solidorgans         # Abdominal X-Ray: Solid organs
AR-bones               # Abdominal X-Ray: Bones

CT-brainparenchyma     # CT: Brain parenchyma
CT-ventricles          # CT: Ventricles
CT-liver               # CT: Liver
CT-kidneys             # CT: Kidneys

US-liver               # Ultrasound: Liver
US-gallbladder         # Ultrasound: Gallbladder
US-kidneys             # Ultrasound: Kidneys
US-thyroid             # Ultrasound: Thyroid

MR-spine-cervical      # MRI: Cervical spine
MR-spine-lumbar        # MRI: Lumbar spine
MR-shoulder            # MRI: Shoulder
```

---

## Picklist Naming

### Picklist ID Pattern
```
{structure}_{finding_type}
```

### Examples
```
ett                    # Endotracheal tube
ngt                    # Nasogastric tube
central_line           # Central venous catheter
chest_tube             # Chest tube
pacer                  # Pacemaker/ICD

lung_opacities         # Pulmonary opacities
pleural_effusion       # Pleural effusion
pneumothorax           # Pneumothorax

cardiac_size           # Cardiac size
mediastinal_contours   # Mediastinal contours

liver_size             # Liver size
liver_lesions          # Hepatic lesions
```

---

## Option ID Pattern

### Format
```
{picklist_id}-{descriptor}
```

### Examples
```
ett-none               # No ETT
ett-good               # ETT in good position
ett-low                # ETT positioned low
ett-mainstem           # ETT in mainstem bronchus

ngt-none               # No enteric tube
ngt-good               # NGT in stomach
ngt-esoph              # NGT in esophagus

cvc-none               # No central line
cvc-rij                # Right IJ catheter
cvc-lsc                # Left subclavian catheter
```

---

## State Values

Option states use lowercase identifiers:

| State | Description |
|-------|-------------|
| `absent` | Structure/device not present |
| `normal` | Normal finding |
| `abnormal` | Abnormal finding |
| `critical` | Critical finding |
| `chronic` | Chronic/stable finding |
| `benign` | Benign finding |
| `surgical` | Post-surgical state |
| `device` | Device present and positioned |
| `limitation` | Technical limitation |

---

## Modality Abbreviations

| Abbreviation | Full Name |
|--------------|-----------|
| `xray` / `xr` | X-Ray / Radiograph |
| `ct` | Computed Tomography |
| `cta` | CT Angiography |
| `mri` | Magnetic Resonance Imaging |
| `mra` | MR Angiography |
| `us` | Ultrasound |
| `nm` | Nuclear Medicine |
| `pet` | PET/CT |
| `fluoro` | Fluoroscopy |
| `dexa` | Bone Densitometry |

---

## Body Region Terms

| Term | Description |
|------|-------------|
| `chest` | Thorax |
| `abdomen` | Abdomen |
| `pelvis` | Pelvis |
| `head` | Head/Brain |
| `neck` | Neck |
| `cspine` | Cervical spine |
| `tspine` | Thoracic spine |
| `lspine` | Lumbar spine |
| `shoulder` | Shoulder |
| `knee` | Knee |
| `ankle` | Ankle |

---

## File Naming

### JSON Files
```
template-map.json      # All template definitions
component-map.json     # All component definitions
```

### Template Files
```
{cpt}-{modality}-{region}[-variant].json
```

Examples:
```
71046-xr-chest-2view.json
74177-ct-abdomen-pelvis-w.json
70551-mri-brain-wo.json
```

### Component Files
```
{component-id}.json
```

Examples:
```
CR-lungsandpleura.json
CT-liver.json
US-gallbladder.json
```

---

## Reserved Terms

Avoid these legacy terms:
- `master` (use template or component)
- `root` (use template)
- `sub` (use component)
- `final` (not needed)
- `AT` (use template)
- `FM` (use structured)
