# FePDB
## README
FePDB is a curated, sequence-based protein database designed for the integrated annotation of microbial iron (Fe), phosphorus (P), and magnesium (Mg)-related metabolisms. It was developed to support comparative analysis of genomes, metagenomes, and other omics datasets where Fe and P cycling may be metabolically linked.

FePDB is intended for researchers studying microbial nutrient cycling, environmental microbiology, biogeochemistry, soil phosphorus mobilization, wastewater phosphorus removal, acid mine drainage, aquatic systems, and other environments where Fe-P interactions influence nutrient availability.


### Database contents



#### FePDB_v1.0.1.faa
Final non-redundant FePDB protein FASTA database. This is the primary file to use for 	   sequence searches and DIAMOND database construction.

#### Supplemental_Information.xlsx
Metadata describing FePDB gene families, protein names, metabolism groups, and sequence counts.

The current FePDB release contains:

- 375 gene families
- 18 metabolism groups
- More than 1.37 million protein reference sequences
- Fe-, P-, and Mg-associated pathways relevant to microbial nutrient acquisition, storage, regulation, transport, redox transformations, and central metabolism

Major metabolic categories include:

- P transporters
- P transporter regulators
- Polyphosphate metabolism
- Phosphonate and phosphinate metabolism
- Organic phosphoester hydrolysis
- Purine synthesis
- Pyrimidine synthesis
- Pentose phosphate pathway
- Pyruvate metabolism
- Filament and pili-related genes
- Fe oxidation
- Fe reduction
- Siderophore synthesis
- Siderophore transport
- Fe transport
- Fe gene regulation
- Fe storage
- Mg regulation


### FASTA header format

FePDB sequence identifiers are tagged with the prefix "fpdb_" to make downstream parsing and functional categorization easier.

Example identifier format:

from the _simple.faa files
> `>`accession_number fpdb_geneid

from the appended files
> `>`accession_number fpdb_geneid full_protein_name [species name]

The exact accession structure may vary by source sequence, but the "fpdb_" prefix indicates that the sequence belongs to FePDB.


### Recommended use with DIAMOND

FePDB can be used with DIAMOND for fast protein-level annotation of predicted proteins or translated nucleotide sequences.

For example:

1. Build a DIAMOND database:

    ```diamond makedb in FePDB_v1.0.1.faa db FePDB```

2. Search predicted proteins against FePDB:
```bash
diamond blastp \
  --query proteins.faa \
  --db FePDB.dmnd \
  --out FePDB_hits.tsv \
  --outfmt 6 qseqid sseqid pident length evalue bitscore qcovhsp scovhsp \
  --evalue 1e-5 \
  --max-target-seqs 1
```
  

A percent identity threshold of approximately 45% was used in the associated FePDB analysis after validation against a mixed FePDB/NCycDB benchmark dataset (*manuscript in process*.) Users may adjust identity, query coverage, and length thresholds depending on the goals of their analysis and desired balance between sensitivity and specificity.

Suggested filtering fields

For typical downstream analyses, consider filtering DIAMOND output using:

- e-value
- percent identity (pident)
- alignment length
- query coverage (qcovhsp)
- subject coverage (scovhsp), if relevant
- best hit per query sequence, when discrete gene counts are desired

Because FePDB is sequence-based, annotations are most appropriate for gene-level or protein-level abundance comparisons generated using a consistent search and filtering strategy.


### Example downstream workflow

A typical FePDB annotation workflow may look like this:

1. Predict genes or proteins from genomes/metagenomes.
2. Search predicted proteins against FePDB_v1.0.1.faa using DIAMOND blastp.
3. Filter DIAMOND hits using consistent identity, coverage, length, and e-value thresholds.
4. Parse FePDB identifiers to assign each hit to a gene family and metabolism group.
5. Summarize annotations by sample, genome, contig, gene family, or metabolic category.
6. Normalize counts as appropriate for the dataset, such as by total predicted genes, total mapped reads, TPM, or another study-specific denominator.


For stronger ecological interpretation, FePDB annotations should be paired when possible with:

- metatranscriptomic data
- metaproteomic data
- geochemical measurements
- environmental metadata
- genome-resolved or contig-level context

FePDB was designed to make Fe and P cycling easier to examine jointly. This is especially useful because microbial P availability may be influenced not only by canonical P acquisition genes, but also by Fe redox cycling, siderophore metabolism, intracellular Fe storage, polyphosphate metabolism, Mg regulation, and nutrient homeostasis.


Citation

Until a formal publication, DOI, or release archive is available, please cite this GitHub repository and include the version or commit hash used in your analysis.


Contact

For questions, corrections, or suggestions, please contact:

Olivia A. Rumble
Email: oarumb01@gmail.com
GitHub: https://github.com/OliviaAnneRumble


Version notes

Recommended release information to include:

Version: v1.0.1
Release date: 05-14-2026
Database file: FePDB_v1.0.1.faa
Number of gene families: 375
Number of metabolism groups: 18
Number of reference sequences: 1,374,199
# FePDB
FePDB is a databank containing protein sequences for iron and phosphorus genes in soil.
