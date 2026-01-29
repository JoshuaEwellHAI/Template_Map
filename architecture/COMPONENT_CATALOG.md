# Component Catalog

This document catalogs all reusable components in the template mapping system.

## Component Types

| Prefix | Type | Description |
|--------|------|-------------|
| `HDR.` | Header | Report header components (exam info, indication, comparison) |
| `TEC.` | Technique | Technique/protocol description components |
| `FND.` | Findings | Complete findings section containers |
| `SUB.` | Subcomponent | Individual finding sections within findings |
| `ATM.` | Atomic | Smallest picklist elements |
| `IMP.` | Impression | Impression/conclusion components |

---

## Header Components (HDR.)

### Standard Headers
| Component ID | Name | Used By |
|--------------|------|---------|
| `HDR.standard` | Universal Standard Header | All modalities |
| `HDR.emergency` | Emergency Header | ER templates |
| `HDR.icu` | ICU Header | ICU templates |

### CT Headers
| Component ID | Name | Used By |
|--------------|------|---------|
| `HDR.ct.standard` | CT Standard Header | Most CT exams |
| `HDR.ct.abdomen` | CT Abdomen Header | CT Abd |
| `HDR.ct.abdomen_pelvis` | CT Abd/Pel Header | CT Abd/Pel |
| `HDR.ct.cardiac` | CT Cardiac Header | Calcium Score, CTA Coronary |
| `HDR.cta.abdomen` | CTA Abdomen Header | CTA Abd |
| `HDR.cta.abdomen_pelvis` | CTA Abd/Pel Header | CTA Abd/Pel |
| `HDR.ct.lung_screening` | Lung Screening Header | LDCT |

### MRI Headers
| Component ID | Name | Used By |
|--------------|------|---------|
| `HDR.mri.brain` | MRI Brain Header | MRI Brain |
| `HDR.mri.brain.spectroscopy` | MRS Header | Brain Spectroscopy |
| `HDR.mri.spine.cervical` | MRI C-spine Header | MRI C-spine |
| `HDR.mri.spine.thoracic` | MRI T-spine Header | MRI T-spine |
| `HDR.mri.spine.lumbar` | MRI L-spine Header | MRI L-spine |
| `HDR.mra.head` | MRA Head Header | MRA Head |
| `HDR.mra.neck` | MRA Neck Header | MRA Neck |

### X-Ray Headers
| Component ID | Name | Used By |
|--------------|------|---------|
| `HDR.chest.xr.standard` | Chest XR Standard | All chest XR |

### Ultrasound Headers
| Component ID | Name | Used By |
|--------------|------|---------|
| `HDR.us.abdomen` | US Abdomen Header | US Abd Complete |
| `HDR.us.abdomen.limited` | US Abd Limited Header | US Abd Limited |
| `HDR.us.thyroid` | US Thyroid Header | US Thyroid |
| `HDR.us.renal` | US Renal Header | US Renal |

### Nuclear Medicine Headers
| Component ID | Name | Used By |
|--------------|------|---------|
| `HDR.nm.cardiac` | NM Cardiac Header | MPI |
| `HDR.nm.bone` | NM Bone Header | Bone Scan |
| `HDR.pet.body` | PET Body Header | PET/CT Body |

---

## Technique Components (TEC.)

### CT Techniques
| Component ID | Protocol |
|--------------|----------|
| `TEC.ct.chest.without` | CT Chest without contrast |
| `TEC.ct.chest.with` | CT Chest with contrast |
| `TEC.ct.chest.with_without` | CT Chest with and without |
| `TEC.ct.chest.low_dose` | LDCT Lung Screening |
| `TEC.cta.chest` | CTA Chest (PE/routine) |
| `TEC.ct.abd.without` | CT Abd without |
| `TEC.ct.abd.with` | CT Abd with |
| `TEC.ct.abd.with_without` | CT Abd with and without |
| `TEC.ct.abd_pel.without` | CT Abd/Pel without |
| `TEC.ct.abd_pel.with` | CT Abd/Pel with |
| `TEC.ct.abd_pel.multiphase` | CT Abd/Pel multiphase |

