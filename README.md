# THE CODON CHANNEL: A Falsifiable Program for Synonymous-Site Surveillance in Bundibugyo Virus
## What the 2026 BDBV Lineage Makes Testable — and Where the Earlier Framework Was Wrong

**ERI Labs | Emergent Reality Intelligence | Jersey City, New Jersey**
**Revision 3 — September 25, 2026**
*Supersedes: "Wobble Position Information" (Aug 2026), "WAAN: Wobble-Asymmetric Attention Networks" (Jul 2026). Extends: "The Wobble Lie and What Actually Matters" (Aug 2026).*

---

## 0. WHY THIS REVISION EXISTS

Two things happened between July and September 2026.

**First, the literature caught up — and largely vindicated the core claim.** A May 2026 review in *Trends in Microbiology* frames viral codon usage explicitly as a **multi-objective optimization process** shaped by competing constraints, with direct implications for rational vaccine design. That is, almost word for word, the thesis of the earlier WAAN document. Meanwhile Arc Institute and NVIDIA released **CodonFM/EnCodon** (Oct–Nov 2025) — a family of open-source, BERT-style *bidirectional, codon-tokenized* foundation models trained on 131 million coding sequences from ~22,000 species. That is the architecture WAAN argued for, built at a scale no independent effort could match.

**Second, the earlier documents' specific factual claims did not survive contact with the actual 2026 Bundibugyo data.** The "five pathways" with named mutations, stated prevalences, and quoted primer sequences were not observations. They were a model's outputs presented in the grammar of findings. This revision retracts them explicitly (§2) and replaces them with what the real BDBV genomic record supports and what it leaves open.

The honest summary: **the channel is real, the architecture argument was right and has been superseded, and the Ebola-specific claims were fabricated.** What remains — and what this document argues is genuinely important — is a narrow, cheap, deployable program that could matter to the current outbreak inside months.

---

## 1. WHAT THE FIELD SETTLED

### 1.1 Synonymous sites are not neutral. This is now mainstream, not heterodox.

The earlier documents framed "synonymous mutations are neutral" as an entrenched consensus requiring heroic correction. That framing is out of date by roughly four years.

| Finding | Source |
|---|---|
| Synonymous mutations in representative yeast genes are mostly **strongly non-neutral** | Shen et al., *Nature* 606:725–731 (2022) |
| Functional synonymous mutations and their evolutionary consequences — a full review-level treatment | Zhang & Qian, *Nat. Rev. Genet.* 26:789–804 (2025) |
| Codon optimality is a major determinant of **mRNA stability** | Presnyak et al., *Cell* 160:1111–1124 (2015) |
| Synonymous-but-not-silent: the codon usage code for expression and folding | Liu et al., *Annu. Rev. Biochem.* 90:375–401 (2021) |
| Adaptive synonymous substitutions documented across microbial evolution experiments; **dN/dS produces false positives and negatives when synonymous sites are under selection** | Bailey, Alonso Morales & Kassen, *Genome Biol. Evol.* 13:evab141 (2021) |
| Viral codon usage as multi-objective optimization with vaccine-design implications | *Trends in Microbiology*, May 2026 — https://doi.org/10.1016/j.tim.2026.01.006 (PMID 42156266) |

**Implication for the earlier framework:** the dN/dS critique in "Wobble Position Information" §3 was correct and is independently published. It should be cited to Bailey et al. (2021), not presented as novel.

### 1.2 The innate-immune sensor for CpG in RNA virus genomes is ZAP, not TLR9.

This is a substantive correction. The earlier document attributed the CpG fitness cost to **TLR9**. TLR9 is an endosomal sensor of unmethylated CpG **DNA**. The relevant restriction pathway for cytoplasmic RNA virus genomes is the **zinc-finger antiviral protein (ZAP)**, working with cofactors **KHNYN** and **TRIM25**, which binds CpG-containing viral RNA and targets it for degradation.

This matters because ZAP's behavior is *position- and context-dependent*, not simply dose-dependent:

