# phenotypes

JSON files containing genetic score models (in /json)

entries are:

1. "snps": vector of vector of SNPs in the model, see below.

2. "effect scale": the scale of the effect sizes. This is either "log-odds" or "sd", for a log-odds ratio scale or a standard deviation scale.

3. "pheno_id": should hold an identifier for the study from which this was defined, not currently used.

4. "build": the genome build for the SNP positions. 

5. "pheno": an abbreviation for the phenotype. 

Description of the "snps" object:


