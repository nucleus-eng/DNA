# DNA

This repository contains sequence files for the Nucleus Distribution DNA library. It is the companion DNA registry to the [Nucleus Distribution documentation](https://docs.nucleus.engineering), which describes the protocols and modules that use these parts.

All files are in GenBank format and can be opened in [Benchling](https://benchling.com), [Snapgene](https://www.snapgene.com/), or any other sequence editor that supports the GenBank format. Most carry a `.gb` extension; two predate that convention and use `.gbk`, and are not renamed because documentation pages link to them by path.

## Naming convention

Most parts in this library use the `pOpen` backbone — a modular cloning (MoClo) compatible entry vector (medium copy, ampicilin resistance). File names follow the pattern `pOpen-[part-name].gb`, where the part name describes the genetic element cloned into the backbone. Expression constructs for PURE system proteins use the `pET28a` backbone (medium copy, kanamycin resistance, lac inducible T7 expression) and follow the pattern `pET28a-[protein-name].gb`.

Linear constructs — amplified fragments used directly in cell-free reactions rather than maintained in a vector — have no backbone to name, and follow the pattern `[regulatory-element]-[payload]-linear.gb`.

**A construct carrying two modules' elements is filed under the module its payload serves.** `pT7-tetO-PLA1-linear.gb` puts a tetR-aTc operator and a PLA1 coding sequence on one molecule; it is filed under `effectors/`, because PLA1 is what it makes. Its detector membership is recorded in `manifest.tsv`, not in the path. This follows the earlier `emitters/pT7-tetO-tetO-bjaI-linear.gb`, filed by its bjaI payload for the same reason.

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
├── effectors/           # payloads that act on the synthetic cell itself
│   └── <module>/        # grouped by the docs module the payload serves
├── reporters/
│   └── <module>/        # linear reporter constructs, grouped as above
└── detectors/
    ├── quorum-sensing/  # BjaI/BjaR components
    ├── <module>/        # grouped by the docs module the construct serves
    └── ...              # LacI/TetR-based repressor and operator constructs
```

Where a directory nests a second level, that level is named for the module directory in [the Nucleus Distribution documentation](https://docs.nucleus.engineering) — `detector-ph/`, `detector-tetr-atc/`, `detector-3oc6-hsl/`. Parts that predate this convention stay at the root of their directory; nothing has been moved.

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

Subdirectories hold linear constructs in which a detector's regulatory element drives a reporter — deGFP for a fluorescent readout, C23DO for a colorimetric one. These are used directly in cell-free reactions and are not maintained in a vector.

---

### `pores/` — Passive transport through the membrane

The `pores/` directory contains passive transport membrane channel proteins for use in synthetic cells. Includes [Cx43 and Cx43-eGFP](https://docs.nucleus.engineering/docs/modules/membrane-pore-cx43/spec/) in pOpen.

---

### `energy/` — Metabolism modules that generate energy-carrying molecules

The `energy/` directory contains modules that generate energy carrying molecules (e.g., rATP, CP). Includes [PPK](https://docs.nucleus.engineering/docs/modules/energy-ppk/spec/) in pOpen.

---


### `emitters/` — Signal emission 

The `emitters/` directory contains constructs for signal emission modules, typically small molecule generators. Includes [bjaI (tet regulation)](https://docs.nucleus.engineering/docs/implementations/responder-atc-ivhsl/main/), which produces the quorum sensing module IV-HSL. Also includes `luxI-linear.gb`, the LuxI synthase.

**BjaI and LuxI are not the same system.** BjaI produces IV-HSL (a branched-chain acyl-homoserine lactone, detected by BjaR); LuxI produces 3OC6-HSL (detected by LuxR). Both are commonly shortened to "AHL" and they are not interchangeable. `luxI-linear.gb` is driven by a *lacUV5* promoter for expression in *E. coli* rather than in a synthetic cell, and no module currently claims it.

---

### `effectors/` — Payloads that act on the synthetic cell itself

The `effectors/` directory contains constructs whose payload changes the cell that expresses it, rather than emitting, reporting or modulating a signal. Currently [PLA1](https://docs.nucleus.engineering/docs/modules/effector-pla1/spec/), a phospholipase from *Serratia* sp. MK1 that lyses phospholipid membranes and so releases whatever a compartment holds.

Every construct here is a linear fusion: a detector's regulatory element driving PLA1. They are grouped by the detector that gates them — `detector-ph/`, `detector-tetr-atc/`, `detector-3oc6-hsl/` — because that is the module a reader looks up when choosing one.

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

**`detectors/detector-ph/`** — pH-responsive toehold switch. The two synthesized oligonucleotides that make up the sensing element:
- `pH-responsive-ssDNA-2.gb` — the pH-responsive strand
- `trigger-ssDNA-3.gb` — the trigger strand it releases on acidification

**`detectors/detector-3oc6-hsl/`** — LuxR/pLux quorum sensing, responding to 3OC6-HSL:
- `J23101-luxR-linear.gb` — constitutive LuxR receiver

**`detectors/quorum-sensing/`** — BjaI/BjaR quorum sensing system from *Bradyrhizobium japonicum*:
- `pOpen-pT7-bjaI.gb` — BjaI synthase (signal production)
- `pOpen-bjaR-GFP-native.gb` — BjaR receptor fused to GFP reporter under native promoter. Used in an _E. coli_ strain as a reporter for signal emitted by a syncell with bjaI.

---

## `manifest.tsv` — which modules use which construct

A construct can serve several modules, and a module can need several constructs. Directories are a tree and cannot hold that relation, so it lives in `manifest.tsv` at the repository root:

| column | meaning |
| --- | --- |
| `file` | path, relative to the repository root |
| `modules` | comma-separated module directory names from `docs.nucleus.engineering`, listing **direct membership only**; empty when no module claims the construct |
| `state` | `built` if the construct has been amplified and purified, `designed` if it exists only as a sequence |

**Direct membership means the module whose own composition names this construct**, not every module that inherits it. A fusion carries two modules' elements and so lists two. A sensing cell that composes a detector does *not* appear — follow `# Constituent Modules` on the module pages to get the full set. Listing the closure here would state the same relation twice, and the two copies would drift.

The directory a file sits in records **one** of its memberships — the one its payload serves. The manifest records all of them. When the two seem to disagree, the manifest is the complete answer and the path is a filing decision.

An empty `modules` column is information, not an omission: it marks a sequence the documentation does not yet describe.

---

## Relationship to Nucleus Distribution docs

Protocol pages in the [Nucleus Distribution documentation](https://docs.nucleus.engineering) reference specific constructs from this repository by filename. When a protocol calls for a specific plasmid, the corresponding `.gb` file can be found here.

**Paths in this repository are a public interface.** Documentation pages link to files as `github.com/nucleus-eng/DNA/blob/main/<path>`, so moving or renaming a file breaks those links silently — the docs' own link checker cannot see across repositories. Add new directories freely; do not reorganize existing ones without fixing the links in the same change.
