# Component Catalog

Master catalog of all reusable components in the Template Map system.

---

## Component Types

| Prefix | Type | Description |
|--------|------|-------------|
| `CR-` | Chest Radiograph | X-Ray chest finding components |
| `AR-` | Abdominal Radiograph | X-Ray abdomen finding components |
| `XR-` | X-Ray General | X-Ray spine, MSK components |
| `CT-` | CT | CT finding components |
| `US-` | Ultrasound | Ultrasound finding components |
| `MR-` | MRI | MRI finding components |
| `NM-` | Nuclear Medicine | Nuclear medicine components |

---

## Chest Radiograph Components (CR-)

### CR-devices
**Display Name:** Lines and Tubes  
**Description:** Support devices on chest radiograph

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `ett` | Endotracheal Tube | None, Good position, Low, High, Mainstem |
| `ngt` | Enteric Tube | None, Stomach, Esophagus, Malpositioned |
| `central_line` | Central Venous Catheter | None, RIJ, LIJ, Subclavian, PICC, Port |
| `chest_tube` | Chest Tube | None, Right, Left, Malpositioned |
| `pacer` | Pacemaker/ICD | None, Single, Dual, BiV, ICD |
| `trach` | Tracheostomy Tube | None, Good position, Low, High |
| `swan_ganz` | Swan-Ganz Catheter | None, Good position, Too distal |
| `iabp` | Intra-aortic Balloon Pump | None, Good position, Malpositioned |

**Used By:** xr-chest-portable

---

### CR-lungsandpleura
**Display Name:** Lungs and Pleura  
**Description:** Pulmonary and pleural findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `lung_opacities` | Lung Opacities | Clear, Consolidation, GGO, Atelectasis, Mass |
| `pleural_effusion` | Pleural Effusion | None, Small, Moderate, Large |
| `pneumothorax` | Pneumothorax | None, Small, Moderate, Large, Tension |
| `lung_volumes` | Lung Volumes | Normal, Hyperinflated, Low |

**Used By:** xr-chest-portable, xr-chest-2view, xr-chest-3plus, xr-ribs

---

### CR-heartmediastinum
**Display Name:** Heart and Mediastinum  
**Description:** Cardiac and mediastinal findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `cardiac_size` | Cardiac Size | Normal, Mildly enlarged, Moderately enlarged, Severely enlarged |
| `cardiac_contour` | Cardiac Contour | Normal, Abnormal |
| `mediastinum` | Mediastinal Contours | Normal, Widened, Mass |
| `aorta` | Aortic Contour | Normal, Tortuous, Aneurysmal, Calcified |

**Used By:** xr-chest-portable, xr-chest-2view, xr-chest-3plus, xr-ribs

---

### CR-bones
**Display Name:** Bones and Soft Tissues  
**Description:** Osseous and soft tissue findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `ribs` | Rib Findings | Normal, Fracture, Healed fracture, Metastatic |
| `spine` | Spine Findings | Normal, Degenerative, Compression fracture |
| `soft_tissue` | Soft Tissue | Normal, Subcutaneous emphysema, Mass |
| `clavicle` | Clavicle | Normal, Fracture, Healed fracture |

**Used By:** xr-chest-2view, xr-chest-3plus, xr-ribs

---

## Abdominal Radiograph Components (AR-)

### AR-bowelgas
**Display Name:** Bowel Gas Pattern  
**Description:** GI tract gas distribution

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `gas_pattern` | Bowel Gas Pattern | Nonobstructive, SBO pattern, LBO pattern, Ileus |
| `free_air` | Pneumoperitoneum | None, Present |
| `distension` | Bowel Distension | None, Mild, Moderate, Severe |

**Used By:** xr-abdomen, xr-acute-abdomen

---

### AR-solidorgans
**Display Name:** Solid Organs  
**Description:** Visible solid organ findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `liver` | Liver | Normal, Hepatomegaly, Calcification |
| `spleen` | Spleen | Normal, Splenomegaly |
| `kidneys` | Kidneys | Normal, Nephrolithiasis, Enlarged |

**Used By:** xr-abdomen, xr-acute-abdomen

---

## CT Components (CT-)

### CT-brainparenchyma
**Display Name:** Brain Parenchyma  
**Description:** Brain tissue findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `gray_white` | Gray-White Differentiation | Normal, Reduced, Effaced |
| `hemorrhage` | Intracranial Hemorrhage | None, Intraparenchymal, Subarachnoid, Subdural, Epidural |
| `mass_effect` | Mass Effect | None, Mild, Moderate, Severe with herniation |
| `infarct` | Infarct | None, Acute, Subacute, Chronic |

**Used By:** ct-head, cta-head, mri-brain

---

### CT-ventricles
**Display Name:** Ventricles  
**Description:** Ventricular system findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `ventricular_size` | Ventricular Size | Normal, Mildly dilated, Moderately dilated, Severe hydrocephalus |
| `midline` | Midline Shift | None, Mild (<5mm), Moderate (5-10mm), Severe (>10mm) |

**Used By:** ct-head, cta-head, mri-brain

---

### CT-liver
**Display Name:** Liver  
**Description:** Hepatic CT findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `liver_size` | Liver Size | Normal, Hepatomegaly |
| `liver_density` | Liver Density | Normal, Fatty infiltration, Cirrhotic |
| `liver_lesions` | Hepatic Lesions | None, Cyst, Hemangioma, Metastases, HCC |

**Used By:** ct-abdomen-pelvis, mri-abdomen

---

