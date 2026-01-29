# Naming Conventions

This document defines the standardized naming conventions for all components in the template mapping system.

---

## General Rules

1. **Use lowercase** for all identifiers (except CPT codes)
2. **Use dots (.)** to separate hierarchical levels
3. **Use underscores (_)** for multi-word elements within a level
4. **Be consistent** - same structure = same name pattern
5. **Be specific** - names should be self-documenting

---

## CPT Code Template Names

### Pattern
```
CPT.{cpt_code}[-{variant_id}]
```

### Examples
```
CPT.71046              # Base template for CPT 71046
CPT.71046-GT40         # Variant for patients >40 years old
CPT.74177-F            # Female variant
CPT.74177-M            # Male variant
CPT.74177-ER           # Emergency variant
```

---

## Component ID Patterns

### Header Components (HDR.)
```
HDR.{modality}.{body_region}[.{variant}]
```

**Examples:**
```
HDR.ct.standard               # Standard CT header
HDR.ct.abdomen                # CT Abdomen header
HDR.ct.abdomen_pelvis         # CT Abd/Pel header
HDR.ct.cardiac                # CT Cardiac header
HDR.mri.brain                 # MRI Brain header
HDR.mri.spine.cervical        # MRI C-spine header
HDR.us.abdomen                # US Abdomen header
HDR.us.abdomen.limited        # US Abdomen Limited header
HDR.nm.cardiac                # NM Cardiac header
HDR.pet.body                  # PET/CT Body header
HDR.emergency                 # Universal emergency header
HDR.icu                       # Universal ICU header
```

### Technique Components (TEC.)
```
TEC.{modality}.{body_region}.{contrast|protocol}
```

**Examples:**
```
TEC.ct.chest.without          # CT Chest without contrast
TEC.ct.chest.with             # CT Chest with contrast
TEC.ct.chest.with_without     # CT Chest with and without
TEC.ct.chest.low_dose         # LDCT technique
TEC.cta.chest                 # CTA Chest
TEC.mri.brain.without         # MRI Brain without
TEC.mri.spine.cervical.with   # MRI C-spine with contrast
TEC.mra.head.tof              # MRA Head time-of-flight
TEC.us.abdomen.complete       # US Abdomen complete
TEC.nm.myocardial_perfusion   # NM MPI technique
```

### Subcomponents (SUB.)
```
SUB.{modality}.{body_region}.{section_name}
```

**Examples:**
```
SUB.ct.chest.lungs_airways_pleura      # CT chest lungs section
SUB.ct.chest.mediastinum_hila          # CT chest mediastinum section
SUB.ct.abd.liver                       # CT abdomen liver section
SUB.ct.abd.gallbladder_biliary         # CT abdomen GB section
SUB.ct.pel.bladder                     # CT pelvis bladder section
SUB.ct.pel.reproductive_female         # CT pelvis female repro organs
SUB.mri.brain.parenchyma               # MRI brain parenchyma
SUB.mri.spine.cord                     # MRI spine cord
SUB.mri.spine.discs_lumbar             # MRI lumbar discs
SUB.us.abd.liver                       # US abdomen liver
SUB.us.thyroid.nodules                 # US thyroid nodules
SUB.cta.chest.pulmonary_arteries       # CTA chest PA section
SUB.mra.head.anterior_circulation      # MRA head anterior circ
```

### Atomic Elements (ATM.)
```
ATM.{organ|structure}.{finding_type}
```

**Examples:**
```
ATM.lungs.opacities           # Lung opacity picklist
ATM.lungs.volumes             # Lung volume options
ATM.lungs.nodules             # Lung nodule options
ATM.pleura.effusion           # Pleural effusion options
ATM.pleura.pneumothorax       # Pneumothorax options
ATM.heart.size                # Cardiac size options
ATM.heart.contour             # Cardiac contour options
ATM.liver.size                # Liver size options
ATM.liver.lesions             # Liver lesion options
ATM.kidney.cysts              # Renal cyst options
ATM.spine.disc_herniation     # Disc herniation options
ATM.devices.ett               # ETT position options
ATM.devices.cvl               # CVL position options
```

### Impression Components (IMP.)
```
IMP.{modality}.{body_region}[.{variant}]
```

