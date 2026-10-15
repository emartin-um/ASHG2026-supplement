# African and Indigenous American ancestry shape plasma CNS biomarker baselines within and across populations, modifying Alzheimer's disease trajectories

**ASHG 2026 · Montréal · poster board 1003W, Wednesday 21 October 2026, 2:30 to 4:30 PM**. Contributing studies and consortia: **DAWN**, **PeADI**, **PRADI** and the **African Dementia Consortium (AfDC)**.

Eden R. Martin, Tianjie Gu, Olabode Omotoso, Lissette Gomez, Maryanella Illanes-Manrique, Kazeem Sanjo Akinwande, Patrice Whitehead, Michael Cuccaro, Alfred Kongnyu Njamnshi, Njideka Okubadejo, Jean Ikanga, Damas Andrea, Michelle Nichols, Olusegun Baiyewu, Mayowa Owolabi, Rajesh Kalaria, Brian Kunkle, Jeffery Vance, Christiane Reitz, Giuseppe Tosto, William Bush, Jonathan Haines, Adesola Ogunniyi, Goldie Byrd, Farid Rajabli, Rufus Akinyemi, Mario Cornejo-Olivas, Margaret A. Pericak-Vance, Anthony Griswold.

*John P. Hussman Institute for Human Genomics, University of Miami, and partner institutions in the US, Peru and Africa.*

---

This is the supplement behind the poster's QR code.

## The poster
- `poster/ASHG2026_Poster_Martin_36x72.pdf` and `poster/ASHG2026_Poster_Martin_36x72.pptx` (36 x 72 in; the file is built at 24 x 48 in and prints at 150%).

## Methods
- `METHODS.md`: participants, the assay, plates and reagent lots, the model and why each term is in it, the tests, APOE ε4, the genotype prediction, the regional contrasts, the cut-points, the sensitivity arms.

## Figures (`figures/`)
- `figS1_cohort_5panel.png`: the cohort in five panels, diagnosis, birthplace, sex, age and recruitment place by group.
- `fig2a_afr_caterpillar.png`: the 49 proteins that differ between African and HI-WH cognitively normal participants, a bar for the main-model estimate and a dot for each lot.
- `fig_pqtl_dose_freq.png`: CHIT1, IL6R and TIMP3 by allele dose within group, and each group's difference against its allele frequency.
- `fig3a_e4_by_group.png` and `fig3a_e4_by_group_nci.png`: the ε4 slope on p-tau and NEFL by group and lot, all diagnoses and cognitively normal only (the poster carries this as text).
- `fig4a_interaction_arms.png`: the ancestry × diagnosis interactions under six model arms.
- `fig4b_stage_by_group.png`: pTau-217, BD-pTau-217, NEFL and GFAP at NCI, MCI and AD in each group, relative to HI-WH cognitively normal, each lot alone (the poster's section 2 figure).
- `fig4b_ad_effect_by_group.png`: AD minus cognitively normal within each group, both lots, eight markers, Aβ42, TREM2, pSNCA-129 and SNCA among them (on the poster until 2026-10-15).
- `fig5_regional.png`: Peruvian and Ecuadorian vs Caribbean over all sites and inside one New York site; East vs West Africa with site in the model.
- `fig5_regional_onesite_by_lot.png`: the proteins that differ with site separated (10 inside one New York site, 5 East vs West Africa), each lot alone, coloured by function.
- `fig6_cutpoint_by_group.png`: one cut-point per lot applied to every group, five markers.

## Tables (`tables/`)
- `per_marker_results.csv`: the main model, every target: the ancestry omnibus, the NCI omnibus, the three contrasts vs HI-WH with their lot basis and between-lot I², the ancestry × diagnosis test, the APOE adjustment.
- `term_contributions.csv` and `term_contributions_numbers.txt`: what each model term moves.
- `afr_nci_by_lot.csv`: the African vs HI-WH difference at NCI in each lot, every target.
- `ad_effect_by_group.csv`, `interaction_2026lot.csv`: the AD effect within group and the lot-2 replication of the interactions.
- `cutpoint_by_group_lot.csv`, `bdptau217_cut_by_site_lot.csv`: the cut-point results by group and by site.
- `e4_slope_by_group_lot.csv`, `e4_slope_by_group_lot_nci.csv`: the ε4 slopes.
- `regional_results.csv`: the regional contrasts, every design.
- `site_inference.csv`: the ancestry omnibus per protein with its χ² p and its site-level bootstrap p.
- `aa_gradient.csv`: the AA vs HI-WH difference against the African vs HI-WH difference, per protein.
- `wgs_pqtl_pairs.csv`, `wgs_pqtl_per_protein.csv`, `wgs_pqtl_screen.csv`, `wgs_pqtl_numbers.txt`: the full genotype table, per variant, per protein, and the screen.

No individual-level data are here. Proteins are named by HGNC symbol.

Questions: emartin1@miami.edu