### CT-kidneys
**Display Name:** Kidneys  
**Description:** Renal CT findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `kidney_size` | Kidney Size | Normal, Enlarged, Atrophic |
| `hydronephrosis` | Hydronephrosis | None, Mild, Moderate, Severe |
| `nephrolithiasis` | Stones | None, Nonobstructing, Obstructing |
| `renal_lesions` | Renal Lesions | None, Simple cyst, Complex cyst, Mass |

**Used By:** ct-abdomen-pelvis, us-renal

---

## Ultrasound Components (US-)

### US-liver
**Display Name:** Liver  
**Description:** Hepatic ultrasound findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `echogenicity` | Liver Echogenicity | Normal, Increased (fatty), Coarsened |
| `focal_lesions` | Focal Lesions | None, Cyst, Hemangioma, Solid mass |
| `hepatic_veins` | Hepatic Veins | Patent, Thrombosed |

**Used By:** us-abdomen

---

### US-gallbladder
**Display Name:** Gallbladder  
**Description:** Gallbladder ultrasound findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `gb_wall` | GB Wall | Normal (<3mm), Thickened, Edematous |
| `cholelithiasis` | Gallstones | None, Present, Sludge |
| `pericholecystic` | Pericholecystic Fluid | None, Present |
| `sonographic_murphy` | Sonographic Murphy Sign | Negative, Positive |

**Used By:** us-abdomen

---

### US-kidneys
**Display Name:** Kidneys  
**Description:** Renal ultrasound findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `kidney_size` | Kidney Size | Normal, Enlarged, Atrophic |
| `echogenicity` | Cortical Echogenicity | Normal, Increased |
| `hydronephrosis` | Hydronephrosis | None, Mild, Moderate, Severe |
| `cysts` | Renal Cysts | None, Simple, Complex |
| `stones` | Nephrolithiasis | None, Present |

**Used By:** us-abdomen, us-renal, us-scrotum

---

### US-thyroid
**Display Name:** Thyroid  
**Description:** Thyroid ultrasound findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `thyroid_size` | Thyroid Size | Normal, Enlarged, Atrophic |
| `echogenicity` | Echogenicity | Normal, Heterogeneous |
| `nodules` | Nodules | None, Benign appearing, Indeterminate, Suspicious |
| `tirads` | TI-RADS Category | TR1, TR2, TR3, TR4, TR5 |

**Used By:** us-thyroid

---

## MRI Components (MR-)

### MR-spine-cervical
**Display Name:** Cervical Spine  
**Description:** MRI cervical spine findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `alignment` | Alignment | Normal, Straightened, Kyphotic, Subluxation |
| `cord` | Spinal Cord | Normal, Signal abnormality, Compression |
| `discs` | Disc Levels | Normal, Bulge, Protrusion, Extrusion |
| `stenosis` | Central Stenosis | None, Mild, Moderate, Severe |
| `foraminal` | Foraminal Stenosis | None, Mild, Moderate, Severe |

**Used By:** mri-cspine

---

### MR-spine-lumbar
**Display Name:** Lumbar Spine  
**Description:** MRI lumbar spine findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `alignment` | Alignment | Normal, Lordosis loss, Scoliosis, Spondylolisthesis |
| `conus` | Conus Medullaris | Normal position, Low-lying |
| `discs` | Disc Levels | Normal, Bulge, Protrusion, Extrusion, Sequestration |
| `stenosis` | Central Stenosis | None, Mild, Moderate, Severe |
| `foraminal` | Foraminal Stenosis | None, Mild, Moderate, Severe |
| `facets` | Facet Arthropathy | None, Mild, Moderate, Severe |

**Used By:** mri-lspine, mri-tspine

---

### MR-shoulder
**Display Name:** Shoulder  
**Description:** MRI shoulder findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `rotator_cuff` | Rotator Cuff | Intact, Tendinosis, Partial tear, Full-thickness tear |
| `labrum` | Labrum | Intact, Superior tear, Anterior tear, Posterior tear |
| `biceps` | Biceps Tendon | Normal, Tendinosis, Subluxed, Torn |
| `acromion` | Acromion | Type I, Type II, Type III |
| `ac_joint` | AC Joint | Normal, Arthropathy, Separation |

**Used By:** mri-shoulder

---

## Nuclear Medicine Components (NM-)

### NM-hida
**Display Name:** Hepatobiliary Scan  
**Description:** HIDA scan findings

| Picklist | Display Name | Options |
|----------|--------------|---------|
| `gb_visualization` | GB Visualization | Normal filling, Delayed filling, Non-visualization |
| `ejection_fraction` | Ejection Fraction | Normal (>35%), Reduced |
| `cystic_duct` | Cystic Duct | Patent, Obstructed |
| `cbd` | Common Bile Duct | Patent, Obstructed |

**Used By:** nm-hida

---

## Dependency Matrix

Components shared across multiple templates:

| Component | XR | CT | MRI | US | NM |
|-----------|----|----|-----|----|----|
| Lungs/Pleura | CR- | CT- | - | - | - |
| Heart | CR- | CT- | - | - | - |
| Liver | - | CT- | MR- | US- | NM- |
| Kidneys | AR- | CT- | - | US- | - |
| Brain | - | CT- | MR- | - | - |
| Spine | XR- | CT- | MR- | - | - |
| Bones | CR- | CT- | - | - | NM- |

---

## Adding New Components

1. Choose appropriate prefix based on modality
2. Use descriptive name (lowercase, no spaces)
3. Define picklists with display names
4. Add options with appropriate states
5. Update `routes_to` when adding to templates
6. Update this catalog
