## Installation
### CRAN install
install.packages("hlaR")<br>
### github install<br>
library(devtools)<br>
install_github("LarsenLab/hlaR")<br>
library(hlaR)<br> 

## Usage example
### Allele clean and mis-match
#### - clean
library(readr)<br>
clean <- read.csv(system.file("extdata/example", "HLA_Clean_test.csv", package = "hlaR"))<br>
clean1 <- CleanAllele(clean$recipient_a1, clean$recipient_a2)<br>
clean2 <- CleanAllele(clean$donor_a1, clean$donor_a2)<br>

#### - mis-match
dat <- read.csv(system.file("extdata/example", "HLA_Clean_test.csv", package = "hlaR"))<br>
mm1 <- EvalAlleleMism(dat$donor_a1, dat$donor_a2, dat$recipient_a1, dat$recipient_a2)<br>
mm1 <br>
mm2 <- EvalAlleleMism(dat$donor_b1, dat$donor_b2, dat$recipient_b1, dat$recipient_b2)<br>
mm2<br>

### haplotype
dat <- read.csv(system.file("extdata/example", "Haplotype_test.csv", package = "hlaR"))<br>
re <- ImputeHaplo(dat_in = dat)<br>

### single molecule level eplet mis-match
#### - MHC class I
dat <- read.csv(system.file("extdata/example", "MHC_I_test.csv", package = "hlaR"), sep = ",", header = TRUE)<br>
eplet_mm1_v2 <- CalEpletMHCI(dat, ver = 2)<br>
single_detail <- eplet_mm1_v2$single_detail<br>
overall_count <- eplet_mm1_v2$overall_count<br>

eplet_mm1_v3 <- CalEpletMHCI(dat, ver = 3)<br>
(or simply eplet_mm1_v3 <- CalEpletMHCI(dat) )<br>
single_detail <- eplet_mm1_v3$single_detail<br>
overall_count <- eplet_mm1_v3$overall_count<br>
#### - MHC class II
dat <- read.csv(system.file("extdata/example", "MHC_II_test.csv", package = "hlaR"), sep = ",", header = TRUE)<br>
eplet_mm2_v2 <- CalEpletMHCII(dat, ver = 2)<br>
single_detail <- eplet_mm2_v2$single_detail<br>
overall_count <- eplet_mm2_v2$overall_count<br>
eplet_mm2_v3 <- CalEpletMHCII(dat, ver = 3)<br>
(or simply eplet_mm2_v3 <- CalEpletMHCII_s(dat) )<br>
single_detail <- eplet_mm2_v3$single_detail<br>
overall_count <- eplet_mm2_v3$overall_count<br>

### other functionalities
#### - count of mis-match
hla_mm_cnt <- read.csv(system.file("extdata/example", "HLA_MisMatch_count_test.csv", package = "hlaR"))<br>
classI <- CountAlleleMism(hla_mm_cnt, c("mism_a", "mism_b"))<br>
classII <- CountAlleleMism(hla_mm_cnt, c("mism_drb1", "mism_dqa", "mism_dqb"))<br>
#### - topN most frequent recipient/donor alleles 
dat <- read.csv(system.file("extdata/example", "HLA_MisMatch_test.csv", package = "hlaR"))<br>
don <- c("donor.a1", "donor.a2")<br>
rcpt <- c("recipient.a1", "recipient.a2")<br>
re <- CalAlleleTopN(dat_in = dat, nms_don = don, nms_rcpt = rcpt, top_n = 2)<br>
re<br>
#### - frequency(freq count > 1) of donor mis-match alleles to recipients
dat <- read.csv(system.file("extdata/example", "HLA_MisMatch_test.csv", package = "hlaR"))<br>
don <- c("donor.a1", "donor.a2")<br>
rcpt <- c("recipient.a1", "recipient.a2")<br>
re <- CalAlleleMismFreq(dat_in = dat, nms_don = don, nms_rcpt = rcpt)<br> 
re

## ToDo/Discuss CRAN 0.1.2<br>
1. ~~hla clean: if any of hla typing ends with N or n, then set it to NA. note, this logic should be in the begining of the logic steps
2. ~~in imputation, in case user didn't use our hla-clean function, for each antigen, if there is NA and none-NA pair, then set both of them are none-NA typing
3. ~~low-res-cnt-flag bug
4. ~~vignettes(add DQB1, echo to hapltbl)
5. ~~MM reference tables: all upper cases
6. ~~add "Date/Publication" to the end of DESCRIPTION file (in press, Human Immunology)
7. ~~eplet mismatch: preserve source of DQ alpha and beta, and add them if they have same source
8. ~~eplet mism, remember to change default version to 2




