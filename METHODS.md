# Methods

Supplement to the ASHG 2026 poster (board 1003W). Every number on the poster comes from the analysis described here.
Section numbers in brackets point to the poster.

## Participants

The analysis set is the 67-plate NULISAseq release of the U19 cohort and the HIHG OtherProjects collections (metadata
rebuilt 3 September 2026): 4,546 participants. We excluded 4 participants whose re-assayed plate could not be matched
to a donor at high or medium confidence (below), 10 on one plate with a whole-plate shift, 62 at one site whose samples
carry a hemolysis and degradation signature intrinsic to the specimens, 2 with missing sex, 4 with missing age, and 191
outside the four ancestry groups (77 non-Hispanic White, 95 Hispanic Black, 19 other). 4,273 remain: 616 Hispanic of
European descent (HI-WH), 998 Hispanic of mixed origin (HI-MU), 1,669 African American (AA) and 990 African participants
recruited at sites in Africa (AFR). Ancestry is self-identified in the US; the African group is defined by recruitment in
Africa, and every member was born there. Participants come from 22 recruitment sites and were born in 50 countries. Each
group comes from its own sites (HI-WH 3, HI-MU 6, AA 6, AFR 13 in Nigeria, Ghana, Cameroon, Ethiopia, Kenya, Tanzania,
Uganda and Mozambique), so site and group are largely aliased; five sites recruit more than one group.

Diagnosis is clinical and not amyloid-confirmed: 2,156 cognitively normal (NCI), 1,118 mild cognitive impairment (MCI),
813 Alzheimer's disease dementia (AD) and 186 other dementia. Other dementia stays in the ancestry test as a fourth
diagnostic level and is left out of every test that compares diagnoses. One blood draw per participant.

## Assay

Plasma proteins were measured on the NULISAseq CNS Disease Panel (Alamar Biosciences), 131 targets, reported as log2
Normalized Protein Quantification (NPQ). Every plate passed the HIHG QC pipeline. Per-well total sequencing reads come
from the instrument's sample QC file and enter every model as log2(reads). Five targets read red-cell lysis rather than
plasma (HBA1, PGK1, MDH1, SOD1, ENO2); three of them are also in the module that builds the blood-cell score below. They
are fitted but left out of every FDR denominator, so counts are out of 126 proteins.

## Plates, runs and reagent lots

A run holds up to three physically separate plates (bays). Participants were assayed on two reagent lots: lot 1 (2025,
2,467 participants) and lot 2 (2026, 1,806). Three plates are handled separately. Plate 20251124-1407_Bay1 was loaded
with scrambled sample identities and its re-run, 20260706-1414_Bay1, carries a panel-wide specimen defect; each
1414_Bay1 participant takes the measurement from the 1407_Bay1 well that the cell-composition module assigned to them
at high or medium confidence (67 participants, who count in lot 1), and the 4 assigned only at low confidence are
dropped. Plate 20260813-1408_Bay2 carries a whole-plate shift and is excluded.

**The run anchor.** The pooled-plasma control (HIHG) read high on the six plates of runs 20251125-1332 and
20251124-1407 (a November 2025 bay drift: by bay, +0.02, +0.16 and +0.40 log2 on run 1332). Study wells carry about
half of the control's drift, measured three ways (0.52 from the lot contrast, 0.45 from sites re-recruited in lot 2,
0.43 from the Peru site on run 1407 against a later run). So before fitting, every well on those six plates (451 wells)
has half of its plate's per-target HIHG offset subtracted. This matters for the African group: every lot-1 African
participant was assayed on run 1332.

**Class-1 markers.** 14 targets shift between lots by more than 0.40 log2, with a bootstrap interval excluding zero,
in the 24 technical replicates assayed on both lots (the same specimen on each side, so a reagent effect can be seen on
its own). Nine are firm (PTN, pTau-217, BD-pTau-217, RUVBL2, IL2, CALB2, Aβ38, PDLIM5, PRDX6) and five provisional
(ENO2, ARSA, CD40LG, SOD1, CNTN2); 12 of the 14 are among the 126. They are never compared or pooled across lots.

## The model

Each protein was fitted as

    protein ~ ancestry + sex + age + diagnosis + log2(reads) + blood-cell score + (1 | site) + (1 | run / bay)

- Site is random, not fixed: site is nested in ancestry, so a fixed site term would leave the ancestry contrast
  unidentified. With site random, the ancestry coefficient is estimated mostly through the sites that recruit more than
  one group, and it can be over-shrunk. A one-site population difference is a site difference until shown otherwise.