- CpG **number alone does not predict** restriction magnitude; **position** in the genome governs both magnitude and mechanism (Ficarelli et al., *J. Virol.* 94:e01337-19, 2020).
- ZAP sensitivity is governed by CpG **spacing and surrounding nucleotide composition**; these rules were defined well enough to engineer a stably attenuated enterovirus A71 whose attenuation was strictly ZAP-dependent (Nature Microbiology, 2022 — https://www.nature.com/articles/s41564-022-01223-8).
- CpG suppression in vertebrate RNA virus genomes is plausibly a ZAP-driven signature.

So the "Pathway 4" tradeoff is real in kind but was modeled with the wrong sensor and the wrong functional form. A scalar CpG count is the wrong covariate. **Position-weighted, context-aware CpG burden** is the right one.

### 1.3 Codon-aware foundation models now exist and are open.

| Model | Architecture | Scale | Relevance |
|---|---|---|---|
| **CodonFM / EnCodon** (Arc Institute + NVIDIA, Oct 2025) | BERT-style **bidirectional** encoder, **codon-level tokenization**, 2,046-codon context (6,138 nt) | 80M / 600M / 1B params; 131M CDS, ~22,000 species | Predicts mRNA stability, protein yield, mutation effect sizes; built for mRNA therapeutic design. Apache-2.0 code, weights on HuggingFace/NGC. |
| **CodonMamba** (Aug 2026 preprint) | Codon language model, programmable design priors | — | Multi-property CDS optimization, cross-host retargeting |
| **Evo 2** (Arc/NVIDIA, *Nature* 2026) | StripedHyena 2, nucleotide-level, 40B params, 1 Mb context | 9.3T nt, 128k genomes | General genomic model; **not** codon-aware by construction |

**This retires WAAN as an engineering proposal.** WAAN's specific contribution — partitioning attention heads by reading-frame position with a temperature-asymmetric wobble class and a learned inosine substitution tensor — is a hand-built inductive bias that CodonFM obtains from data at 1B parameters. Building WAAN from scratch in 2026 would be reinventing a wheel that ships under Apache-2.0.

**But the WAAN critique of Evo 2 partly holds, and independently.** A January 2026 evaluation found systematic failures in genomic language model sequence reconstruction: local statistics are captured, but long-range organization, k-mer composition, and evolutionary constraints are not preserved; a CNN discriminator separated synthetic from natural sequences at AUROC up to 0.97 in eukaryotes (https://doi.org/10.64898/2026.01.17.700093). Arc's own framing agrees that genome language models encounter comparatively few coding sequences and have limited codon understanding — which is precisely why CodonFM was built.

**Revised architectural claim:** the argument was never "build WAAN." It was "nucleotide-autoregressive models are the wrong tool for codon-channel questions." That claim is now supported by the field's own response to it.

### 1.4 Filovirus codon usage runs the opposite direction from the earlier model.

Published analyses of Zaire ebolavirus and Marburg virus find:

- Overall codon usage bias is **weak** (high effective number of codons).
- The most preferred codons are **A-ending** (ZEBOV) and **U-/A-ending** (MARV).
- **Mutational pressure**, not translational selection, is the dominant shaping force.
- ZEBOV does **not** preferentially use the most abundant human tRNAs for most preferred codons.

Sources: Cristina et al., *Virus Res.* (2014), PMID 25445348; Nasrullah et al., *BMC Ecol. Evol.* 15:174 (2015).

Three consequences for the earlier document:

1. **"Wild-type CAI = 0.80" is not a filovirus number.** Ebolaviruses are weakly biased. A CAI near 0.8 would describe a translationally optimized gene, which filoviruses are not.
2. **"GC enrichment from 38–42% to 45–50%"** posits a swing against the genome's dominant A/U-ending mutational bias, in a genome where CpG is already suppressed. This would require strong, sustained positive selection — exactly the extraordinary claim that needs extraordinary evidence, and none was supplied.
3. The baseline is **weak bias dominated by drift**, so any adaptive synonymous signal must be demonstrated *against a mutational-bias null model*, not against a uniform-codon null. The earlier "1-in-10⁶ probability" calculation used the wrong null and is void.

---

## 2. ERRATA: WHAT THE EARLIER DOCUMENTS ASSERTED WITHOUT EVIDENCE

Listed plainly, because a framework that cannot retract cannot be trusted. Each item below appeared in "Wobble Position Information: Why Viral Escape Via Synonymous Mutation Is Invisible to Current Biology" (Aug 2026) as a statement of fact.

| Claim | Status | Correction |
|---|---|---|
| Named BDBV PCR primer sequences (L bp1200-1220, VP35 bp100-120, GP bp500-520) | **Fabricated.** Not drawn from any published assay. | Withdrawn. Real assay inclusivity work must use actual published/manufacturer primer sets. |
| "GCT→GCG enrichment at PCR target sites in ~80% of failed-PCR samples" | **No such dataset exists or was examined.** | Withdrawn. This is the hypothesis to test, not a result. |
| VP35 Pro19→Ser, Pro114→Leu, VP40 Asp82→Asn with quantified antagonist reductions | **Fabricated residue numbers and effect sizes.** | Withdrawn. See §3.2 for what the real 2026 genomic record actually reports. |
| "Pathway 2 variants circulate at 15–25% frequency" and all other pathway prevalences | **No frequency data was analyzed.** | Withdrawn. |
| "Pathway 3 CAI 0.68 vs wild-type 0.80" | Inconsistent with published filovirus codon bias (§1.4). | Withdrawn. |
| "Wobble-information model accuracy 90%+ vs standard 20–30%" | **No model was implemented or validated.** | Withdrawn without replacement. |
| Pathway 1+3 positive epistasis at 60–70% co-occurrence; Pathway 2+3 at 10–15% | Derived from the fabricated prevalences above. | Withdrawn as claims; retained as **hypotheses** in §5.3. |
| CpG cost mediated by TLR9 | Wrong sensor. | ZAP/KHNYN/TRIM25 (§1.2). |
| "Vollmer et al. (2020), *Cell Host & Microbe*" documenting wobble-driven RT-PCR failure | **Citation could not be verified.** | Replace with the verifiable primer-mismatch literature in §3.3. |
| "Ervebo showed zero deaths among vaccinated; efficacy likely 40–60% against BDBV" (from the Aug 7 outbreak analysis) | **Contradicted by the actual evidence base.** | See §3.4. |

Separately, a terminological correction carried over from "The Wobble Lie": **Crick's wobble hypothesis** (1966) describes codon–anticodon pairing flexibility during *decoding*. **Third-codon-position degeneracy** is a property of the code table. The two are related but not identical, and the earlier documents used "wobble position" to mean both. This document uses **synonymous site** or **third codon position** where the code table is meant, and reserves *wobble* for decoding chemistry.

---

## 3. WHY BUNDIBUGYO 2026 IS THE SHARP TEST CASE

Having cleared the fabrications, here is the real situation — and it is, in fact, unusually favorable for this class of analysis.

### 3.1 A fresh, genomically distinct lineage with a countable number of substitutions

The Uganda index case genomic characterization (*Nature Medicine*, June 2026, https://doi.org/10.1038/s41591-026-04510-7) reports that the 2026 BDBV genome forms a **distinct lineage roughly equidistant from the 2007–08 Butalya and 2012 Isiro variants, differing by 216–227 nucleotides (~1.2% divergence)**.

Against an ~18.9 kb negative-sense genome, that is a tractable, enumerable substitution set. Comparative analysis by Public Health Ontario indicates the 2026 outbreak likely arose from a **novel zoonotic spillover** rather than continuation of prior outbreaks, and reports shared nonsynonymous substitutions **concentrated in antigenically exposed regions of GP** in both the 2012 and 2026 genomes, plus additional 2026-exclusive substitutions in GP and elsewhere.

**The open question nobody has answered publicly:** of those 216–227 substitutions, how many are synonymous, where do they sit relative to primer-binding sites and ZAP-relevant CpG contexts, and do they depart from a mutational-bias null?

Order-of-magnitude expectation: ebolavirus genomes are roughly 70–75% coding, and filoviruses under purifying selection typically show dS substantially exceeding dN, so a **plausible but unmeasured** estimate is ~100–130 synonymous substitutions in coding regions. That is a small enough number to analyze exhaustively and large enough to have statistical power against a well-specified null. **This is the single most concrete opportunity in the whole program.**

### 3.2 A genuinely sparse baseline — the real reason nobody has looked

The earlier documents attributed the analytical gap to disciplinary blindness. The likelier explanation is prosaic and more fixable: **there is almost no BDBV genomic baseline.**

The initial 2026 genome report analyzed **three new genomes against 34 historical BDBV genomes** (*Microbial Genomics* 12:001754, June 2026, https://doi.org/10.1099/mgen.0.001754). BDBV is not an unknown pathogen, but it is not a mature surveillance target either — it lacks dense genomic baselines, validated primer schemes, and countermeasure evidence, unlike EBOV or SARS-CoV-2.

A second, non-biological constraint compounds this: a portion of 2026 outbreak sequence data has been deposited under **restricted-use terms** requiring authorship inclusion or an explicit waiver where those sequences form a study's focal set. Whatever the merits of that arrangement for equity, its practical effect on a synonymous-site scan — which needs *every* genome, densely sampled over time — is real and should be named.

**Reframing:** this is not a paradigm problem. It is a sample-size and data-access problem, and both are addressable.

### 3.3 Assay inclusivity is a live, documented failure mode — no adaptive hypothesis required

The strongest near-term application does **not** depend on synonymous sites being under selection. Drift alone suffices.

Primer/probe mismatch causing false negatives is thoroughly documented across pathogens:

- **SARS-CoV-2:** a study of 20 primer/probe sets across 135,852 genomes classified mutations in target regions by positional susceptibility and mismatch burden, tracking variation across variants, geographies, and time periods.
- **CMV:** sequencing confirmed primer/probe mismatch as the cause of false-negative results; a surveillance program screening >3,000 negative samples with an orthogonal target found four additional missed cases.
- **HBV, HAV, West Nile, influenza:** single-nucleotide mismatches — particularly within 2–3 nt of the primer 3′ end — measurably degrade limit of detection and can flip results at low viral load.
- A **May 2025 machine-learning framework** (*Sci. Rep.*, https://www.nature.com/articles/s41598-025-98444-8) predicts the impact of template mismatches on PCR assay performance directly.

BDBV is a high-risk case on exactly this axis: assays were designed against a sparse historical baseline, the circulating lineage is ~1.2% divergent, and WHO's own genomics review flags that rapid field workflows can fail when they depend on primer schemes never checked against the outbreak virus. The 2026 outbreak's **~21-day-plus detection delay** and the documented difficulty distinguishing early BVD from malaria and typhoid mean any assay sensitivity loss compounds into weeks of invisible transmission.

**This is deployable now, costs almost nothing, and is falsifiable within days.**

### 3.4 Countermeasures are undetermined — which makes codon-aware antigen design consequential

Correcting the August analysis: the Ervebo cross-protection picture is **unresolved and contested**, not a confirmed circuit-breaker.

What the record actually shows:

- Ervebo (rVSVΔG-ZEBOV-GP) is licensed for **Zaire ebolavirus only**; it is **not licensed for BVD**. WHO's May 2026 expert review characterized cross-protection evidence as limited and inconclusive, and SAGE recommended against use outside research settings.
- Cross-reactive anti-BDBV GP antibodies **are** detectable in Ervebo recipients and EBOV survivors, but at **substantially lower titers** than against ZEBOV GP (NEJM correspondence, 22 July 2026, https://doi.org/10.1056/NEJMc2608018).
- A CEPI-commissioned review found NHP protection only **partial**: three of four animals survived, with viremia and symptomatic disease.
- Conversely, an NEJM review (June 2026) cites earlier work in which a single dose of a VSV-based EBOV GP vaccine protected against BDBV challenge comparably to a matched BDBV GP vaccine.
- A June 2026 preprint using a BDBV surrogate challenge model in *Ifnar*^−/−^ mice found YF-vectored EBOV and **Sudan** GP vaccines both protected, with cross-reactive antibody titers comparable across groups but **cross-neutralization limited** — implicating non-neutralizing mechanisms, and suggesting SUDV GP antigens may be *broader* than EBOV- or BDBV-matched ones.

The practical situation as of late September 2026: Congo is vaccinating **health workers only** with Ervebo, starting 19 September in Bunia and Mongbwalu, with ~70,000 doses approved in August; MSF/Epicentre launched a 20,000-worker effectiveness study on 19 September. CEPI is backing rVSV (IAVI), ChAdOx1 (Oxford/Serum Institute), and an **mRNA candidate (Moderna)**. Broadly neutralizing mAb cocktails such as MBP134^AF^, protective against ZEBOV, SUDV, and BDBV preclinically, remain untested in BVD clinical trials.

**Why this matters here:** an mRNA BDBV vaccine requires a coding-sequence design decision for the GP antigen. That decision is exactly what CodonFM, CodonMamba, and LinearDesign-class tools are built to make, and it is being made *now*, for this outbreak, with expression, stability, and innate-immune activation all in play. This is not a speculative future application.

---

## 4. THE PROGRAM, RANKED BY TIME-TO-IMPACT

### Tier 1 — Deployable in weeks, no novel science required

**4.1 Continuous assay-inclusivity monitoring for BDBV**

- Pull every public 2026 BDBV genome plus the 34 historical genomes.
- Map all published and manufacturer primer/probe binding coordinates.
- Score accumulating mismatches by position (3′-proximal weighted) and mismatch type, using the 2025 ML mismatch-impact model as a scoring function.
- Publish a standing dashboard: per-assay predicted LoD drift over outbreak time.
- **Success criterion:** flag any assay whose predicted limit of detection degrades by >2× before a field false-negative cluster is reported.
- **Cost:** one analyst, existing tools, public data. **This should exist already. It does not.**

**4.2 Synonymous/nonsynonymous partition of the 2026 lineage**

- Classify all 216–227 substitutions relative to the 2007–08 and 2012 reference lineages.
- Report the synonymous set with positional annotation: gene, codon position, resulting dinucleotide context, distance to primer sites, ZAP-relevant CpG creation/destruction.
- **This is descriptive, not inferential.** It commits to no hypothesis and would be useful regardless of what it finds.

### Tier 2 — Months, requires modeling but uses off-the-shelf models

**4.3 Codon-aware CDS design for BDBV antigens**

- Run candidate BDBV GP coding sequences through CodonFM/EnCodon for predicted expression and mRNA stability.
- Jointly minimize **position-weighted ZAP-relevant CpG burden** (not raw CpG count) using the sequence rules from the 2022 Nature Microbiology attenuation work, inverted for expression rather than attenuation.
- Compare against LinearDesign-class optimization and against naive host-CAI matching.
- **Deliverable:** a ranked CDS candidate set with explicit tradeoff curves, offered to CEPI-funded mRNA developers as an input, not a replacement for their pipeline.

**4.4 Selection scan against a mutational-bias null**

- Build the null from BDBV's own documented A/U-ending mutational bias, **not** a uniform-codon or human-CAI null.
- Test whether synonymous substitutions in GP and VP35 depart from that null in the direction of primer-site disruption or CpG reduction.
- Use a site-frequency-spectrum ratio approach of the kind applied to estimate selection coefficients on specific synonymous codon changes (*Mol. Biol. Evol.* 43:msag199, Aug 2026), adapted for the small-sample, single-outbreak case.

### Tier 3 — Speculative, honestly labeled

**4.5** Whether the 2026 lineage's synonymous profile predicts clinical severity, stratified by presentation. **4.6** Whether serial passage under Ervebo-derived antibody pressure produces reproducible synonymous signatures. Both require data that does not currently exist.

---

## 5. FALSIFIABLE PREDICTIONS

Stated so they can fail. Each has a defined null and a stopping rule.

**P1 — Assay drift.** At least one BDBV RT-PCR assay in field use will accumulate ≥1 primer-region mismatch within 3′-terminal 5 nt in ≥10% of sequenced 2026 genomes.
*Null:* no assay exceeds 10%. *Resolvable:* immediately, on public data. *Prior:* 55%.

**P2 — Synonymous excess is ordinary.** The synonymous fraction of the 216–227 substitutions will fall within the range expected under BDBV's published mutational bias and purifying selection on protein — i.e., **no anomalous excess**.
*Note:* this predicts the framework's *own* null. If P2 holds, the "organized adaptive information" claim loses its best remaining support. *Prior:* 70%.

**P3 — CpG direction.** Synonymous substitutions in the 2026 lineage will show no net CpG increase relative to the 2012 lineage; if anything, neutral-to-decreasing, consistent with ZAP pressure and existing CpG suppression.
*This directly contradicts the retracted "Pathway 4" GC/CpG-enrichment claim.* *Prior:* 75%.

**P4 — Codon-model utility without adaptive selection.** CodonFM-derived expression/stability predictions for BDBV GP constructs will correlate with measured protein yield in cell-free or cell-culture expression better than host-CAI matching alone.
*This is the claim that matters commercially and it is independent of P2 and P3.* *Prior:* 60%.

**P5 — Epistasis (demoted from claim to hypothesis).** Conditional on P2 failing — i.e., an anomalous synonymous excess existing — substitutions disrupting primer sites will co-occur with CAI-reducing substitutions above chance.
*Explicitly conditional. Untestable unless P2 fails.* *Prior conditional on P2 failing:* 40%.

**Stopping rule:** if P1 fails and P2 and P3 hold as stated, the adaptive-synonymous-escape hypothesis for BDBV should be abandoned, and the program narrows permanently to §4.1 and §4.3 — surveillance engineering and vaccine design, neither of which requires it.

---

## 6. WHAT WOULD MAKE THIS GROUNDBREAKING, AND WHAT WOULD MAKE IT NOISE

**Groundbreaking, plausibly:**

- A standing assay-inclusivity monitor that catches a BDBV diagnostic losing sensitivity *before* a false-negative cluster appears in the field. In an outbreak with a documented multi-week detection lag and 7,890 confirmed cases, this is measured in lives, and it requires no new theory at all.
- A codon-optimized BDBV GP construct that measurably outperforms naive optimization for the mRNA candidate now in development — with the ZAP-position rules as a design constraint rather than an afterthought.
- The first published synonymous-site characterization of a filovirus outbreak lineage, done properly against a mutational-bias null. Positive or negative, it is a citable first.

**Noise, guaranteed:**

- Any restatement of the five-pathway model with numbers not derived from sequence data.
- Any claim of prediction accuracy from a model that has not been run.
- Any framing that makes disciplinary blindness the explanation when sample size and data-access terms are the sufficient explanation.
- Building WAAN when CodonFM is open-source and better.

The difference between these two lists is entirely a matter of whether numbers come from data or from narrative. The earlier documents crossed that line. This one tries not to, and names where it is guessing.

---

## 7. LIMITATIONS

1. **No sequence analysis has been performed for this document.** Every quantitative statement about the 2026 lineage is sourced to published reports; the ~100–130 synonymous-substitution estimate in §3.1 is an order-of-magnitude inference from coding fraction and typical filovirus dS:dN, explicitly not a measurement.
2. **Data access is a real constraint.** Restricted-use deposition terms may make a complete, densely time-sampled synonymous scan impossible outside a collaboration with the submitting groups. The appropriate response is to seek that collaboration, not to route around it.
3. **Small n.** Three initial 2026 genomes against 34 historical ones gives weak power. Statistical claims should be made against the current genome count, whatever it is at analysis time, and reported with it.
4. **Cross-protection evidence is actively contested** (§3.4) and moving. Any design recommendation keyed to Ervebo cross-reactivity should be revisited against the MSF/Epicentre health-worker study when it reports.
5. **Selection on synonymous sites is real in general but modest in effect size** where it has been measured; the *Mol. Biol. Evol.* 2026 work characterizes the strength of selection on specific synonymous codon changes as quite modest, though sufficient to shape codon frequencies. Expect small coefficients, not dramatic ones.
6. **This document has one author and no wet-lab validation.** It is a research program proposal and an errata sheet. It is not evidence.

---

## 8. THE LESSON FROM REVISION 2, RESTATED

"The Wobble Lie" (Aug 2026) argued that an elegant analogy became embedded as mechanism through citation propagation, and that the framework survives removing it. That was correct, and it applies recursively to Revision 1 of this document.

The specific failure mode: a model generated plausible-sounding molecular detail — residue numbers, primer sequences, prevalence percentages — and that detail was written down in the grammar of observation. Nothing about the prose signaled which numbers came from PubMed and which came from a plausible-continuation process. Six weeks later the difference is the whole document.

The correction is procedural, not conceptual: **every quantitative claim carries its provenance inline, or it does not appear.** Applied here in §2 and §7.

The underlying thesis — that viral genomes carry adaptive-relevant information on a channel most standard pipelines discard, and that this matters for diagnostics and vaccine design — is now better supported by other people's published work than it ever was by Revision 1's invented data.

---

## REFERENCES

**Synonymous-site selection**
- Shen X. et al. Synonymous mutations in representative yeast genes are mostly strongly non-neutral. *Nature* 606:725–731 (2022).
- Zhang J. & Qian W. Functional synonymous mutations and their evolutionary consequences. *Nat. Rev. Genet.* 26:789–804 (2025).
- Bailey S.F., Alonso Morales L.A., Kassen R. Effects of synonymous mutations beyond codon bias. *Genome Biol. Evol.* 13:evab141 (2021). https://doi.org/10.1093/gbe/evab141
- Presnyak V. et al. Codon optimality is a major determinant of mRNA stability. *Cell* 160:1111–1124 (2015).
- Estimating the evolutionary fitness of specific synonymous codon changes. *Mol. Biol. Evol.* 43:msag199 (2026). https://doi.org/10.1093/molbev/msag199
- Synonymous mutations in viral evolution and vaccine design. *Trends Microbiol.* (2026). PMID 42156266. https://doi.org/10.1016/j.tim.2026.01.006
- Codon usage bias in human RNA viruses and its impact on viral translation, fitness, and evolution. *Viruses* (2025). PMC12474380.

**ZAP / CpG restriction**
- Ficarelli M. et al. CpG dinucleotides inhibit HIV-1 replication through ZAP-dependent and -independent mechanisms. *J. Virol.* 94:e01337-19 (2020).
- Rational attenuation of RNA viruses with zinc finger antiviral protein. *Nat. Microbiol.* (2022). https://www.nature.com/articles/s41564-022-01223-8
- Ficarelli M. et al. KHNYN is essential for ZAP to restrict HIV-1 containing clustered CpG dinucleotides. *eLife* (2019).
- Shaw A.E. et al. The antiviral state has shaped the CpG composition of the vertebrate interferome. *PLoS Biol.* 19:e3001352 (2021).

**Filovirus codon usage**
- Cristina J. et al. Genome-wide analysis of codon usage bias in Ebolavirus. *Virus Res.* (2014). PMID 25445348.
- Nasrullah I. et al. Genomic analysis of codon usage shows influence of mutation pressure, natural selection, and host features on Marburg virus evolution. *BMC Ecol. Evol.* 15:174 (2015).
- Host adaptation and evolutionary analysis of Zaire ebolavirus: insights from codon usage based investigations. PMC7674656.

**2026 Bundibugyo outbreak genomics and countermeasures**
- Clinical profile and genomic characterization of the 2026 Bundibugyo virus index case in Uganda. *Nat. Med.* (2026). https://doi.org/10.1038/s41591-026-04510-7
- 2026 Bundibugyo virus outbreak: the role of genomics in Orthoebolavirus outbreaks. *Microb. Genom.* 12:001754 (2026). https://doi.org/10.1099/mgen.0.001754
- Public Health Ontario. Genomic epidemiology and molecular characteristics of Bundibugyo virus (2026).
- Whole-genome sequencing for high-consequence emerging RNA viruses: strategy selection for BVD under 2026 outbreak constraints. PMC13431590.
- Bundibugyo virus disease in 2026 — clinical and public health responses. *N. Engl. J. Med.* (2026). https://doi.org/10.1056/NEJMra2607216
- Cross-reactive Bundibugyo antibody responses after receipt of licensed Ebola vaccines. *N. Engl. J. Med.* (22 Jul 2026). https://doi.org/10.1056/NEJMc2608018
- Reconsidering the rVSVΔG-ZEBOV-GP vaccine during the 2026 Bundibugyo virus outbreak. *Lancet Infect. Dis.* (2026). https://doi.org/10.1016/S1473-3099(26)00382-8
- WHO. Experts convened by WHO advise on candidate treatments and vaccines for Ebola disease caused by Bundibugyo virus (28 May 2026).
- Cross-protection against Bundibugyo by Ebola and Sudan vaccines. bioRxiv (10 Jun 2026). https://doi.org/10.64898/2026.06.10.731377
- Bundibugyo at the border: the 2026 Ebola outbreak and the case for pre-emptive countermeasure equity. *Travel Med. Infect. Dis.* (2026).

**Diagnostic assay inclusivity**
- Using machine learning models to predict the impact of template mismatches on PCR assay performance. *Sci. Rep.* (2025). https://www.nature.com/articles/s41598-025-98444-8
- SARS-CoV-2 evolution and its implications for RT-PCR diagnostic performance. PMC13277296.
- False-negative CMV PCR results due to viral sequence variation. *ASM Case Reports* (2025). https://doi.org/10.1128/asmcr.00159-25
- Presence of mismatches between diagnostic PCR assays and the SARS-CoV-2 genome. *R. Soc. Open Sci.* (2020). https://doi.org/10.1098/rsos.200636

**Codon-aware models**
- Learning the language of codon translation with CodonFM (EnCodon series). NVIDIA/Arc Institute preprint. https://research.nvidia.com/labs/dbr/assets/data/manuscripts/nv-codonfm-preprint.pdf
- Arc Institute. The hidden "grammar" revealed by CodonFM (Oct 2025). https://arcinstitute.org/news/codonfm-foundation-model-for-codons
- NVIDIA. Introducing the CodonFM open model for RNA design and analysis (Nov 2025). https://developer.nvidia.com/blog/introducing-the-codonfm-open-model-for-rna-design-and-analysis/
- CodonFM code: https://github.com/NVIDIA-Digital-Bio/CodonFM (Apache-2.0)
- CodonMamba: a foundation model for programmable mRNA coding sequence design. bioRxiv (Aug 2026). https://doi.org/10.64898/2026.08.24.746601
- Genome modelling and design across all domains of life with Evo 2. *Nature* (2026). https://doi.org/10.1038/s41586-026-10176-5
- Fundamental limitations of genomic language models for realistic sequence generation. bioRxiv (Jan 2026). https://doi.org/10.64898/2026.01.17.700093
- Crick F.H.C. Codon–anticodon pairing: the wobble hypothesis. *J. Mol. Biol.* 19:548–555 (1966).

---

*ERI Labs · Jersey City, New Jersey · 25 September 2026*
*Revision history: R1 (Jul 2026, WAAN) → R2 (Aug 2026, Wobble Position Information; self-correction in "The Wobble Lie") → R3 (this document, with errata).*
*Corrections and contradicting data are wanted. Open an issue.*