### MRI Techniques
| Component ID | Protocol |
|--------------|----------|
| `TEC.mri.brain.without` | MRI Brain without |
| `TEC.mri.brain.with` | MRI Brain with |
| `TEC.mri.brain.with_without` | MRI Brain with and without |
| `TEC.mri.spine.cervical.without` | MRI C-spine without |
| `TEC.mri.spine.lumbar.without` | MRI L-spine without |
| `TEC.mra.head.tof` | MRA Head TOF |
| `TEC.mra.head.contrast` | MRA Head contrast |

### X-Ray Techniques
| Component ID | Protocol |
|--------------|----------|
| `TEC.chest.xr.1view` | Chest XR 1 view |
| `TEC.chest.xr.2view` | Chest XR 2 views |
| `TEC.chest.xr.4view` | Chest XR 4 views |
| `TEC.chest.xr.apical_lordotic` | Chest XR AP Lordotic |

---

## Subcomponent Catalog (SUB.)

### Chest Subcomponents

#### X-Ray Chest
| Component ID | Section Name | Atomic Elements |
|--------------|--------------|-----------------|
| `SUB.chest.xr.exam_quality` | Exam Quality | ATM.exam_quality.* |
| `SUB.chest.xr.support_devices` | Support Devices | ATM.devices.* |
| `SUB.chest.xr.lungs_pleura` | Lungs and Pleura | ATM.lungs.*, ATM.pleura.* |
| `SUB.chest.xr.heart_mediastinum` | Heart and Mediastinum | ATM.heart.*, ATM.mediastinum.* |
| `SUB.chest.xr.bones_soft_tissue` | Bones and Soft Tissues | ATM.bones.*, ATM.soft_tissue.* |
| `SUB.chest.xr.upper_abdomen` | Upper Abdomen | ATM.upper_abd.* |

#### CT Chest
| Component ID | Section Name | Atomic Elements |
|--------------|--------------|-----------------|
| `SUB.ct.chest.exam_quality` | Exam Quality | ATM.quality.* |
| `SUB.ct.chest.lungs_airways_pleura` | Lungs, Airways and Pleura | ATM.lungs.*, ATM.airways.*, ATM.pleura.* |
| `SUB.ct.chest.mediastinum_hila` | Mediastinum and Hila | ATM.mediastinum.*, ATM.hila.* |
| `SUB.ct.chest.heart_pericardium` | Heart and Pericardium | ATM.heart.*, ATM.pericardium.* |
| `SUB.ct.chest.aorta_great_vessels` | Aorta and Great Vessels | ATM.aorta.*, ATM.great_vessels.* |
| `SUB.ct.chest.bones` | Bones | ATM.bones.* |
| `SUB.ct.chest.chest_wall` | Chest Wall | ATM.chest_wall.* |
| `SUB.ct.chest.upper_abdomen` | Upper Abdomen | ATM.liver.*, ATM.adrenals.*, ATM.kidneys.* |
| `SUB.cta.chest.pulmonary_arteries` | Pulmonary Arteries | ATM.pa.* |

### Abdomen Subcomponents

#### CT Abdomen
| Component ID | Section Name | Atomic Elements |
|--------------|--------------|-----------------|
| `SUB.ct.abd.liver` | Liver | ATM.liver.* |
| `SUB.ct.abd.gallbladder_biliary` | Gallbladder and Biliary | ATM.gb.*, ATM.bile_ducts.* |
| `SUB.ct.abd.pancreas` | Pancreas | ATM.pancreas.* |
| `SUB.ct.abd.spleen` | Spleen | ATM.spleen.* |
| `SUB.ct.abd.adrenals` | Adrenal Glands | ATM.adrenal.* |
| `SUB.ct.abd.kidneys` | Kidneys | ATM.kidney.* |
| `SUB.ct.abd.kidneys_ureters` | Kidneys and Ureters | ATM.kidney.*, ATM.ureter.* |
| `SUB.ct.abd.gi_tract` | GI Tract | ATM.stomach.*, ATM.small_bowel.*, ATM.colon.*, ATM.appendix.* |
| `SUB.ct.abd.mesentery` | Mesentery and Peritoneum | ATM.mesentery.*, ATM.peritoneum.* |
| `SUB.ct.abd.retroperitoneum` | Retroperitoneum | ATM.retro.* |
| `SUB.ct.abd.vasculature` | Abdominal Vasculature | ATM.aorta.abdominal, ATM.ivc.*, ATM.portal_vein.* |