- The plate is nested in the run: 17 of 30 runs hold three plates and every plate problem in this release is specific
  to one plate.
- log2(reads) is in every model: read depth is largely a site property and its effect differs by protein.
- The blood-cell score (PC1_cell_h) is the first principal component of a platelet, red-cell and leukocyte module from
  the QC pipeline, a covariate for cell content that survives centrifugation.
- Cystatin C is not in the model: it rises with clinical AD, so conditioning on it removes disease signal. It is a
  sensitivity arm.

**Lots are fitted separately.** Every model is fitted within reagent lot. A lot enters a test only if it holds at least
40 participants, 3 sites and 3 runs for that test. Tests are likelihood-ratio tests on maximum-likelihood fits, and the
χ² from the two lots are summed with their degrees of freedom; the sum tests "no effect in either lot" and needs no
assumption that the lots agree. Estimates are REML coefficients, pooled across lots by inverse-variance weighting when
the lots agree (between-lot I² below 50% and Cochran's Q p above 0.05) and otherwise reported from lot 1, as they
always are for class-1 markers. The gate is anti-conservative: under the global null the gated test rejects at 0.073
for a nominal 0.05, so FDR counts are optimistic by about 1.5-fold and are best read as comparisons between analyses.
HI-WH comes from three sites per lot, so counts that lean on the HI-WH reference are anti-conservative beyond the gate
as well. A parametric bootstrap of test 1 that redraws the site and run effects under the null (999 draws per marker and
lot) gives 62 of 126 at FDR < 0.05 in place of 68; the null χ² runs about 10% above its degrees of freedom, and the six
that drop out are at the margin: ACHE, HTT, ICAM1, SAA1, NPTX1 and FOLR1, bootstrap p 0.031 to 0.045 (all 126, with both
p-values, in tables/site_inference.csv). The poster reports the bootstrap count.

**Tests.** FDR is Benjamini-Hochberg over the 126 proteins, separately for each test, at 0.05.
1. Ancestry, all diagnoses: ancestry + diagnosis + covariates against diagnosis + covariates, all 4,273 participants
   (3 df per lot): 68 of 126 by the χ² reference, 62 by the parametric bootstrap above; the poster reports 62.
2. Ancestry at NCI: the same test within cognitively normal participants, without the diagnosis term.
3. Pairwise contrasts at NCI: HI-MU, AA and AFR each against HI-WH, a Wald test on the gated estimate. The poster's
   49 (AFR), 38 (AA) and 3 (HI-MU) [section 1].
4. Ancestry × diagnosis: ancestry × diagnosis + covariates against ancestry + diagnosis + covariates, in NCI, MCI and
   AD (4,087 participants; 6 df per lot). The poster's 12 [section 2].
5. AD effect within group: AD minus NCI in each group, from the REML fit of model 4, gated across lots [supplement,
   fig4b_ad_effect_by_group].
6. Level by diagnosis stage: NCI, MCI and AD in each group relative to HI-WH NCI, from the REML fit of model 4, each
   lot alone [Fig 4b]. It is cross-sectional: different people at each stage, not one person followed over time.

## APOE ε4

APOE ε4 dose (0, 1 or 2 copies) is available for 4,157 participants (97.3%). Two uses. (a) Adjustment: test 1 was
run with and without one ε4-dose slope on the same participants, and the percent change in the ancestry χ² is
reported (the APOE4 assay itself, which reads the ε4 isoform, is the positive control). (b) ε4 × ancestry: for
pTau-217, BD-pTau-217, BD-pTau-181 and NEFL, ancestry × ε4 dose + diagnosis + covariates within each lot (NCI, MCI and
AD), the interaction tested by likelihood ratio (3 df), and the ε4 slope estimated within each group; the same fit in
cognitively normal participants alone, which is the poster's counter-example card (pTau-217 p 0.75 in lot 1, 0.55 in
lot 2).

## Genotype: does the cohort's own variation predict the African vs HI-WH difference? [section 1]

Whole-genome sequence calls at 74 targeted autosomal variants (cis-pQTLs for panel proteins, APOE, and known
coding variants) were available for 2,278 of the 4,273 participants (HI-WH 341, HI-MU 632, AA 1,123, AFR 182). Every
sequenced African participant is in lot 2 and 330 of the 341 sequenced HI-WH are in lot 1, so dose cannot be fitted
inside a lot for that contrast. Per protein, the per-allele effect of each variant is estimated in the cohort (the model
above plus dose, within lot, gated across lots), the allele frequencies come from the cohort's own African and HI-WH
participants, and

    predicted difference = Σ over the protein's variants of 2 b_j (p_AFR,j − p_HIWH,j)   (log2)

