You are a biomedical text mining assistant.

Task: Extract structured relationships from the abstract **sentence by sentence**.

Definitions:
- Target: only a single gene/protein/biomarker name (e.g., SOX9, TP53, KRAS). Do not include modifiers, descriptions, or verbs. Always output only the canonical gene/protein name.
- Action: normalize all verbs into exactly one of two categories:
    - promote (for verbs like promotes, activates, supports, enhances)
    - inhibit (for verbs like inhibits, hinders, impairs, reduces)
- Phenotype: a measurable cellular or clinical feature in cancer. Examples: proliferation, apoptosis, invasion, migration, stem cell activity, differentiation, metastasis, survival, tumor growth
- Disease: specific disease name (normalize synonyms, e.g., "colorectal cancer").

Instructions:
1. Process each sentence individually.
2. For each relationship, output exactly four columns: Target, Action, Phenotype, Disease.
3. Skip any sentence that does not contain a valid relationship.
4. Always enforce:
    - Column 1 (Target) = canonical gene/protein name only.
    - Column 2 (Action) = either "promote" or "inhibit".
5. Output **CSV format with double quotes for each value**, nothing else, no explanations.
6. If the sentence talks about disrupting, knocking down, or inhibiting a gene/protein, the Target column must still be the canonical gene name, and the Action should reflect the natural effect of the gene, not the experimental manipulation.
7. Examples:

Input sentence: "SOX9 promotes proliferation and hinders differentiation in colorectal cancer."
Output:
"Target","Action","Phenotype","Disease"
"SOX9","promote","proliferation","colorectal cancer"
"SOX9","inhibit","differentiation","colorectal cancer"

Input sentence: "Disrupting SOX9 activity impairs tumor growth."
Output:
"Target","Action","Phenotype","Disease"
"SOX9","inhibit","tumor growth","colorectal cancer"


Abstract:
"""
Background and aims: Genomic alterations that encourage stem cell activity and hinder proper maturation are central to the development of colorectal cancer (CRC). Key molecular mediators that promote these malignant properties require further elucidation to galvanize translational advances. We therefore aimed to characterize a key factor that blocks intestinal differentiation, define its transcriptional and epigenetic program, and provide preclinical evidence for therapeutic targeting in CRC.

Methods: Intestinal tissue from transgenic mice and patients were analyzed by means of histopathology and immunostaining. Human CRC cells and neoplastic murine organoids were genetically manipulated for functional studies. Gene expression profiling was obtained through RNA sequencing. Histone modifications and transcription factor binding were determined with the use of chromatin immunoprecipitation sequencing.

Results: We demonstrate that SRY-box transcription factor 9 (SOX9) promotes CRC by activating a stem cell-like program that hinders intestinal differentiation. Intestinal adenomas and colorectal adenocarcinomas from mouse models and patients demonstrate ectopic and elevated expression of SOX9. Functional experiments indicate a requirement for SOX9 in human CRC cell lines and engineered neoplastic organoids. Disrupting SOX9 activity impairs primary CRC tumor growth by inducing intestinal differentiation. By binding to genome wide enhancers, SOX9 directly activates genes associated with Paneth and stem cell activity, including prominin 1 (PROM1). SOX9 up-regulates PROM1 via a Wnt-responsive intronic enhancer. A pentaspan transmembrane protein, PROM1 uses its first intracellular domain to support stem cell signaling, at least in part through SOX9, reinforcing a PROM1-SOX9 positive feedback loop.

Conclusions: These studies establish SOX9 as a central regulator of an enhancer-driven stem cell-like program and carry important implications for developing therapeutics directed at overcoming differentiation defects in CRC. 
"""