#### CT Pelvis
| Component ID | Section Name | Atomic Elements |
|--------------|--------------|-----------------|
| `SUB.ct.pel.bladder` | Bladder | ATM.bladder.* |
| `SUB.ct.pel.reproductive_female` | Female Reproductive | ATM.uterus.*, ATM.ovaries.*, ATM.adnexa.* |
| `SUB.ct.pel.reproductive_male` | Male Reproductive | ATM.prostate.*, ATM.seminal_vesicles.* |

### Neuro Subcomponents

#### MRI Brain
| Component ID | Section Name | Atomic Elements |
|--------------|--------------|-----------------|
| `SUB.mri.brain.parenchyma` | Brain Parenchyma | ATM.brain.white_matter, ATM.brain.gray_matter, ATM.brain.signal_abnormality |
| `SUB.mri.brain.ventricles` | Ventricles | ATM.brain.ventricle_size, ATM.brain.hydrocephalus |
| `SUB.mri.brain.extra_axial` | Extra-axial Spaces | ATM.brain.subdural, ATM.brain.epidural, ATM.brain.subarachnoid |
| `SUB.mri.brain.enhancement` | Enhancement | ATM.brain.enhancement_pattern |
| `SUB.mri.brain.posterior_fossa` | Posterior Fossa | ATM.brain.cerebellum, ATM.brain.brainstem |
| `SUB.mri.brain.orbits_iac` | Orbits and IACs | ATM.orbits.*, ATM.iac.* |
| `SUB.mri.brain.calvarium` | Calvarium | ATM.skull.* |

#### MRI Spine
| Component ID | Section Name | Atomic Elements |
|--------------|--------------|-----------------|
| `SUB.mri.spine.alignment` | Alignment | ATM.spine.alignment |
| `SUB.mri.spine.cord` | Spinal Cord | ATM.spine.cord_signal, ATM.spine.cord_size, ATM.spine.cord_compression |
| `SUB.mri.spine.conus_cauda` | Conus and Cauda | ATM.spine.conus, ATM.spine.cauda |
| `SUB.mri.spine.discs_cervical` | Cervical Discs | ATM.spine.disc_* |
| `SUB.mri.spine.discs_thoracic` | Thoracic Discs | ATM.spine.disc_* |
| `SUB.mri.spine.discs_lumbar` | Lumbar Discs | ATM.spine.disc_* |
| `SUB.mri.spine.neural_foramina` | Neural Foramina | ATM.spine.foramen_* |
| `SUB.mri.spine.facets` | Facet Joints | ATM.spine.facet_* |
| `SUB.mri.spine.vertebral_bodies` | Vertebral Bodies | ATM.spine.vertebra_* |

---

## Atomic Element Catalog (ATM.)

### Lungs
| Element ID | Name | Options |
|------------|------|---------|
| `ATM.lungs.volumes` | Lung Volumes | Normal, Hyperinflated, Low volumes |
| `ATM.lungs.opacities` | Pulmonary Opacities | Clear, Consolidation, GGO, Atelectasis, etc. |
| `ATM.lungs.nodules` | Pulmonary Nodules | None, Single, Multiple with size/location |
| `ATM.lungs.parenchyma` | Lung Parenchyma | Normal, Emphysema, Fibrosis, etc. |

### Pleura
| Element ID | Name | Options |
|------------|------|---------|
| `ATM.pleura.effusion` | Pleural Effusion | None, Small, Moderate, Large; Right/Left/Bilateral |
| `ATM.pleura.pneumothorax` | Pneumothorax | None, Small, Moderate, Large, Tension |
| `ATM.pleura.thickening` | Pleural Thickening | None, Focal, Diffuse |

### Heart
| Element ID | Name | Options |
|------------|------|---------|
| `ATM.heart.size` | Cardiac Size | Normal, Mildly enlarged, Moderately enlarged, Severely enlarged |
| `ATM.heart.contour` | Cardiac Contour | Normal, Abnormal with description |
| `ATM.heart.chambers` | Chamber Size | Normal, LA enlarged, LV dilated, etc. |