sits beside the observed African minus HI-WH difference at NCI (test 3). The share is predicted over observed. A
screen of every called variant against every protein (model residuals, within lot; 61 variants × 131 targets,
Bonferroni) adds pairs not named in advance (Duffy-null rs2814778 against CCL2, CCL26 and CCL17 among them). The
poster's three panels are the proteins among the 49 whose confirmed variant predicts between 0 and 100% of the
difference and whose lots agree (between-lot I² below 50%): CHIT1 (78%), IL6R (45%), TIMP3 (15%). The before / after
contrast in the figure caption is one fit over the sequenced cognitively normal participants with and without the dose
term, both lots in one model with a lot term; it crosses lots, which is why the whole-cohort share is the headline
number.

## Regional contrasts within a group [section 3]

Two contrasts designed so that region is not the same thing as recruitment site. Peruvian and Ecuadorian versus
Caribbean HI-MU inside one New York site (CU: 53 born in Peru, Ecuador or Bolivia (25, 27, 1), 379 Caribbean; region +
diagnosis + covariates + (1 | run / bay)), because 197 of the 260 HI-MU participants born in Peru, Ecuador, Bolivia or
Chile come from the Peru site, which no Caribbean participant attends. The poster also gives the contrast over all sites (848 HI-MU: 260 vs 588;
site random): 22 of 126 at FDR < 0.05, 8 of the one-site 10 among them (SAA1 and CST3 differ only inside the site).
The 14 others are all higher in Peruvian and Ecuadorian participants, as an offset at the Peru site would be, so over
all sites region and the Peru site cannot be separated. East versus West Africa within the
African group, region being the recruiting site's country (West: Nigeria, Ghana, Cameroon; East: Ethiopia, Kenya,
Tanzania, Uganda, Mozambique), with region fixed and site random, so the contrast is tested against site-to-site
variation. Both fitted within lot and combined as above. Fig 5 shows both Peruvian and Ecuadorian estimates for the 24 proteins
that differ in either design, and names the 15 that hold with site separated in bold, coloured by a functional category
(immune, vascular, neuronal / synaptic, amyloid / proteolysis, epithelial / transport).

## Cut-points [section 2]

For BD-pTau-217, pTau-217, BD-pTau-181, NEFL and Aβ42 one cut-point was applied to every group: the 90th percentile
of HI-WH cognitively normal participants (the 10th for Aβ42, which falls in AD), set within each lot on raw NPQ with
no covariate adjustment, because a class-1 marker has no validated bridge between lots. In each group we report the
percent of cognitively normal participants beyond the cut (10% in HI-WH by construction), the percent of clinical AD
participants beyond it, and the AUC for AD against NCI (Mann-Whitney); MCI is not included. The same percentages by
site are in the tables.

## Aβ42

In lot 2, seven Aβ42 values below the lot median minus 4 MAD (7.9 log2 NPQ), all from African participants at four
sites on seven different plates, are set to missing (Aβ42 only; the rest of the row stays). Lot 1 has none below its
own cut.

## What each model term moves

The term table (tables/term_contributions.csv) drops one term at a time from the model and records the counts and the
median shift of the 49 African differences: site moves them most (median 0.06 log2; without it the African count is 68
and the HI-MU count 36), then the run anchor (0.03), the blood-cell score (0.03), reads (0.03), run / bay (0.02), sex
(0.02) and age (0.01).

## Sensitivity arms

The six-arm matrix (figures/fig4a_interaction_arms.png) shows the ancestry × diagnosis interactions under: the main
model; no anchor and no cell score; the re-assayed plate kept as run (no remap); run 1332 dropped (which removes
every lot-1 African participant); cystatin C added; and lot 2 alone. Five interactions survive every arm they can be
tested in (ACHE, BD-pTau-217, CXCL1, IL18, IL1B). BD-pTau-217's interaction holds in lot 2 alone (p 0.002);
pTau-217's does not (p 0.10).

## Software

R 4.6.1, lme4 2.0.6 (bobyqa optimizer), ggplot2 4.0.3. The analysis plan is the U19 67-plate plan with its
9 October 2026 amendment. The code is in a private repository; it is available on request (emartin1@miami.edu).
