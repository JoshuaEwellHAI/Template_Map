# Radiology Template Map

A modular, component-based architecture for radiology reporting templates. Templates are composed of reusable components with picklists, enabling consistent reporting and easy maintenance.

## Quick Start

1. **Run locally**: `python -m http.server 8000`
2. **Open browser**: http://localhost:8000
3. **Or deploy to GitHub Pages**: The `index.html` serves as the main application

## Live Demo

If deployed to GitHub Pages: https://joshuaewellhai.github.io/Template_Map/

## Features

### Template Editor
- **View all templates** organized by modality and body region
- **Universal template structure**: Header, Technique, Comparison, Findings, Impression
- **Create new templates** with full hierarchy
- **Duplicate existing templates** with new CPT codes
- **Add/remove components** from template findings

### Component Management
- **Reusable components** shared across multiple templates
- **Dependency tracking** - see which templates use each component
- **Multiple picklists per component** for different finding categories

### Picklist Editor
- **Create picklists** within components
- **Add/edit/remove options** with clinical states (normal, abnormal, critical, etc.)
- **Color-coded states** for quick visual identification

### Data Persistence
- **Auto-save** to JSON files
- **Unsaved changes warning** before leaving
- **Keyboard shortcut** (Ctrl/Cmd+S) to save

## Directory Structure

```
Template Map/
├── index.html                    # Main application (GitHub Pages entry)
├── template-map-viewer.html      # Template editor application
├── template-map.json             # Template definitions and CPT mappings
├── component-map.json            # Component definitions with picklists
├── README.md                     # This file
│
├── architecture/                 # System design documentation
│   ├── ARCHITECTURE.md          # Core architecture concepts
│   ├── NAMING_CONVENTIONS.md    # Naming standards
│   └── COMPONENT_CATALOG.md     # Component reference
│
├── templates/                    # Individual template JSON files
│   ├── schema/                  # JSON schema for templates
│   ├── xray/                    # X-Ray templates by body region
│   ├── ct/                      # CT templates
│   ├── mri/                     # MRI templates
│   ├── ultrasound/              # Ultrasound templates
│   └── nuclear-medicine/        # Nuclear medicine templates
│
├── components/                   # Component JSON files
│   ├── headers/                 # Header components
│   ├── atomic/                  # Atomic picklist elements
│   ├── findings/                # Finding components
│   ├── xray/                    # X-Ray specific components
│   └── ct/                      # CT specific components
│
├── cpt-mapping/                  # CPT code reference files
│   ├── schema/                  # JSON schemas
│   └── [modality]/              # By modality (ct, mri, xr, us, etc.)
│
└── source/                       # Original source files
    ├── AutoTextExport (46).xml  # Legacy template export
    └── cpt-code-2024.pdf        # CPT code reference
```

## Data Model

### Templates (template-map.json)
Each template represents a radiological exam mapped to CPT codes:

```json
{
  "primary_cpt": "71046",
  "description": "XR Chest, 2 views",
  "component_templates": ["CR-devices", "CR-lungsandpleura", "CR-heartmediastinum"],
  "variants": { "71046": { "description": "2 views" } }
}
```

### Components (component-map.json)
Reusable finding components with picklists:

```json
{
  "CR-lungsandpleura": {
    "display_name": "Lungs and Pleura",
    "routes_to": ["xr-chest-portable", "xr-chest-2view"],
    "picklists": {
      "lung_opacities": {
        "display_name": "Lung Opacities",
        "options": [
          { "state": "normal", "text": "Lungs are clear." },
          { "state": "abnormal", "text": "Opacity in the..." }
        ]
      }
    }
  }
}
```

### Universal Template Structure
Every template follows this structure:

| Section | Type | Description |
|---------|------|-------------|
| **EXAM** | Merge Field | Procedure name from PACS/EMR |
| **DEMOGRAPHICS** | Merge Fields | Patient name, age, sex |
| **CLINICAL HISTORY** | Merge Field | PMHx/Indication from EMR |
| **TECHNIQUE** | Picklist | Study-specific technique options |
| **COMPARISON** | Hybrid | Prior studies (merge field + picklist) |
| **FINDINGS** | Components | Body region components with picklists |
| **IMPRESSION** | AI Field | AI-generated or default "Normal exam." |

## Option States

Each picklist option has a clinical state:

| State | Color | Description |
|-------|-------|-------------|
| `absent` | Gray | Structure/device not present |
| `normal` | Green | Normal finding |
| `abnormal` | Yellow | Abnormal finding requiring attention |
| `critical` | Red | Critical finding requiring immediate action |
| `chronic` | Purple | Chronic/stable finding |
| `benign` | Teal | Definitively benign finding |
| `surgical` | Blue | Post-surgical state |

## Modalities

| Modality | Abbreviation | Templates |
|----------|--------------|-----------|
| X-Ray | XR | Chest, MSK, Abdomen, Spine |
| CT | CT | Head, Neck, Chest, Abdomen/Pelvis |
| MRI | MRI | Brain, Spine, Body, MSK |
| Ultrasound | US | Abdomen, Pelvis, Vascular, OB |
| Fluoroscopy | FL | UGI, Barium studies |
| Nuclear Medicine | NM | VQ scan, HIDA |
| DEXA | DXA | Bone density |

## Current Statistics

- **76 templates** mapped to CPT codes
- **210+ CPT code variants**
- **7 modalities** covered
- Components organized by body region

## Integration

### Merge Fields (HL7/EMR)
The following merge fields are populated from PACS/EMR:
- `Procedures` - Exam name
- `Patient Name`, `Patient Age`, `Patient Sex`
- `PMHx` / `Indication` - Clinical history
- `Prior Studies` / `Comparison` - Prior exams

### AI Integration
The Impression field is designed for AI population:
- Default text: "Normal exam."
- AI can populate structured impressions based on findings

## Development

### Running Locally
```bash
cd "Template Map"
python -m http.server 8000
# Open http://localhost:8000
```

### Deploying to GitHub Pages
1. Push to GitHub repository
2. Enable GitHub Pages in repository settings
3. Set source to main branch, root folder
4. Access at: `https://[username].github.io/[repo-name]/`

### Making Changes
1. Edit templates/components in the viewer UI
2. Click "Save All" or press Ctrl/Cmd+S
3. Changes save to `template-map.json` and `component-map.json`
4. Commit and push to deploy

## Browser Support
- Chrome (recommended)
- Firefox
- Safari
- Edge

Requires JavaScript enabled. File System Access API used for saving (with download fallback).

## License
Internal use only - Harrison.ai
