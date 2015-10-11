# phenotypes

JSON files containing genetic score models (in json/)

##JSON entries are:

1. "snps": vector of vector of SNPs in the model, see below.
2. "effect scale": the scale of the effect sizes. This is either "log-odds" or "sd", for a log-odds ratio scale or a standard deviation scale.
3. "pheno_id": should hold an identifier for the study from which this was defined, not currently used.
4. "build": the genome build for the SNP positions. 
5. "pheno": an abbreviation for the phenotype. 

##Description of the "snps" object:

This is a vector of vectors containing the lead SNPs that go into the phenotype score as well as all SNPs in LD with the lead SNP. In general you will only want to use the first entry in each of these vectors, which represents the lead SNP. 

Each SNP has the properties:

1. "snp_id": SNP identifier, usually an rs number. 
2. "chr": chromosome
3. "pos": position in the genome build defined above
4. "ref": reference allele
5. "alt": alternate allele
6. "eur_af": frequency of the alternate allele in European individuals (from 1000 Genomes Phase 1)
7. "afr_af": frequency of the alternate allele in African individuals (from 1000 Genomes Phase 1)
8. "asn_af": frequency of the alternate allele in East Asian individuals (from 1000 Genomes Phase 1)
9. "amr_af": frequency of the alternate allele in Native American individuals (from 1000 Genomes Phase 1)
10. "alt_effect_het": the effect size of the alternate allele in heterozygotes
11. "alt_effect_hom": the effect size of the alternate allele in homozygotes (in most cases this is just twice the effect size in heterozygotes since we're generally ignoring dominance)

##Usage

If you have a test genome, the score of the individual can be determined by simply adding up the effect sizes for all sites where the individual is either heterozygous or homozygous for the alternate allele (being sure to choose only one each of the SNPs that are in linkage disequilibrium). 

This is only meaningful in comparison with the population average, which can be obtained by summing the effect sizes times the allele frequencies in the relevant population for all alternate alleles (being sure to only include the same SNPs as used for the test genome). 

That is, if the units are standard deviations and the individual has a score of 2 compared to a population average of 1 (assuming the population--EUR, AFR, AMR, or ASN--is the population from which the individual is drawn), then the individual is predicted to be 1 s.d. above the mean. This can be converted to more natural units (e.g. cm for height) if the population mean and standard deviation are known.  

If the units are log-odds, this would mean that the individual's odds ratio to have the trait is 2.71 (e^1). Note that moving this to the probability scale requires knowing the population prevalence of the trait. 