### Liver
| Element ID | Name | Options |
|------------|------|---------|
| `ATM.liver.size` | Liver Size | Normal, Hepatomegaly |
| `ATM.liver.echotexture` | Liver Echotexture (US) | Normal, Increased echogenicity (fatty), Coarse |
| `ATM.liver.parenchyma` | Liver Parenchyma (CT/MR) | Normal, Fatty, Cirrhotic |
| `ATM.liver.lesions` | Hepatic Lesions | None, Cyst, Hemangioma, Metastases, HCC, etc. |

### Support Devices
| Element ID | Name | Options |
|------------|------|---------|
| `ATM.devices.ett` | Endotracheal Tube | None, Present with position |
| `ATM.devices.ngt` | Nasogastric Tube | None, Present with position |
| `ATM.devices.cvl` | Central Venous Line | None, Right IJ, Left IJ, Subclavian, PICC |
| `ATM.devices.chest_tube` | Chest Tube | None, Right, Left |
| `ATM.devices.pacer` | Pacemaker/ICD | None, Single lead, Dual chamber, ICD |

---

## Impression Components (IMP.)

| Component ID | Name | Used By |
|--------------|------|---------|
| `IMP.normal` | Normal Study | Any normal exam |
| `IMP.abnormal` | Abnormal Findings | Any abnormal exam |
| `IMP.critical` | Critical Findings | Requires communication |
| `IMP.chest.xr.standard` | Chest XR Impression | Chest XR |
| `IMP.ct.chest.standard` | CT Chest Impression | CT Chest |
| `IMP.cta.chest` | CTA Chest Impression | CTA Chest |
| `IMP.ct.lung_rads` | Lung-RADS Impression | LDCT Lung Screening |
| `IMP.ct.abd.standard` | CT Abd Impression | CT Abdomen |
| `IMP.ct.abd_pel.standard` | CT Abd/Pel Impression | CT Abd/Pel |
| `IMP.mri.brain.standard` | MRI Brain Impression | MRI Brain |
| `IMP.mri.spine.cervical` | MRI C-spine Impression | MRI C-spine |
| `IMP.mri.spine.lumbar` | MRI L-spine Impression | MRI L-spine |
| `IMP.us.abdomen` | US Abdomen Impression | US Abdomen |
| `IMP.us.thyroid` | US Thyroid Impression | US Thyroid (TI-RADS) |

---

## Cross-Reference: Shared Components by Body Region

### Components Used Across Multiple Modalities

| Component | XR | CT | MRI | US | NM |
|-----------|----|----|-----|----|----|
| Lungs/Pleura | ✓ | ✓ | ✓ | - | - |
| Heart | ✓ | ✓ | ✓ | ✓ | ✓ |
| Liver | - | ✓ | ✓ | ✓ | ✓ |
| Kidneys | - | ✓ | ✓ | ✓ | ✓ |
| Spine | ✓ | ✓ | ✓ | - | ✓ |
| Brain | - | ✓ | ✓ | - | ✓ |
| Bones | ✓ | ✓ | ✓ | - | ✓ |
| Aorta | - | ✓ | ✓ | ✓ | - |

---

## Template Dependency Graph Example

```
CPT.71046 (XR Chest 2 Views)
    │
    ├─► HDR.chest.xr.standard
    │       └─► ATM.exam_info
    │       └─► ATM.indication
    │       └─► ATM.comparison
    │
    ├─► TEC.chest.xr.2view
    │
    ├─► SUB.chest.xr.lungs_pleura ◄──────┐
    │       └─► ATM.lungs.opacities      │
    │       └─► ATM.lungs.volumes        │ SHARED
    │       └─► ATM.pleura.effusion      │
    │       └─► ATM.pleura.pneumothorax  │
    │                                    │
    ├─► SUB.chest.xr.heart_mediastinum   │
    │       └─► ATM.heart.size           │
    │       └─► ATM.mediastinum.width    │
    │                                    │
    └─► IMP.chest.xr.standard            │
                                         │
CPT.71045 (XR Chest 1 View) ─────────────┘
CPT.71047 (XR Chest AP Lordotic) ────────┘
CPT.71048 (XR Chest 4 Views) ────────────┘
```

Changes to `SUB.chest.xr.lungs_pleura` automatically propagate to all four CPT templates.