**Examples:**
```
IMP.normal                    # Universal normal impression
IMP.ct.chest.standard         # CT Chest impression
IMP.cta.chest                 # CTA Chest impression
IMP.ct.lung_rads              # Lung-RADS impression
IMP.ct.abd_pel.standard       # CT Abd/Pel impression
IMP.mri.brain.standard        # MRI Brain impression
IMP.us.thyroid                # US Thyroid (TI-RADS) impression
IMP.pet.oncology              # PET oncology impression
```

---

## Modality Abbreviations

| Abbreviation | Full Name |
|--------------|-----------|
| `xr` | X-Ray / Radiograph |
| `ct` | Computed Tomography |
| `cta` | CT Angiography |
| `mri` | Magnetic Resonance Imaging |
| `mra` | MR Angiography |
| `us` | Ultrasound |
| `nm` | Nuclear Medicine |
| `pet` | PET/CT |
| `fluoro` | Fluoroscopy |
| `mammo` | Mammography |

---

## Body Region Abbreviations

| Abbreviation | Full Name |
|--------------|-----------|
| `chest` | Chest/Thorax |
| `abd` | Abdomen |
| `pel` | Pelvis |
| `abd_pel` | Abdomen and Pelvis |
| `neuro` | Neuroimaging (Brain/Spine) |
| `brain` | Brain |
| `spine` | Spine (general) |
| `cervical` | Cervical Spine |
| `thoracic` | Thoracic Spine |
| `lumbar` | Lumbar Spine |
| `head` | Head |
| `neck` | Neck |
| `msk` | Musculoskeletal |
| `cardiac` | Cardiac |
| `vascular` | Vascular |

---

## Contrast Abbreviations

| Term | Meaning |
|------|---------|
| `without` | Without IV contrast |
| `with` | With IV contrast |
| `with_without` | With and without contrast |
| `na` | Not applicable |

---

## Variant Identifiers

### Clinical Context
| Code | Meaning |
|------|---------|
| `STD` | Standard/Routine |
| `OP` | Outpatient |
| `IP` | Inpatient |
| `ER` | Emergency |
| `ICU` | Intensive Care Unit |
| `TRAUMA` | Trauma protocol |

### Patient Demographics
| Code | Meaning |
|------|---------|
| `F` | Female |
| `M` | Male |
| `PED` | Pediatric |
| `GT40` | Greater than 40 years |
| `18-40` | 18-40 years |

### Reporting Style
| Code | Meaning |
|------|---------|
| `FREE` | Free text |
| `STRUCT` | Structured/Picklist |
| `FM` | Formatted/Macro-based |

### Special Protocols
| Code | Meaning |
|------|---------|
| `PE` | Pulmonary embolism protocol |
| `DISSECTION` | Aortic dissection protocol |
| `LIRADS` | LI-RADS liver protocol |
| `LUNGRADS` | Lung-RADS screening |
| `TIRADS` | TI-RADS thyroid |
| `BIRADS` | BI-RADS breast |

---

## File Naming

### CPT Mapping Files
```
{modality}_{body_region}.json
```

**Examples:**
```
ct_chest.json
ct_abdomen.json
mri_neuro.json
us_abdomen.json
xr_chest.json
```

### Component Files
```
{component_id}.json
```

**Examples:**
```
SUB.chest.xr.lungs_pleura.json
ATM.lungs.opacities.json
HDR.ct.standard.json
```

---

## Template Name Mapping (Legacy to New)

When mapping existing template names to new component IDs:

| Legacy Name | New Component ID |
|-------------|------------------|
| `chest XR chest master header` | `HDR.chest.xr.standard` |
| `chest XR chest master root` | `CPT.71046` |
| `chest CT chest findings FM` | `FND.ct.chest.structured` |
| `Lungs, Airways and Pleura CT sub final` | `SUB.ct.chest.lungs_airways_pleura` |
| `abd CT abd/pel with female (CT3043)` | `CPT.74177-F` |
| `abd CT master findings abd/pel female*` | `FND.ct.abd_pel.female` |

---

## Reserved Words

Avoid using these as component identifiers:
- `master` (legacy system term)
- `root` (legacy system term)
- `sub` (use `SUB.` prefix instead)
- `final` (legacy system term)
- `AT` (autotext - legacy)
- `FM` (formatted macro - use `STRUCT`)
