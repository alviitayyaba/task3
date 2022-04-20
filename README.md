# Task 3 - Single nucleotide variants hands-on
Task completion using SNPEff and SNPSift tools:
1.)	Discard all the variants which are failed to pass the filtering
A)	Through attached R code
B)	Through SNPSift
cat tasks/task3/tumor_vs_normal.strelka.somatic.snvs.vcf | java -jar $SNPSift filter (“FILTER==’PASS’)” > filtered.vcf
2.)	Annotate filtered variants with the SNPeff using hg19 database
java -jar $SNPEff  hg19 tasks/task3/filtered.vcf > tumor_vs_normal.strelka.somatic.snvs.ann.vcf
3.)	Count the variants that change the protein encoded by the gene in which the variant is located. The list of possible consequences of changes
java -jar $SNPSift filter "ANN[*].EFFECT has 'missense_variant'" tasks/task3/tumor_vs_normal.strelka.somatic.snvs.anno.vcf > filter_missense_any.vcf
4.)	List a genes which are affected with the predicted Loss of function effect.
cat tasks/task3/tumor_vs_normal.strelka.somatic.snvs.anno.vcf | java -jar $SNPSift filter "(exists LOF[*].PERC) & (LOF[*].PERC > 0.5)" > tasks/task3/filtered-LOF.vcf
Supplimentary data:
tumor_vs_normal.strelka.somatic.snvs.vcf.gz
