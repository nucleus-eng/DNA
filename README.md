# DNA

This repository contains sequence files for the Nucleus Distribution DNA library. It is the companion DNA registry to the [Nucleus Distribution documentation](https://docs.nucleus.engineering), which describes the protocols and modules that use these parts.

All files are in GenBank (`.gb`) format and can be opened in [Benchling](https://benchling.com), [Snapgene](https://www.snapgene.com/), [Benchling](https://benchling.com), or any other sequence editor that supports the GenBank format.

## Naming convention

Most parts in this library use the `pOpen` backbone — a modular cloning (MoClo) compatible entry vector (medium copy, ampicilin resistance). File names follow the pattern `pOpen-[part-name].gb`, where the part name describes the genetic element cloned into the backbone. Expression constructs for PURE system proteins use the `pET28a` backbone (medium copy, kanamycin resistance, lac inducible T7 expression) and follow the pattern `pET28a-[protein-name].gb`.

## Repository structure

```
DNA/
├── PURE/
│   ├── cloning/         # pOpen entry vectors for all PURE system proteins
│   └── expression/      # pET28a expression vectors for PURE system proteins
├── assembly/            # MoClo backbone (pOpen-pOpenv3-MCL0)
├── promoters/           # Level-matched T7 promoter library 
├── RBS/                 # Ribosome binding site and UTR parts
├── terminators/         # T7 terminator variants
├── reporters/           # Protein reporter constructs 
├── pores/               # passive membrane transport
├── energy/              # metabolism to boost cytosol performance
├── emitters/            # signal emission 
├── control/             # signal modulation 
└── detectors/
    ├── quorum-sensing/  # Quorum sensing circuit components
    └── ...              # LacI/TetR-based repressor and operator constructs
```

---

## Part types
### `PURE/` — Protein components of PURE system
The `PURE/` directory contains genes encoding the 36 proteins included in the [PURE](https://doi.org/10.1038/90802) cell-free translation system. These genes include all 20 canonical aminoacyl-tRNA synthetases (AlaRS, ArgRS, AsnRS, etc) and methionyl-tRNA formyltransferase (MTF); *E. coli* translation initiation factors (IF1, IF2, IF3), elongation factors (EF-G, EF-Ts, EF-Tu), and release factors (RF1, RF2, RF3, RRF); energy regeneration enzymes (AK, CK, NDK, PPiase), and T7 phage RNA polymerase (T7RNAP). 

This distribution includes several variants of a few genes:
- adenylate kinase (AK) from *E. coli*, *S. cerevisiae*, chicken (*G. gallus*) and rabbit (*O. cuniculus*)
- creatine kinase (CK) from chicken (*G. gallus*) and rabbit (*O. cuniculus*)
- glyRS (heterodimer) as individual monomers (glyS, glyQ) and as integrated transcription units (glyQS, glySQ, glyQS-DualHis)
- pheRS (heterodimer) as individual monomers (pheS, pheT) and as integrated transcription units (pheST, pheTS, pheST-DualHis)

### `PURE/cloning/` — PURE protein cloning vectors

The `PURE/cloning/` directory contains pOpen entry vectors encoding each protein component of the PURE cell-free transcription/translation system. These plasmids are meant to be used for stable maintenance of these genes *in vivo* and downstream assembly into appropriate expression plasmids. They are NOT appropriate to use directly as expression plasmids.

---

### `PURE/expression/` — PURE protein expression vectors

The `PURE/expression/` directory contains pET28a-based expression vectors for producing each PURE system protein in *E. coli*. These are the constructs used for protein production to make the protein components of the PURE system using a lac inducible *E. coli* expression system.

---

### `assembly/` — MoClo backbone

The `assembly/` directory contains the pOpen MoClo backbone vector:
- `pOpen-pOpenv3-MCL0.gb` — MCL0 destination backbone for MoClo Level 0 assembly

---

### `promoters/` — T7 promoter library

The `promoters/` directory contains ten T7 promoter variants (`pOpen-PURET7-1.gb` through `pOpen-PURET7-10.gb`) designed for use in PURE cell-free expression. The variants are level-matched: expression is calibrated relative to `PURET7-10`, which is defined as 1.0. `PURET7-1` has a relative expression of ~0.35, providing approximately a 3× dynamic range across the series.

---

### `RBS/` — Ribosome binding sites and UTRs

The `RBS/` directory contains translation initiation parts:
- `pOpen-RBS.gb` — Elowitz (1999) reference *E. coli* ribosome binding site
- `pOpen-UTR1.gb` — 5′ UTR element

---

### `terminators/` — T7 terminator variants

The `terminators/` directory contains three T7 terminator variants originally developed in [Calvopina-Chavez, Gardner, and Griffitts, 2022](https://doi.org/10.1093/g3journal/jkac070):
- `pOpen-tT7.gb` — native T7 terminator
- `pOpen-tT7hyb6.gb` — hybrid T7 terminator variant 6
- `pOpen-tT7hyb10.gb` — hybrid T7 terminator variant 10

---

### `reporters/` — Protein reporters

The `reporters/` directory contains fluorescent protein and chromoprotein reporter constructs. Includes deGFP, cjBlue, eforRed, plamGFP, amajLime, gfasPurple, meleRFP, and mmilCFP. Several reporters include a lacO operator insert for lac-regulated expression, and some include a C-terminal His6 tag for downstream purification.

---

### `pores/` — Passive transport through the membrane

The `pores/` directory contains passive transport membrane channel proteins for use in synthetic cells. Includes [Cx43 and Cx43-eGFP](https://docs.nucleus.engineering/docs/modules/membrane-pore-cx43/spec/) in pOpen.

---

### `energy/` — Metabolism modules that generate energy-carrying molecules

The `energy/` directory contains modules that generate energy carrying molecules (e.g., rATP, CP). Includes [PPK](https://docs.nucleus.engineering/docs/modules/energy-ppk/spec/) in pOpen.

---


### `emitters/` — Signal emission 

The `emitters/` directory contains constructs for signal emission modules, typically small molecule generators. Includses [bjaI (tet regulation)](https://docs.nucleus.engineering/docs/implementations/responder-atc-ivhsl/main/), which produces the quorum sensing module IV-HSL.

---

### `control/` — Signal modulation

The `control/` directory contains modules that alter or modulate output signals. Includes ClpXP, an ATP-dependent protease that degrades targets with a C-terminal ssrA tag. Constructs used to produce protein components of this module found under `control/protein-purification/` subdirectory.

---

### `detectors/` — Regulatory and sensing circuits

The `detectors/` directory contains constructs for building gene circuits that respond to small molecule inputs.

**Root level** — LacI/TetR-based regulation:
- `pOpen-lacI.gb`, `pOpen-tetR.gb` — repressor expression constructs
- `pOpen-pT7-lacO.gb`, `pOpen-pT7-tetO.gb` — T7 promoters with single operator sites
- `pOpen-pT7-lacO-tetO.gb`, `pOpen-pT7-tetO-lacO.gb` — dual-operator promoters for AND-gate logic

**`detectors/quorum-sensing/`** — BjaI/BjaR quorum sensing system from *Bradyrhizobium japonicum*:
- `pOpen-pT7-bjaI.gb` — BjaI synthase (signal production)
- `pOpen-bjaR-GFP-native.gb` — BjaR receptor fused to GFP reporter under native promoter. Used in an _E. coli_ strain as a reporter for signal emitted by a syncell with bjaI.

---

## Relationship to Nucleus Distribution docs

Protocol pages in the [Nucleus Distribution documentation](https://docs.nucleus.engineering) reference specific constructs from this repository by filename. When a protocol calls for a specific plasmid, the corresponding `.gb` file can be found here.
