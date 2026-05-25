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
├── RBS/                 # Ribosome binding site and UTR parts
├── promoters/           # Level-matched T7 promoter library (PURET7-1 through -10)
├── reporters/           # Protein reporter constructs (fluorescent and chromoproteins)
├── terminators/         # T7 terminator variants
└── detectors/
    ├── quorum-sensing/  # Quorum sensing circuit components
    └── ...              # LacI/TetR-based repressor and operator constructs
```

---

## Part types

### `promoters/` — T7 promoter library

The `promoters/` directory contains ten T7 promoter variants (`pOpen-PURET7-1.gb` through `pOpen-PURET7-10.gb`) designed for use in PURE cell-free expression. The variants are level-matched: expression is calibrated relative to `PURET7-10`, which is defined as 1.0. `PURET7-1` has a relative expression of ~0.35, providing approximately a 3× dynamic range across the series.

> **TODO:** Add a table of relative expression levels for PURET7-1 through PURET7-10 and describe the measurement conditions (reporter used, PURE reaction conditions, incubation time/temperature).

---

### `RBS/` — Ribosome binding sites and UTRs

The `RBS/` directory contains translation initiation parts:
- `pOpen-RBS.gb` — Elowitz (1999) reference *E. coli* ribosome binding site
- `pOpen-UTR1.gb` — 5′ UTR element

> **TODO:** Describe the MoClo assembly level for these parts and the compatible overhang sequences.

---

### `assembly/` — MoClo backbone

The `assembly/` directory contains the pOpen MoClo backbone vector:
- `pOpen-pOpenv3-MCL0.gb` — MCL0 destination backbone for MoClo Level 0 assembly

> **TODO:** Describe the assembly level and overhang scheme used by pOpenv3-MCL0.

---

### `reporters/` — Protein reporters

The `reporters/` directory contains fluorescent protein and chromoprotein reporter constructs in multiple configurations (PURE-optimized, TXTL-optimized, and chimeric). Includes cjBlue, eforRed, plamGFP, amajLime, gfasPurple, meleRFP, and mmilCFP. Several reporters include a lacO operator insert for regulated expression, and some include a C-terminal His6 tag.

> **TODO:** Add notes on which reporter configurations are recommended for PURE vs. TXTL reactions. Describe the `-lacO` and `-lacO-His6` variants and when to use them.

---

### `terminators/` — T7 terminator variants

The `terminators/` directory contains three T7 terminator variants:
- `pOpen-tT7.gb` — native T7 terminator
- `pOpen-tT7hyb6.gb` — hybrid T7 terminator variant 6
- `pOpen-tT7hyb10.gb` — hybrid T7 terminator variant 10

> **TODO:** Describe the differences between the native and hybrid terminator variants and when to choose each.

---

### `PURE/cloning/` — PURE protein cloning vectors

The `PURE/cloning/` directory contains pOpen entry vectors encoding each protein component of the PURE cell-free transcription/translation system. Proteins include all 20 aminoacyl-tRNA synthetases (AlaRS, ArgRS, AsnRS, etc.), translation initiation factors (IF1, IF2, IF3), elongation factors (EF-G, EF-Ts, EF-Tu), release factors (RF1, RF2, RF3, RRF), energy regeneration enzymes (AK, CK, NDK), and auxiliary proteins (MTF, PPiase, T7RNAP).

> **TODO:** Describe the purpose of these cloning vectors — are they used to transfer inserts into expression backbones via MoClo? Note any dual-His tag variants (e.g., `pOpen-glyQS-DualHis.gb`, `pOpen-pheST-DualHis.gb`) and when to use them vs. the standard versions.

---

### `PURE/expression/` — PURE protein expression vectors

The `PURE/expression/` directory contains pET28a-based expression vectors for producing each PURE system protein in *E. coli*. These are the constructs used for large-scale protein production and purification to reconstitute the PURE system.

> **TODO:** Document the expression and purification workflow: expression strain, induction conditions (IPTG concentration, temperature, time), and purification strategy (His-tag affinity, etc.). Note any proteins with special expression considerations (e.g., `pET28a-pT5-IF2.gb` and `pET28a-pT5-T7RNAP.gb` use a pT5 promoter instead of pT7 — describe why).

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

> **TODO:** Document induction conditions for the LacI/TetR circuits (IPTG and aTc concentrations, working ranges in PURE and TXTL). Describe the BjaI/BjaR quorum sensing system: signal molecule identity, detection threshold, and recommended use cases.

---

## Relationship to Nucleus Distribution docs

Protocol pages in the [Nucleus Distribution documentation](https://docs.nucleus.engineering) reference specific constructs from this repository by filename. When a protocol calls for a specific plasmid (e.g., `pOpen-PURET7-3`), the corresponding `.gb` file can be found here.

> **TODO:** Link to the relevant Addgene collection or internal distribution source for obtaining physical plasmid stocks.

## Contributing

> **TODO:** Describe the process for adding a new part — naming conventions, required GenBank annotation fields, which folder it belongs in, and how to open a PR.
