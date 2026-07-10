# Variant Structure Viewer

Interactive 3D visualization of ClinVar pathogenic variants on AlphaFold protein structures.

## Features

- **967 genes** with ClinVar variant annotations
- **5,030 variant positions** with pathogenicity rates
- **3D protein structures** loaded from AlphaFold (no local files needed)
- **Color-coded spheres** at variant positions (green → yellow → red = benign → pathogenic)
- **Click-to-zoom** on variant positions
- **Tooltip** with variant details on click
- **Searchable variant table** in sidebar

## Quick Start

```bash
# Serve locally
python3 -m http.server 8000

# Open in browser
open http://localhost:8000
```

No dependencies required — just a static HTML file that fetches structures from [AlphaFold](https://alphafold.ebi.ac.uk/).

## File Structure

```
variant-viewer/
├── index.html            # Main application (single HTML file)
├── data/
│   ├── genes.json        # Gene list with UniProt IDs
│   └── variants.json     # Per-position pathogenicity rates
├── scripts/
│   └── prepare_data.py   # Regenerate data from benchmark_v3
└── README.md
```

## Data Source

- **Variants**: ClinVar pathogenic/benign missense variants
- **Structures**: AlphaFold predicted structures (v4)
- **Benchmark**: V3 benchmark dataset (5,932 variants, 973 genes)

## Regenerating Data

If you have the benchmark dataset:

```bash
cd scripts
python3 prepare_data.py
```

This reads `benchmark_v3/data/benchmark_v3.csv` and outputs `data/genes.json` and `data/variants.json`.

## How Pathogenicity Rate is Calculated

For each residue position in a protein:
```
pathogenicity_rate = (# pathogenic variants at position) / (# total variants at position)
```

- **0% (green)**: All variants at this position are benign
- **50% (yellow)**: Equal mix of pathogenic and benign
- **100% (red)**: All variants at this position are pathogenic

## Requirements

- Modern web browser (Chrome, Firefox, Safari, Edge)
- Internet connection (loads protein structures from AlphaFold API)

## License

Data sourced from ClinVar (NCBI) and AlphaFold (EMBL-EBI).
