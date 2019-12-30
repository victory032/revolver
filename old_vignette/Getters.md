Getter functions
================
Giulio Caravagna
May 1, 2019

``` r
# Load REVOLVER 
library(revolver)
```

    ##  [ ctree - Clone Trees in cancer ] 
    ## Author :  Giulio Caravagna <gcaravagn@gmail.com> 
    ## GitHub :  caravagn/ctree 
    ## 
    ## Available datasets ~ use data('xxx', package='REVOLVER_datasets') to load dataset 'xxx'
    ## 
    ## ◉ TRACERx_NEJM_2017 Mutations from TRACERx lung (NEJM2017, PMID: 28445112). n = 99 patients, multi-region WES. 
    ## ◉ TRACERx_NEJM_2017_REVOLVER REVOLVER analysis of TRACERx_NEJM_2017. 
    ##  [ REVOLVER - Repeated Evolution in Cancer ] 
    ## Author :  Giulio Caravagna <gcaravagn@gmail.com> 
    ## GitHub :  caravagn/revolver

In this vignette we make use of one of the cohort objects released with
the tool.

``` r
# Data released in the 'evoverse.datasets'
data('TRACERx_NEJM_2017_REVOLVER', package = 'evoverse.datasets')

# We can use S3 object functions to retrieve simple information about the plot.
# The `print` functions runs also the `revolver_check_cohort` function which 
# tells us that some patient have only 1 clone with drivers, and therefore they
# can just be expanded.
TRACERx_NEJM_2017_REVOLVER
```

    ## $patients
    ##  [1] "CRUK0001" "CRUK0002" "CRUK0003" "CRUK0004" "CRUK0005" "CRUK0006"
    ##  [7] "CRUK0007" "CRUK0008" "CRUK0009" "CRUK0010" "CRUK0011" "CRUK0012"
    ## [13] "CRUK0013" "CRUK0014" "CRUK0015" "CRUK0016" "CRUK0017" "CRUK0018"
    ## [19] "CRUK0019" "CRUK0020" "CRUK0021" "CRUK0022" "CRUK0023" "CRUK0024"
    ## [25] "CRUK0025" "CRUK0026" "CRUK0027" "CRUK0028" "CRUK0029" "CRUK0030"
    ## [31] "CRUK0031" "CRUK0032" "CRUK0033" "CRUK0034" "CRUK0035" "CRUK0036"
    ## [37] "CRUK0037" "CRUK0038" "CRUK0039" "CRUK0040" "CRUK0041" "CRUK0042"
    ## [43] "CRUK0043" "CRUK0044" "CRUK0045" "CRUK0046" "CRUK0047" "CRUK0048"
    ## [49] "CRUK0049" "CRUK0050" "CRUK0051" "CRUK0052" "CRUK0054" "CRUK0055"
    ## [55] "CRUK0056" "CRUK0057" "CRUK0058" "CRUK0059" "CRUK0060" "CRUK0061"
    ## [61] "CRUK0062" "CRUK0063" "CRUK0064" "CRUK0065" "CRUK0066" "CRUK0067"
    ## [67] "CRUK0068" "CRUK0069" "CRUK0070" "CRUK0071" "CRUK0072" "CRUK0073"
    ## [73] "CRUK0074" "CRUK0075" "CRUK0076" "CRUK0077" "CRUK0078" "CRUK0079"
    ## [79] "CRUK0080" "CRUK0081" "CRUK0082" "CRUK0083" "CRUK0084" "CRUK0085"
    ## [85] "CRUK0086" "CRUK0087" "CRUK0088" "CRUK0089" "CRUK0090" "CRUK0091"
    ## [91] "CRUK0092" "CRUK0093" "CRUK0094" "CRUK0095" "CRUK0096" "CRUK0097"
    ## [97] "CRUK0098" "CRUK0099" "CRUK0100"
    ## 
    ## $variantIDs
    ##  [1] "NF1"       "ARHGAP35"  "TP53"      "MGA"       "WRN"      
    ##  [6] "EGFR"      "PASK"      "RB1"       "IKZF1"     "KRAS"     
    ## [11] "MET"       "TERT"      "EP300"     "PIK3CA"    "CDKN2A"   
    ## [16] "CTNNB1"    "SMAD4"     "NOTCH1"    "NRAS"      "CMTR2"    
    ## [21] "BRAF"      "PLXNB2"    "KEAP1"     "MAP3K1"    "FANCC"    
    ## [26] "SGK223"    "STK11"     "PRDM1"     "U2AF1"     "MYC"      
    ## [31] "ARID2"     "KMT2C"     "NFE2L2"    "SETD2"     "FLT4"     
    ## [36] "RNF43"     "BAP1"      "FAT1"      "SPEN"      "CBLB"     
    ## [41] "ASXL1"     "PTPRC"     "DNM2"      "LATS1"     "ARID1B"   
    ## [46] "COL5A2"    "COL2A1"    "PRF1"      "NCOR1"     "CHEK2"    
    ## [51] "CIC"       "KMT2D"     "POLE"      "ATM"       "SERPINB13"
    ## [56] "APC"       "CCND1"     "TSC2"      "FBXW7"     "FGFR1"    
    ## [61] "RAD21"     "FAS"       "NCOA6"     "CREBBP"    "PHOX2B"   
    ## [66] "GATA3"     "NOTCH2"    "UBR5"      "FANCM"     "RASA1"    
    ## [71] "SMARCA4"   "SOX2"      "CYLD"      "MLH1"      "PDGFRA"   
    ## [76] "PTEN"      "DICER1"    "WT1"       "CUX1"     
    ## 
    ## $variantIDs.driver
    ##  [1] "NF1"       "ARHGAP35"  "TP53"      "MGA"       "WRN"      
    ##  [6] "EGFR"      "PASK"      "RB1"       "IKZF1"     "KRAS"     
    ## [11] "MET"       "TERT"      "EP300"     "PIK3CA"    "CDKN2A"   
    ## [16] "CTNNB1"    "SMAD4"     "NOTCH1"    "NRAS"      "CMTR2"    
    ## [21] "BRAF"      "PLXNB2"    "KEAP1"     "MAP3K1"    "FANCC"    
    ## [26] "SGK223"    "STK11"     "PRDM1"     "U2AF1"     "MYC"      
    ## [31] "ARID2"     "KMT2C"     "NFE2L2"    "SETD2"     "FLT4"     
    ## [36] "RNF43"     "BAP1"      "FAT1"      "SPEN"      "CBLB"     
    ## [41] "ASXL1"     "PTPRC"     "DNM2"      "LATS1"     "ARID1B"   
    ## [46] "COL5A2"    "COL2A1"    "PRF1"      "NCOR1"     "CHEK2"    
    ## [51] "CIC"       "KMT2D"     "POLE"      "ATM"       "SERPINB13"
    ## [56] "APC"       "CCND1"     "TSC2"      "FBXW7"     "FGFR1"    
    ## [61] "RAD21"     "FAS"       "NCOA6"     "CREBBP"    "PHOX2B"   
    ## [66] "GATA3"     "NOTCH2"    "UBR5"      "FANCM"     "RASA1"    
    ## [71] "SMARCA4"   "SOX2"      "CYLD"      "MLH1"      "PDGFRA"   
    ## [76] "PTEN"      "DICER1"    "WT1"       "CUX1"     
    ## 
    ## $numVariants
    ## [1] 450
    ## 
    ## $annotation
    ## [1] "TRACERx NEJM 2017"
    ## 
    ## $dataset
    ## $dataset$CRUK0001
    ## # A tibble: 7 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0001  NF1       TRUE      FALSE     1                  1
    ## 2 __mu… CRUK… CRUK0001  ARHGAP35  TRUE      FALSE     2                  1
    ## 3 __mu… CRUK… CRUK0001  TP53      TRUE      TRUE      3                  4
    ## 4 __mu… CRUK… CRUK0001  MGA       TRUE      TRUE      3                  4
    ## 5 __mu… CRUK… CRUK0001  WRN       TRUE      TRUE      3                  4
    ## 6 __mu… Anno… CRUK0001  EGFR      TRUE      TRUE      3                  4
    ## 7 __mu… CRUK… CRUK0001  PASK      TRUE      FALSE     5                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0002
    ## # A tibble: 7 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0002  RB1       TRUE      FALSE     1                  3
    ## 2 __mu… CRUK… CRUK0002  IKZF1     TRUE      FALSE     1                  3
    ## 3 __mu… Anno… CRUK0002  KRAS      TRUE      FALSE     1                  3
    ## 4 __mu… CRUK… CRUK0002  MET       TRUE      TRUE      2                  2
    ## 5 __mu… Anno… CRUK0002  TERT      TRUE      TRUE      2                  2
    ## 6 __mu… CRUK… CRUK0002  NF1       TRUE      FALSE     5                  1
    ## 7 __mu… CRUK… CRUK0002  EP300     TRUE      FALSE     6                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0003
    ## # A tibble: 4 x 14
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0003  PIK3CA    TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0003  EGFR      TRUE      TRUE      1                  3
    ## 3 __mu… Anno… CRUK0003  CDKN2A    TRUE      TRUE      1                  3
    ## 4 __mu… CRUK… CRUK0003  CTNNB1    TRUE      FALSE     4                  1
    ## # … with 6 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>, R6 <dbl>
    ## 
    ## $dataset$CRUK0004
    ## # A tibble: 4 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0004  SMAD4     TRUE      FALSE     1                  2
    ## 2 __mu… CRUK… CRUK0004  NOTCH1    TRUE      FALSE     1                  2
    ## 3 __mu… CRUK… CRUK0004  TP53      TRUE      TRUE      2                  2
    ## 4 __mu… CRUK… CRUK0004  EGFR      TRUE      TRUE      2                  2
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0005
    ## # A tibble: 6 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0005  NRAS      TRUE      FALSE     1                  1
    ## 2 __mu… CRUK… CRUK0005  CMTR2     TRUE      TRUE      2                  5
    ## 3 __mu… CRUK… CRUK0005  TP53      TRUE      TRUE      2                  5
    ## 4 __mu… CRUK… CRUK0005  BRAF      TRUE      TRUE      2                  5
    ## 5 __mu… CRUK… CRUK0005  PASK      TRUE      TRUE      2                  5
    ## 6 __mu… Anno… CRUK0005  TERT      TRUE      TRUE      2                  5
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0006
    ## # A tibble: 6 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0006  PLXNB2    TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0006  TP53      TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0006  KEAP1     TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0006  TERT      TRUE      TRUE      1                  4
    ## 5 __mu… CRUK… CRUK0006  MAP3K1    TRUE      FALSE     2                  1
    ## 6 __mu… CRUK… CRUK0006  FANCC     TRUE      FALSE     7                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0007
    ## # A tibble: 3 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0007  PIK3CA    TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0007  EGFR      TRUE      TRUE      1                  3
    ## 3 __mu… Anno… CRUK0007  SGK223    TRUE      TRUE      1                  3
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0008
    ## # A tibble: 6 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0008  KEAP1     TRUE      TRUE      2                  5
    ## 2 __mu… CRUK… CRUK0008  STK11     TRUE      TRUE      2                  5
    ## 3 __mu… CRUK… CRUK0008  PRDM1     TRUE      TRUE      2                  5
    ## 4 __mu… CRUK… CRUK0008  U2AF1     TRUE      TRUE      2                  5
    ## 5 __mu… Anno… CRUK0008  MYC       TRUE      TRUE      2                  5
    ## 6 __mu… CRUK… CRUK0008  ARID2     TRUE      FALSE     3                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0009
    ## # A tibble: 7 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0009  BRAF      TRUE      TRUE      1                  6
    ## 2 __mu… CRUK… CRUK0009  TP53      TRUE      TRUE      1                  6
    ## 3 __mu… CRUK… CRUK0009  ARHGAP35  TRUE      TRUE      1                  6
    ## 4 __mu… CRUK… CRUK0009  KMT2C     TRUE      TRUE      1                  6
    ## 5 __mu… Anno… CRUK0009  NFE2L2    TRUE      TRUE      1                  6
    ## 6 __mu… Anno… CRUK0009  MET       TRUE      TRUE      1                  6
    ## 7 __mu… Anno… CRUK0009  TERT      TRUE      FALSE     2                  1
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0010
    ## # A tibble: 3 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0010  SETD2     TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0010  EGFR      TRUE      TRUE      1                  3
    ## 3 __mu… Anno… CRUK0010  TERT      TRUE      TRUE      1                  3
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0011
    ## # A tibble: 2 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0011  KRAS      TRUE      TRUE      1                  1
    ## 2 __mu… CRUK… CRUK0011  FLT4      TRUE      FALSE     3                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0012
    ## # A tibble: 1 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0012  EGFR      TRUE      TRUE      1                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0013
    ## # A tibble: 4 x 14
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0013  STK11     TRUE      TRUE      1                  1
    ## 2 __mu… CRUK… CRUK0013  NOTCH1    TRUE      FALSE     2                  1
    ## 3 __mu… Anno… CRUK0013  KRAS      TRUE      FALSE     3                  1
    ## 4 __mu… Anno… CRUK0013  EGFR      TRUE      FALSE     4                  1
    ## # … with 6 more variables: CCF <chr>, LN1 <dbl>, LN2 <dbl>, R1 <dbl>,
    ## #   R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0014
    ## # A tibble: 3 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0014  TP53      TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0014  KRAS      TRUE      TRUE      1                  2
    ## 3 __mu… CRUK… CRUK0014  RNF43     TRUE      FALSE     2                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0015
    ## # A tibble: 4 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0015  BAP1      TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0015  EGFR      TRUE      TRUE      1                  2
    ## 3 __mu… CRUK… CRUK0015  TP53      TRUE      FALSE     2                  1
    ## 4 __mu… CRUK… CRUK0015  RB1       TRUE      FALSE     3                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0016
    ## # A tibble: 11 x 11
    ##    id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##    <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ##  1 __mu… CRUK… CRUK0016  TP53      TRUE      TRUE      1                  6
    ##  2 __mu… CRUK… CRUK0016  FAT1      TRUE      TRUE      1                  6
    ##  3 __mu… CRUK… CRUK0016  SPEN      TRUE      TRUE      1                  6
    ##  4 __mu… CRUK… CRUK0016  CBLB      TRUE      TRUE      1                  6
    ##  5 __mu… Anno… CRUK0016  TERT      TRUE      TRUE      1                  6
    ##  6 __mu… Anno… CRUK0016  CDKN2A    TRUE      TRUE      1                  6
    ##  7 __mu… CRUK… CRUK0016  ASXL1     TRUE      FALSE     2                  1
    ##  8 __mu… CRUK… CRUK0016  PTPRC     TRUE      FALSE     6                  1
    ##  9 __mu… CRUK… CRUK0016  DNM2      TRUE      FALSE     10                 1
    ## 10 __mu… CRUK… CRUK0016  LATS1     TRUE      FALSE     16                 2
    ## 11 __mu… CRUK… CRUK0016  ARID1B    TRUE      FALSE     16                 2
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0017
    ## # A tibble: 6 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0017  TP53      TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0017  ARID1B    TRUE      TRUE      1                  5
    ## 3 __mu… CRUK… CRUK0017  ARID2     TRUE      TRUE      1                  5
    ## 4 __mu… CRUK… CRUK0017  KEAP1     TRUE      TRUE      1                  5
    ## 5 __mu… Anno… CRUK0017  MYC       TRUE      TRUE      1                  5
    ## 6 __mu… CRUK… CRUK0017  KRAS      TRUE      FALSE     3                  1
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0018
    ## # A tibble: 4 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0018  CMTR2     TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0018  KRAS      TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0018  MGA       TRUE      TRUE      1                  4
    ## 4 __mu… CRUK… CRUK0018  COL5A2    TRUE      TRUE      1                  4
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0019
    ## # A tibble: 1 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0019  EGFR      TRUE      TRUE      1                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0020
    ## # A tibble: 10 x 11
    ##    id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##    <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ##  1 __mu… CRUK… CRUK0020  KEAP1     TRUE      TRUE      1                  7
    ##  2 __mu… CRUK… CRUK0020  TP53      TRUE      TRUE      1                  7
    ##  3 __mu… CRUK… CRUK0020  MGA       TRUE      TRUE      1                  7
    ##  4 __mu… CRUK… CRUK0020  ARID2     TRUE      TRUE      1                  7
    ##  5 __mu… CRUK… CRUK0020  COL2A1    TRUE      TRUE      1                  7
    ##  6 __mu… CRUK… CRUK0020  PRF1      TRUE      TRUE      1                  7
    ##  7 __mu… Anno… CRUK0020  KRAS      TRUE      TRUE      1                  7
    ##  8 __mu… CRUK… CRUK0020  PIK3CA    TRUE      FALSE     2                  1
    ##  9 __mu… CRUK… CRUK0020  BAP1      TRUE      FALSE     3                  1
    ## 10 __mu… CRUK… CRUK0020  NCOR1     TRUE      FALSE     4                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0021
    ## # A tibble: 4 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0021  EGFR      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0021  TP53      TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0021  CHEK2     TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0021  CDKN2A    TRUE      TRUE      1                  4
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0022
    ## # A tibble: 3 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0022  TP53      TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0022  EGFR      TRUE      TRUE      1                  2
    ## 3 __mu… CRUK… CRUK0022  CIC       TRUE      FALSE     2                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0023
    ## # A tibble: 6 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0023  WRN       TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0023  KRAS      TRUE      TRUE      1                  3
    ## 3 __mu… Anno… CRUK0023  CDKN2A    TRUE      TRUE      1                  3
    ## 4 __mu… CRUK… CRUK0023  TP53      TRUE      FALSE     2                  1
    ## 5 __mu… CRUK… CRUK0023  PTPRC     TRUE      FALSE     4                  2
    ## 6 __mu… CRUK… CRUK0023  KMT2D     TRUE      FALSE     4                  2
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0024
    ## # A tibble: 6 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0024  TP53      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0024  STK11     TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0024  POLE      TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0024  EGFR      TRUE      TRUE      1                  4
    ## 5 __mu… CRUK… CRUK0024  ATM       TRUE      FALSE     3                  1
    ## 6 __mu… CRUK… CRUK0024  NCOR1     TRUE      FALSE     4                  1
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R3 <dbl>, R4 <dbl>,
    ## #   R6 <dbl>
    ## 
    ## $dataset$CRUK0025
    ## # A tibble: 3 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0025  KRAS      TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0025  TP53      TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0025  MGA       TRUE      TRUE      1                  3
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0026
    ## # A tibble: 4 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0026  TP53      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0026  EGFR      TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0026  RB1       TRUE      TRUE      1                  4
    ## 4 __mu… CRUK… CRUK0026  SERPINB13 TRUE      TRUE      1                  4
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0027
    ## # A tibble: 3 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0027  KRAS      TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0027  TP53      TRUE      TRUE      1                  2
    ## 3 __mu… CRUK… CRUK0027  PLXNB2    TRUE      FALSE     2                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0028
    ## # A tibble: 2 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0028  APC       TRUE      TRUE      1                  2
    ## 2 __mu… Anno… CRUK0028  EGFR      TRUE      TRUE      1                  2
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0029
    ## # A tibble: 4 x 15
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0029  TP53      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0029  NRAS      TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0029  MGA       TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0029  CCND1     TRUE      TRUE      1                  4
    ## # … with 7 more variables: CCF <chr>, R2 <dbl>, R4 <dbl>, R5 <dbl>,
    ## #   R6 <dbl>, R7 <dbl>, R8 <dbl>
    ## 
    ## $dataset$CRUK0030
    ## # A tibble: 6 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0030  KRAS      TRUE      TRUE      1                  6
    ## 2 __mu… CRUK… CRUK0030  TSC2      TRUE      TRUE      1                  6
    ## 3 __mu… CRUK… CRUK0030  U2AF1     TRUE      TRUE      1                  6
    ## 4 __mu… CRUK… CRUK0030  TP53      TRUE      TRUE      1                  6
    ## 5 __mu… CRUK… CRUK0030  FBXW7     TRUE      TRUE      1                  6
    ## 6 __mu… CRUK… CRUK0030  NF1       TRUE      TRUE      1                  6
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0031
    ## # A tibble: 5 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0031  KEAP1     TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0031  CDKN2A    TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0031  PRF1      TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0031  FGFR1     TRUE      TRUE      1                  4
    ## 5 __mu… CRUK… CRUK0031  NF1       TRUE      FALSE     6                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0032
    ## # A tibble: 6 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0032  ATM       TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0032  RAD21     TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0032  U2AF1     TRUE      TRUE      1                  4
    ## 4 __mu… CRUK… CRUK0032  RNF43     TRUE      TRUE      1                  4
    ## 5 __mu… Anno… CRUK0032  CCND1     TRUE      FALSE     4                  1
    ## 6 __mu… CRUK… CRUK0032  ARID1B    TRUE      FALSE     6                  1
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0033
    ## # A tibble: 2 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0033  KEAP1     TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0033  CTNNB1    TRUE      TRUE      1                  2
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0034
    ## # A tibble: 4 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0034  ATM       TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0034  KRAS      TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0034  PLXNB2    TRUE      TRUE      1                  3
    ## 4 __mu… CRUK… CRUK0034  MGA       TRUE      FALSE     4                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0035
    ## # A tibble: 3 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0035  TP53      TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0035  FAS       TRUE      TRUE      1                  2
    ## 3 __mu… CRUK… CRUK0035  FLT4      TRUE      FALSE     4                  1
    ## # … with 5 more variables: CCF <chr>, LN1 <dbl>, R1 <dbl>, R2 <dbl>,
    ## #   R3 <dbl>
    ## 
    ## $dataset$CRUK0036
    ## # A tibble: 5 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0036  KRAS      TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0036  PIK3CA    TRUE      TRUE      1                  5
    ## 3 __mu… CRUK… CRUK0036  KEAP1     TRUE      TRUE      1                  5
    ## 4 __mu… CRUK… CRUK0036  ARHGAP35  TRUE      TRUE      1                  5
    ## 5 __mu… Anno… CRUK0036  TERT      TRUE      TRUE      1                  5
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0037
    ## # A tibble: 3 x 14
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0037  NCOA6     TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0037  CREBBP    TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0037  KRAS      TRUE      TRUE      1                  3
    ## # … with 6 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>, R5 <dbl>
    ## 
    ## $dataset$CRUK0038
    ## # A tibble: 2 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0038  KRAS      TRUE      TRUE      1                  1
    ## 2 __mu… CRUK… CRUK0038  KMT2D     TRUE      FALSE     3                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0039
    ## # A tibble: 4 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0039  KRAS      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0039  CMTR2     TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0039  NF1       TRUE      TRUE      1                  4
    ## 4 __mu… CRUK… CRUK0039  PHOX2B    TRUE      TRUE      1                  4
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0040
    ## # A tibble: 4 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0040  NCOR1     TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0040  RAD21     TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0040  KRAS      TRUE      TRUE      1                  4
    ## 4 __mu… CRUK… CRUK0040  GATA3     TRUE      TRUE      1                  4
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0041
    ## # A tibble: 3 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0041  BRAF      TRUE      TRUE      1                  3
    ## 2 __mu… Anno… CRUK0041  TERT      TRUE      TRUE      1                  3
    ## 3 __mu… Anno… CRUK0041  EGFR      TRUE      TRUE      1                  3
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0042
    ## # A tibble: 1 x 10
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0042  KRAS      TRUE      TRUE      1                  1
    ## # … with 2 more variables: CCF <chr>, R1 <dbl>
    ## 
    ## $dataset$CRUK0043
    ## # A tibble: 1 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0043  MET       TRUE      TRUE      1                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0044
    ## # A tibble: 1 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0044  KRAS      TRUE      TRUE      1                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0045
    ## # A tibble: 1 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0045  BAP1      TRUE      TRUE      1                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0046
    ## # A tibble: 2 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0046  KEAP1     TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0046  APC       TRUE      TRUE      1                  2
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0047
    ## # A tibble: 4 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0047  STK11     TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0047  APC       TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0047  KRAS      TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0047  MYC       TRUE      TRUE      1                  4
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0048
    ## # A tibble: 7 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0048  APC       TRUE      TRUE      1                  7
    ## 2 __mu… CRUK… CRUK0048  PRDM1     TRUE      TRUE      1                  7
    ## 3 __mu… CRUK… CRUK0048  ARHGAP35  TRUE      TRUE      1                  7
    ## 4 __mu… CRUK… CRUK0048  TP53      TRUE      TRUE      1                  7
    ## 5 __mu… CRUK… CRUK0048  BRAF      TRUE      TRUE      1                  7
    ## 6 __mu… Anno… CRUK0048  EGFR      TRUE      TRUE      1                  7
    ## 7 __mu… Anno… CRUK0048  MYC       TRUE      TRUE      1                  7
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0049
    ## # A tibble: 5 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0049  RB1       TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0049  TP53      TRUE      TRUE      1                  5
    ## 3 __mu… CRUK… CRUK0049  COL2A1    TRUE      TRUE      1                  5
    ## 4 __mu… Anno… CRUK0049  EGFR      TRUE      TRUE      1                  5
    ## 5 __mu… Anno… CRUK0049  KRAS      TRUE      TRUE      1                  5
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0050
    ## # A tibble: 3 x 14
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0050  KRAS      TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0050  STK11     TRUE      TRUE      1                  3
    ## 3 __mu… Anno… CRUK0050  MYC       TRUE      TRUE      1                  3
    ## # … with 6 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>, R5 <dbl>
    ## 
    ## $dataset$CRUK0051
    ## # A tibble: 5 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0051  KRAS      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0051  FBXW7     TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0051  TP53      TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0051  EGFR      TRUE      TRUE      1                  4
    ## 5 __mu… CRUK… CRUK0051  EP300     TRUE      FALSE     3                  1
    ## # … with 4 more variables: CCF <chr>, R2 <dbl>, R3 <dbl>, R4 <dbl>
    ## 
    ## $dataset$CRUK0052
    ## # A tibble: 9 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0052  KMT2D     TRUE      TRUE      1                  8
    ## 2 __mu… CRUK… CRUK0052  KRAS      TRUE      TRUE      1                  8
    ## 3 __mu… CRUK… CRUK0052  NOTCH2    TRUE      TRUE      1                  8
    ## 4 __mu… CRUK… CRUK0052  MGA       TRUE      TRUE      1                  8
    ## 5 __mu… CRUK… CRUK0052  KEAP1     TRUE      TRUE      1                  8
    ## 6 __mu… CRUK… CRUK0052  TP53      TRUE      TRUE      1                  8
    ## 7 __mu… CRUK… CRUK0052  NF1       TRUE      TRUE      1                  8
    ## 8 __mu… CRUK… CRUK0052  SGK223    TRUE      TRUE      1                  8
    ## 9 __mu… CRUK… CRUK0052  UBR5      TRUE      FALSE     2                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R3 <dbl>, R4 <dbl>
    ## 
    ## $dataset$CRUK0054
    ## # A tibble: 1 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0054  EGFR      TRUE      TRUE      1                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0055
    ## # A tibble: 3 x 10
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0055  FANCM     TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0055  UBR5      TRUE      TRUE      1                  2
    ## 3 __mu… CRUK… CRUK0055  FAT1      TRUE      FALSE     2                  1
    ## # … with 2 more variables: CCF <chr>, R2 <dbl>
    ## 
    ## $dataset$CRUK0056
    ## # A tibble: 3 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0056  RASA1     TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0056  CREBBP    TRUE      TRUE      1                  2
    ## 3 __mu… CRUK… CRUK0056  TP53      TRUE      FALSE     3                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0057
    ## # A tibble: 5 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0057  KRAS      TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0057  SMARCA4   TRUE      TRUE      1                  5
    ## 3 __mu… CRUK… CRUK0057  TSC2      TRUE      TRUE      1                  5
    ## 4 __mu… CRUK… CRUK0057  DNM2      TRUE      TRUE      1                  5
    ## 5 __mu… Anno… CRUK0057  TERT      TRUE      TRUE      1                  5
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0058
    ## # A tibble: 2 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0058  TP53      TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0058  EGFR      TRUE      TRUE      1                  2
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0059
    ## # A tibble: 1 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0059  KRAS      TRUE      TRUE      1                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0060
    ## # A tibble: 11 x 10
    ##    id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##    <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ##  1 __mu… CRUK… CRUK0060  SERPINB13 TRUE      TRUE      1                 11
    ##  2 __mu… CRUK… CRUK0060  ARID2     TRUE      TRUE      1                 11
    ##  3 __mu… CRUK… CRUK0060  COL5A2    TRUE      TRUE      1                 11
    ##  4 __mu… CRUK… CRUK0060  FANCM     TRUE      TRUE      1                 11
    ##  5 __mu… CRUK… CRUK0060  PHOX2B    TRUE      TRUE      1                 11
    ##  6 __mu… CRUK… CRUK0060  COL2A1    TRUE      TRUE      1                 11
    ##  7 __mu… CRUK… CRUK0060  RASA1     TRUE      TRUE      1                 11
    ##  8 __mu… CRUK… CRUK0060  NF1       TRUE      TRUE      1                 11
    ##  9 __mu… CRUK… CRUK0060  NCOA6     TRUE      TRUE      1                 11
    ## 10 __mu… CRUK… CRUK0060  NOTCH2    TRUE      TRUE      1                 11
    ## 11 __mu… CRUK… CRUK0060  KMT2C     TRUE      TRUE      1                 11
    ## # … with 2 more variables: CCF <chr>, R1 <dbl>
    ## 
    ## $dataset$CRUK0061
    ## # A tibble: 1 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0061  STK11     TRUE      TRUE      1                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0062
    ## # A tibble: 7 x 16
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0062  FAS       TRUE      FALSE     1                  1
    ## 2 __mu… CRUK… CRUK0062  PLXNB2    TRUE      FALSE     2                  1
    ## 3 __mu… CRUK… CRUK0062  TP53      TRUE      TRUE      4                  4
    ## 4 __mu… Anno… CRUK0062  PIK3CA    TRUE      TRUE      4                  4
    ## 5 __mu… Anno… CRUK0062  SOX2      TRUE      TRUE      4                  4
    ## 6 __mu… Anno… CRUK0062  CCND1     TRUE      TRUE      4                  4
    ## 7 __mu… CRUK… CRUK0062  UBR5      TRUE      FALSE     16                 1
    ## # … with 8 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>, R5 <dbl>, R6 <dbl>, R7 <dbl>
    ## 
    ## $dataset$CRUK0063
    ## # A tibble: 11 x 14
    ##    id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##    <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ##  1 __mu… CRUK… CRUK0063  NF1       TRUE      FALSE     1                  2
    ##  2 __mu… CRUK… CRUK0063  CYLD      TRUE      FALSE     1                  2
    ##  3 __mu… CRUK… CRUK0063  PIK3CA    TRUE      TRUE      2                  7
    ##  4 __mu… CRUK… CRUK0063  TP53      TRUE      TRUE      2                  7
    ##  5 __mu… CRUK… CRUK0063  FBXW7     TRUE      TRUE      2                  7
    ##  6 __mu… CRUK… CRUK0063  CDKN2A    TRUE      TRUE      2                  7
    ##  7 __mu… Anno… CRUK0063  SOX2      TRUE      TRUE      2                  7
    ##  8 __mu… Anno… CRUK0063  TERT      TRUE      TRUE      2                  7
    ##  9 __mu… Anno… CRUK0063  PRF1      TRUE      TRUE      2                  7
    ## 10 __mu… CRUK… CRUK0063  FANCM     TRUE      FALSE     6                  1
    ## 11 __mu… CRUK… CRUK0063  EP300     TRUE      FALSE     10                 1
    ## # … with 6 more variables: CCF <chr>, R3 <dbl>, R4 <dbl>, R5 <dbl>,
    ## #   R6 <dbl>, R7 <dbl>
    ## 
    ## $dataset$CRUK0064
    ## # A tibble: 3 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0064  TP53      TRUE      TRUE      1                  1
    ## 2 __mu… CRUK… CRUK0064  MLH1      TRUE      FALSE     2                  2
    ## 3 __mu… CRUK… CRUK0064  FAT1      TRUE      FALSE     2                  2
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0065
    ## # A tibble: 9 x 15
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0065  TP53      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0065  NFE2L2    TRUE      TRUE      1                  4
    ## 3 __mu… Anno… CRUK0065  PIK3CA    TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0065  SOX2      TRUE      TRUE      1                  4
    ## 5 __mu… CRUK… CRUK0065  MLH1      TRUE      FALSE     2                  3
    ## 6 __mu… CRUK… CRUK0065  PTPRC     TRUE      FALSE     2                  3
    ## 7 __mu… CRUK… CRUK0065  UBR5      TRUE      FALSE     2                  3
    ## 8 __mu… CRUK… CRUK0065  NOTCH1    TRUE      FALSE     6                  2
    ## 9 __mu… CRUK… CRUK0065  NCOA6     TRUE      FALSE     6                  2
    ## # … with 7 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>, R5 <dbl>, R6 <dbl>
    ## 
    ## $dataset$CRUK0066
    ## # A tibble: 8 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0066  TP53      TRUE      TRUE      1                  7
    ## 2 __mu… CRUK… CRUK0066  NOTCH1    TRUE      TRUE      1                  7
    ## 3 __mu… CRUK… CRUK0066  CDKN2A    TRUE      TRUE      1                  7
    ## 4 __mu… CRUK… CRUK0066  WRN       TRUE      TRUE      1                  7
    ## 5 __mu… Anno… CRUK0066  PDGFRA    TRUE      TRUE      1                  7
    ## 6 __mu… Anno… CRUK0066  TERT      TRUE      TRUE      1                  7
    ## 7 __mu… Anno… CRUK0066  NCOA6     TRUE      TRUE      1                  7
    ## 8 __mu… CRUK… CRUK0066  COL5A2    TRUE      FALSE     9                  1
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0067
    ## # A tibble: 6 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0067  NOTCH1    TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0067  TP53      TRUE      TRUE      1                  5
    ## 3 __mu… Anno… CRUK0067  PIK3CA    TRUE      TRUE      1                  5
    ## 4 __mu… Anno… CRUK0067  SOX2      TRUE      TRUE      1                  5
    ## 5 __mu… Anno… CRUK0067  CDKN2A    TRUE      TRUE      1                  5
    ## 6 __mu… CRUK… CRUK0067  NFE2L2    TRUE      FALSE     2                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0068
    ## # A tibble: 8 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0068  TP53      TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0068  PTEN      TRUE      TRUE      1                  5
    ## 3 __mu… CRUK… CRUK0068  KMT2D     TRUE      TRUE      1                  5
    ## 4 __mu… Anno… CRUK0068  PIK3CA    TRUE      TRUE      1                  5
    ## 5 __mu… Anno… CRUK0068  SOX2      TRUE      TRUE      1                  5
    ## 6 __mu… CRUK… CRUK0068  MGA       TRUE      FALSE     3                  1
    ## 7 __mu… CRUK… CRUK0068  SETD2     TRUE      FALSE     4                  1
    ## 8 __mu… Anno… CRUK0068  TERT      TRUE      FALSE     9                  1
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0069
    ## # A tibble: 5 x 14
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0069  TP53      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0069  FAT1      TRUE      TRUE      1                  4
    ## 3 __mu… Anno… CRUK0069  PDGFRA    TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0069  FGFR1     TRUE      TRUE      1                  4
    ## 5 __mu… CRUK… CRUK0069  KRAS      TRUE      FALSE     13                 1
    ## # … with 6 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>, R5 <dbl>
    ## 
    ## $dataset$CRUK0070
    ## # A tibble: 6 x 14
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0070  DNM2      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0070  TP53      TRUE      TRUE      1                  4
    ## 3 __mu… Anno… CRUK0070  COL5A2    TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0070  SOX2      TRUE      TRUE      1                  4
    ## 5 __mu… CRUK… CRUK0070  CBLB      TRUE      FALSE     2                  1
    ## 6 __mu… Anno… CRUK0070  NFE2L2    TRUE      FALSE     3                  1
    ## # … with 6 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R4 <dbl>,
    ## #   R6 <dbl>, R7 <dbl>
    ## 
    ## $dataset$CRUK0071
    ## # A tibble: 4 x 15
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0071  CMTR2     TRUE      TRUE      1                  3
    ## 2 __mu… Anno… CRUK0071  PIK3CA    TRUE      TRUE      1                  3
    ## 3 __mu… Anno… CRUK0071  SOX2      TRUE      TRUE      1                  3
    ## 4 __mu… CRUK… CRUK0071  UBR5      TRUE      FALSE     4                  1
    ## # … with 7 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R5 <dbl>, R6 <dbl>, R7 <dbl>
    ## 
    ## $dataset$CRUK0072
    ## # A tibble: 6 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0072  TP53      TRUE      TRUE      1                  6
    ## 2 __mu… CRUK… CRUK0072  NFE2L2    TRUE      TRUE      1                  6
    ## 3 __mu… Anno… CRUK0072  PIK3CA    TRUE      TRUE      1                  6
    ## 4 __mu… Anno… CRUK0072  SOX2      TRUE      TRUE      1                  6
    ## 5 __mu… Anno… CRUK0072  EGFR      TRUE      TRUE      1                  6
    ## 6 __mu… Anno… CRUK0072  MYC       TRUE      TRUE      1                  6
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R4 <dbl>
    ## 
    ## $dataset$CRUK0073
    ## # A tibble: 9 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0073  CDKN2A    TRUE      TRUE      1                  8
    ## 2 __mu… CRUK… CRUK0073  DICER1    TRUE      TRUE      1                  8
    ## 3 __mu… CRUK… CRUK0073  NFE2L2    TRUE      TRUE      1                  8
    ## 4 __mu… CRUK… CRUK0073  FAT1      TRUE      TRUE      1                  8
    ## 5 __mu… CRUK… CRUK0073  KMT2D     TRUE      TRUE      1                  8
    ## 6 __mu… CRUK… CRUK0073  NOTCH2    TRUE      TRUE      1                  8
    ## 7 __mu… Anno… CRUK0073  FGFR1     TRUE      TRUE      1                  8
    ## 8 __mu… Anno… CRUK0073  MYC       TRUE      TRUE      1                  8
    ## 9 __mu… CRUK… CRUK0073  PLXNB2    TRUE      FALSE     2                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0074
    ## # A tibble: 6 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0074  TP53      TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0074  NFE2L2    TRUE      TRUE      1                  5
    ## 3 __mu… Anno… CRUK0074  PIK3CA    TRUE      TRUE      1                  5
    ## 4 __mu… Anno… CRUK0074  SOX2      TRUE      TRUE      1                  5
    ## 5 __mu… Anno… CRUK0074  CCND1     TRUE      TRUE      1                  5
    ## 6 __mu… CRUK… CRUK0074  UBR5      TRUE      FALSE     3                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0075
    ## # A tibble: 8 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0075  NOTCH1    TRUE      TRUE      1                  7
    ## 2 __mu… CRUK… CRUK0075  RASA1     TRUE      TRUE      1                  7
    ## 3 __mu… CRUK… CRUK0075  TP53      TRUE      TRUE      1                  7
    ## 4 __mu… CRUK… CRUK0075  FAT1      TRUE      TRUE      1                  7
    ## 5 __mu… CRUK… CRUK0075  MGA       TRUE      TRUE      1                  7
    ## 6 __mu… CRUK… CRUK0075  PIK3CA    TRUE      TRUE      1                  7
    ## 7 __mu… Anno… CRUK0075  FGFR1     TRUE      TRUE      1                  7
    ## 8 __mu… CRUK… CRUK0075  NFE2L2    TRUE      FALSE     2                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0076
    ## # A tibble: 8 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0076  SERPINB13 TRUE      TRUE      1                  6
    ## 2 __mu… CRUK… CRUK0076  TP53      TRUE      TRUE      1                  6
    ## 3 __mu… CRUK… CRUK0076  ARID1B    TRUE      TRUE      1                  6
    ## 4 __mu… Anno… CRUK0076  PIK3CA    TRUE      TRUE      1                  6
    ## 5 __mu… Anno… CRUK0076  SOX2      TRUE      TRUE      1                  6
    ## 6 __mu… Anno… CRUK0076  FGFR1     TRUE      TRUE      1                  6
    ## 7 __mu… CRUK… CRUK0076  NCOR1     TRUE      FALSE     2                  1
    ## 8 __mu… CRUK… CRUK0076  COL5A2    TRUE      FALSE     3                  1
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0077
    ## # A tibble: 3 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0077  TP53      TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0077  LATS1     TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0077  KEAP1     TRUE      TRUE      1                  3
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0078
    ## # A tibble: 5 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0078  PLXNB2    TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0078  PTEN      TRUE      TRUE      1                  5
    ## 3 __mu… Anno… CRUK0078  PIK3CA    TRUE      TRUE      1                  5
    ## 4 __mu… Anno… CRUK0078  SOX2      TRUE      TRUE      1                  5
    ## 5 __mu… Anno… CRUK0078  FGFR1     TRUE      TRUE      1                  5
    ## # … with 4 more variables: CCF <chr>, R2 <dbl>, R3 <dbl>, R4 <dbl>
    ## 
    ## $dataset$CRUK0079
    ## # A tibble: 6 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0079  FAT1      TRUE      TRUE      1                  6
    ## 2 __mu… CRUK… CRUK0079  TP53      TRUE      TRUE      1                  6
    ## 3 __mu… CRUK… CRUK0079  POLE      TRUE      TRUE      1                  6
    ## 4 __mu… Anno… CRUK0079  PIK3CA    TRUE      TRUE      1                  6
    ## 5 __mu… Anno… CRUK0079  SOX2      TRUE      TRUE      1                  6
    ## 6 __mu… Anno… CRUK0079  FGFR1     TRUE      TRUE      1                  6
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0080
    ## # A tibble: 5 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0080  TP53      TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0080  WT1       TRUE      TRUE      1                  4
    ## 3 __mu… Anno… CRUK0080  EGFR      TRUE      TRUE      1                  4
    ## 4 __mu… Anno… CRUK0080  CCND1     TRUE      TRUE      1                  4
    ## 5 __mu… CRUK… CRUK0080  IKZF1     TRUE      FALSE     3                  1
    ## # … with 5 more variables: CCF <chr>, R3 <dbl>, R4 <dbl>, R5 <dbl>,
    ## #   R6 <dbl>
    ## 
    ## $dataset$CRUK0081
    ## # A tibble: 6 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0081  NOTCH1    TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0081  TP53      TRUE      TRUE      1                  5
    ## 3 __mu… CRUK… CRUK0081  CDKN2A    TRUE      TRUE      1                  5
    ## 4 __mu… CRUK… CRUK0081  FAT1      TRUE      TRUE      1                  5
    ## 5 __mu… CRUK… CRUK0081  FANCC     TRUE      TRUE      1                  5
    ## 6 __mu… CRUK… CRUK0081  CYLD      TRUE      FALSE     3                  1
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R5 <dbl>
    ## 
    ## $dataset$CRUK0082
    ## # A tibble: 8 x 14
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0082  TP53      TRUE      TRUE      1                  8
    ## 2 __mu… CRUK… CRUK0082  WT1       TRUE      TRUE      1                  8
    ## 3 __mu… CRUK… CRUK0082  PTEN      TRUE      TRUE      1                  8
    ## 4 __mu… CRUK… CRUK0082  COL5A2    TRUE      TRUE      1                  8
    ## 5 __mu… CRUK… CRUK0082  KMT2D     TRUE      TRUE      1                  8
    ## 6 __mu… Anno… CRUK0082  PIK3CA    TRUE      TRUE      1                  8
    ## 7 __mu… Anno… CRUK0082  SOX2      TRUE      TRUE      1                  8
    ## 8 __mu… Anno… CRUK0082  FGFR1     TRUE      TRUE      1                  8
    ## # … with 6 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>, R5 <dbl>
    ## 
    ## $dataset$CRUK0083
    ## # A tibble: 7 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0083  TP53      TRUE      TRUE      1                  7
    ## 2 __mu… CRUK… CRUK0083  FBXW7     TRUE      TRUE      1                  7
    ## 3 __mu… CRUK… CRUK0083  RASA1     TRUE      TRUE      1                  7
    ## 4 __mu… Anno… CRUK0083  PIK3CA    TRUE      TRUE      1                  7
    ## 5 __mu… Anno… CRUK0083  SOX2      TRUE      TRUE      1                  7
    ## 6 __mu… Anno… CRUK0083  FGFR1     TRUE      TRUE      1                  7
    ## 7 __mu… Anno… CRUK0083  MYC       TRUE      TRUE      1                  7
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0084
    ## # A tibble: 1 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0084  CREBBP    TRUE      TRUE      1                  1
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0085
    ## # A tibble: 4 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0085  CHEK2     TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0085  CREBBP    TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0085  LATS1     TRUE      TRUE      1                  4
    ## 4 __mu… CRUK… CRUK0085  FANCM     TRUE      TRUE      1                  4
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0086
    ## # A tibble: 3 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0086  TP53      TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0086  ARID2     TRUE      TRUE      1                  3
    ## 3 __mu… Anno… CRUK0086  FAT1      TRUE      TRUE      1                  3
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R4 <dbl>
    ## 
    ## $dataset$CRUK0087
    ## # A tibble: 4 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0087  NFE2L2    TRUE      TRUE      1                  4
    ## 2 __mu… CRUK… CRUK0087  TP53      TRUE      TRUE      1                  4
    ## 3 __mu… CRUK… CRUK0087  ASXL1     TRUE      TRUE      1                  4
    ## 4 __mu… CRUK… CRUK0087  PIK3CA    TRUE      TRUE      1                  4
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0088
    ## # A tibble: 2 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0088  CUX1      TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0088  TP53      TRUE      TRUE      1                  2
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0089
    ## # A tibble: 3 x 10
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0089  PIK3CA    TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0089  SMAD4     TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0089  KEAP1     TRUE      TRUE      1                  3
    ## # … with 2 more variables: CCF <chr>, R2 <dbl>
    ## 
    ## $dataset$CRUK0090
    ## # A tibble: 5 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0090  CDKN2A    TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0090  NCOA6     TRUE      TRUE      1                  5
    ## 3 __mu… CRUK… CRUK0090  CUX1      TRUE      TRUE      1                  5
    ## 4 __mu… CRUK… CRUK0090  COL2A1    TRUE      TRUE      1                  5
    ## 5 __mu… CRUK… CRUK0090  NRAS      TRUE      TRUE      1                  5
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0091
    ## # A tibble: 3 x 10
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0091  TP53      TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0091  SMARCA4   TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0091  CDKN2A    TRUE      TRUE      1                  3
    ## # … with 2 more variables: CCF <chr>, R2 <dbl>
    ## 
    ## $dataset$CRUK0092
    ## # A tibble: 5 x 10
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0092  TP53      TRUE      TRUE      1                  5
    ## 2 __mu… CRUK… CRUK0092  SMAD4     TRUE      TRUE      1                  5
    ## 3 __mu… CRUK… CRUK0092  RASA1     TRUE      TRUE      1                  5
    ## 4 __mu… CRUK… CRUK0092  CBLB      TRUE      TRUE      1                  5
    ## 5 __mu… CRUK… CRUK0092  PIK3CA    TRUE      TRUE      1                  5
    ## # … with 2 more variables: CCF <chr>, R1 <dbl>
    ## 
    ## $dataset$CRUK0093
    ## # A tibble: 7 x 10
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0093  DICER1    TRUE      TRUE      1                  7
    ## 2 __mu… CRUK… CRUK0093  CDKN2A    TRUE      TRUE      1                  7
    ## 3 __mu… CRUK… CRUK0093  COL2A1    TRUE      TRUE      1                  7
    ## 4 __mu… CRUK… CRUK0093  GATA3     TRUE      TRUE      1                  7
    ## 5 __mu… CRUK… CRUK0093  CIC       TRUE      TRUE      1                  7
    ## 6 __mu… CRUK… CRUK0093  COL5A2    TRUE      TRUE      1                  7
    ## 7 __mu… CRUK… CRUK0093  TP53      TRUE      TRUE      1                  7
    ## # … with 2 more variables: CCF <chr>, R1 <dbl>
    ## 
    ## $dataset$CRUK0094
    ## # A tibble: 2 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0094  SMARCA4   TRUE      TRUE      1                  2
    ## 2 __mu… Anno… CRUK0094  TERT      TRUE      TRUE      1                  2
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>
    ## 
    ## $dataset$CRUK0095
    ## # A tibble: 3 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0095  TP53      TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0095  NF1       TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0095  RASA1     TRUE      TRUE      1                  3
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0096
    ## # A tibble: 3 x 16
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0096  KRAS      TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0096  SGK223    TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0096  MAP3K1    TRUE      TRUE      1                  3
    ## # … with 8 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>,
    ## #   R4 <dbl>, R5 <dbl>, R6 <dbl>, R7 <dbl>
    ## 
    ## $dataset$CRUK0097
    ## # A tibble: 2 x 11
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0097  TP53      TRUE      TRUE      1                  2
    ## 2 __mu… CRUK… CRUK0097  PTEN      TRUE      TRUE      1                  2
    ## # … with 3 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>
    ## 
    ## $dataset$CRUK0098
    ## # A tibble: 3 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0098  TP53      TRUE      TRUE      1                  2
    ## 2 __mu… Anno… CRUK0098  PTEN      TRUE      TRUE      1                  2
    ## 3 __mu… CRUK… CRUK0098  UBR5      TRUE      FALSE     3                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## $dataset$CRUK0099
    ## # A tibble: 3 x 13
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0099  STK11     TRUE      TRUE      1                  3
    ## 2 __mu… CRUK… CRUK0099  KEAP1     TRUE      TRUE      1                  3
    ## 3 __mu… CRUK… CRUK0099  TP53      TRUE      TRUE      1                  3
    ## # … with 5 more variables: CCF <chr>, R1 <dbl>, R3 <dbl>, R6 <dbl>,
    ## #   R7 <dbl>
    ## 
    ## $dataset$CRUK0100
    ## # A tibble: 6 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0100  TP53      TRUE      TRUE      1                  6
    ## 2 __mu… CRUK… CRUK0100  PHOX2B    TRUE      TRUE      1                  6
    ## 3 __mu… CRUK… CRUK0100  COL5A2    TRUE      TRUE      1                  6
    ## 4 __mu… CRUK… CRUK0100  STK11     TRUE      TRUE      1                  6
    ## 5 __mu… CRUK… CRUK0100  SPEN      TRUE      TRUE      1                  6
    ## 6 __mu… Anno… CRUK0100  CDKN2A    TRUE      TRUE      1                  6
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>
    ## 
    ## 
    ## $CCF
    ## $CCF$CRUK0001
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 3           4 TRUE      TRUE       0.99  0.99  1   
    ## 2 1           1 TRUE      FALSE      0.86  0     0   
    ## 3 2           1 TRUE      FALSE      0.19  0     0.95
    ## 4 5           1 TRUE      FALSE      0.82  0     0.71
    ## 
    ## $CCF$CRUK0002
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      FALSE      0     0.92  0   
    ## 2 2           2 TRUE      TRUE       0.99  0.98  0.99
    ## 3 5           1 TRUE      FALSE      0.78  0     0   
    ## 4 6           1 TRUE      FALSE      0.96  0.03  0.98
    ## 
    ## $CCF$CRUK0003
    ## # A tibble: 2 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.97  0.87  0.97  0.99
    ## 2 4           1 TRUE      FALSE      0     0     0.49  0     0.01
    ## 
    ## $CCF$CRUK0004
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      FALSE      0    0      0.95  0.01
    ## 2 2           2 TRUE      TRUE       0.99 0.985  0.99  0.98
    ## 
    ## $CCF$CRUK0005
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 2           5 TRUE      TRUE          1     1  0.97     1
    ## 2 1           1 TRUE      FALSE         0     0  0.8      0
    ## 
    ## $CCF$CRUK0006
    ## # A tibble: 3 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1   
    ## 2 2           1 TRUE      FALSE      0     0.93
    ## 3 7           1 TRUE      FALSE      0.99  0.06
    ## 
    ## $CCF$CRUK0007
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.93
    ## 
    ## $CCF$CRUK0008
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 2           5 TRUE      TRUE       0.99     1
    ## 2 3           1 TRUE      FALSE      0.86     0
    ## 
    ## $CCF$CRUK0009
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99  0.98  0.99
    ## 2 2           1 TRUE      FALSE      0     0.93  0     0.96
    ## 
    ## $CCF$CRUK0010
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.95  0.98
    ## 
    ## $CCF$CRUK0011
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.97     1
    ## 2 3           1 TRUE      FALSE      0.95  0        0
    ## 
    ## $CCF$CRUK0012
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.98  0.95
    ## 
    ## $CCF$CRUK0013
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal   LN1   LN2    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99  0.99 0.99   0.99
    ## 2 2           1 TRUE      FALSE      0     0     0    0.75   0   
    ## 3 3           1 TRUE      FALSE      0.97  0.96  0.01 0.580  0.94
    ## 4 4           1 TRUE      FALSE      0     0     0.97 0.37   0.01
    ## 
    ## $CCF$CRUK0014
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.96  0.96
    ## 2 2           1 TRUE      FALSE      0.35  0.01
    ## 
    ## $CCF$CRUK0015
    ## # A tibble: 3 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.99
    ## 2 2           1 TRUE      FALSE      0.94  0.01
    ## 3 3           1 TRUE      FALSE      0.01  0.65
    ## 
    ## $CCF$CRUK0016
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## $CCF$CRUK0017
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1  1     1     1   
    ## 2 3           1 TRUE      FALSE         0  0.94  0.95  0.59
    ## 
    ## $CCF$CRUK0018
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1     1
    ## 
    ## $CCF$CRUK0019
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.97  0.96
    ## 
    ## $CCF$CRUK0020
    ## # A tibble: 4 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       1     1   
    ## 2 2           1 TRUE      FALSE      0.87  0   
    ## 3 3           1 TRUE      FALSE      0.9   0.08
    ## 4 4           1 TRUE      FALSE      0     0.85
    ## 
    ## $CCF$CRUK0021
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99
    ## 
    ## $CCF$CRUK0022
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.99
    ## 2 2           1 TRUE      FALSE      0.85  0   
    ## 
    ## $CCF$CRUK0023
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99 0.98   0.99  0.95
    ## 2 4           2 TRUE      FALSE      0.01 0.945  0     0   
    ## 3 2           1 TRUE      FALSE      0.81 0      0     0   
    ## 
    ## $CCF$CRUK0024
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R3    R4    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1        1
    ## 2 3           1 TRUE      FALSE      0.88  0.97  0.95     0
    ## 3 4           1 TRUE      FALSE      0.83  0     0        0
    ## 
    ## $CCF$CRUK0025
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1
    ## 
    ## $CCF$CRUK0026
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.98  0.98
    ## 
    ## $CCF$CRUK0027
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.96  1   
    ## 2 2           1 TRUE      FALSE      0     0.99
    ## 
    ## $CCF$CRUK0028
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE      0.975  0.95
    ## 
    ## $CCF$CRUK0029
    ## # A tibble: 1 x 10
    ##   cluster nMuts is.driver is.clonal    R2    R4    R5    R6    R7    R8
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99  0.98     1     1     1
    ## 
    ## $CCF$CRUK0030
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.98  0.98
    ## 
    ## $CCF$CRUK0031
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1        1
    ## 2 6           1 TRUE      FALSE      0.88  0.05     0
    ## 
    ## $CCF$CRUK0032
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  1        1  1   
    ## 2 4           1 TRUE      FALSE         0  0.97     0  0.98
    ## 3 6           1 TRUE      FALSE         0  0        0  0.3 
    ## 
    ## $CCF$CRUK0033
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.98
    ## 
    ## $CCF$CRUK0034
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1   1       1
    ## 2 4           1 TRUE      FALSE         0   0.5     0
    ## 
    ## $CCF$CRUK0035
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal   LN1    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.98  0.99  0.99
    ## 2 4           1 TRUE      FALSE      0     0.8   0     0.01
    ## 
    ## $CCF$CRUK0036
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  0.98  0.97     1
    ## 
    ## $CCF$CRUK0037
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99     1     1     1     1
    ## 
    ## $CCF$CRUK0038
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99
    ## 2 3           1 TRUE      FALSE      0     0.38
    ## 
    ## $CCF$CRUK0039
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1  0.98
    ## 
    ## $CCF$CRUK0040
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.99  0.99
    ## 
    ## $CCF$CRUK0041
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.99  0.99  0.99
    ## 
    ## $CCF$CRUK0042
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           1 TRUE      TRUE       0.91
    ## 
    ## $CCF$CRUK0043
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.98
    ## 
    ## $CCF$CRUK0044
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE          1     1
    ## 
    ## $CCF$CRUK0045
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.98  0.98
    ## 
    ## $CCF$CRUK0046
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1  0.98 0.995  0.96
    ## 
    ## $CCF$CRUK0047
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.99     1
    ## 
    ## $CCF$CRUK0048
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE          1     1     1
    ## 
    ## $CCF$CRUK0049
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## $CCF$CRUK0050
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99  0.99  0.99     1  0.99
    ## 
    ## $CCF$CRUK0051
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1        1     1
    ## 2 3           1 TRUE      FALSE      0.97     0     0
    ## 
    ## $CCF$CRUK0052
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1     1  1   
    ## 2 2           1 TRUE      FALSE         0     0  0.86
    ## 
    ## $CCF$CRUK0054
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99
    ## 
    ## $CCF$CRUK0055
    ## # A tibble: 2 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           2 TRUE      TRUE       1   
    ## 2 2           1 TRUE      FALSE      0.32
    ## 
    ## $CCF$CRUK0056
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1  1     1   
    ## 2 3           1 TRUE      FALSE         0  0.12  0.98
    ## 
    ## $CCF$CRUK0057
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## $CCF$CRUK0058
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.99
    ## 
    ## $CCF$CRUK0059
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.98
    ## 
    ## $CCF$CRUK0060
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1          11 TRUE      TRUE          1
    ## 
    ## $CCF$CRUK0061
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99     1
    ## 
    ## $CCF$CRUK0062
    ## # A tibble: 4 x 11
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 4           4 TRUE      TRUE       0.99  0.99  0.98  0.97  0.99  0.99
    ## 2 1           1 TRUE      FALSE      0     0.01  0     0     0     0.94
    ## 3 16          1 TRUE      FALSE      0.93  0.86  0.08  0.02  0.12  0   
    ## 4 2           1 TRUE      FALSE      0.84  0.83  0.02  0     0     0   
    ## # … with 1 more variable: R7 <dbl>
    ## 
    ## $CCF$CRUK0063
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 2           7 TRUE      TRUE       0.93  0.99  0.99  0.99  1   
    ## 2 1           2 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 3 10          1 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 4 6           1 TRUE      FALSE      0     0.02  0.7   0.36  0.55
    ## 
    ## $CCF$CRUK0064
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 2           2 TRUE      FALSE      0.64  0.11
    ## 2 1           1 TRUE      TRUE       1     1   
    ## 
    ## $CCF$CRUK0065
    ## # A tibble: 3 x 10
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99  0.99     1  1     1   
    ## 2 2           3 TRUE      FALSE         0  0     0        0  0.48  0   
    ## 3 6           2 TRUE      FALSE         0  0     0        0  0.01  0.83
    ## 
    ## $CCF$CRUK0066
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       0.99  1     1     0.99
    ## 2 9           1 TRUE      FALSE      0     0.91  0.01  0   
    ## 
    ## $CCF$CRUK0067
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1   
    ## 2 2           1 TRUE      FALSE      0.61  0.83
    ## 
    ## $CCF$CRUK0068
    ## # A tibble: 4 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1     1     1   
    ## 2 3           1 TRUE      FALSE      0.5   0     0     0   
    ## 3 4           1 TRUE      FALSE      0.98  0.37  0.99  0.01
    ## 4 9           1 TRUE      FALSE      0     0     0     0.69
    ## 
    ## $CCF$CRUK0069
    ## # A tibble: 2 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1     1     1   
    ## 2 13          1 TRUE      FALSE      0.93  0.42  0.32  0.94  0.96
    ## 
    ## $CCF$CRUK0070
    ## # A tibble: 3 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1     1     1   
    ## 2 2           1 TRUE      FALSE      0     0     0     0.95  0.98
    ## 3 3           1 TRUE      FALSE      0.95  0.96  0.98  0     0.01
    ## 
    ## $CCF$CRUK0071
    ## # A tibble: 2 x 10
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1 0.99      1     1     1     1
    ## 2 4           1 TRUE      FALSE         0 0.570     0     0     0     0
    ## 
    ## $CCF$CRUK0072
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.99  0.99
    ## 
    ## $CCF$CRUK0073
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1  1   
    ## 2 2           1 TRUE      FALSE         0  0.93
    ## 
    ## $CCF$CRUK0074
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1   
    ## 2 3           1 TRUE      FALSE      0     0.99
    ## 
    ## $CCF$CRUK0075
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       1     0.99
    ## 2 2           1 TRUE      FALSE      0.15  0.98
    ## 
    ## $CCF$CRUK0076
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       1        1  1        1
    ## 2 2           1 TRUE      FALSE      0.93     0  0.28     0
    ## 3 3           1 TRUE      FALSE      0.93     0  0.81     0
    ## 
    ## $CCF$CRUK0077
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1     1
    ## 
    ## $CCF$CRUK0078
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1     1
    ## 
    ## $CCF$CRUK0079
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.99     1     1
    ## 
    ## $CCF$CRUK0080
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1  1     1   
    ## 2 3           1 TRUE      FALSE         0     0  0.97  0.83
    ## 
    ## $CCF$CRUK0081
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       1     0.99
    ## 2 3           1 TRUE      FALSE      0.93  0.01
    ## 
    ## $CCF$CRUK0082
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1     1     1     1     1
    ## 
    ## $CCF$CRUK0083
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE          1     1     1  0.99
    ## 
    ## $CCF$CRUK0084
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE          1     1     1     1
    ## 
    ## $CCF$CRUK0085
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1     1
    ## 
    ## $CCF$CRUK0086
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1
    ## 
    ## $CCF$CRUK0087
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1
    ## 
    ## $CCF$CRUK0088
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1     1
    ## 
    ## $CCF$CRUK0089
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           3 TRUE      TRUE       0.99
    ## 
    ## $CCF$CRUK0090
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## $CCF$CRUK0091
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           3 TRUE      TRUE          1
    ## 
    ## $CCF$CRUK0092
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           5 TRUE      TRUE          1
    ## 
    ## $CCF$CRUK0093
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           7 TRUE      TRUE       0.96
    ## 
    ## $CCF$CRUK0094
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.98  0.97  0.99
    ## 
    ## $CCF$CRUK0095
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99  0.99  0.98
    ## 
    ## $CCF$CRUK0096
    ## # A tibble: 1 x 11
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1     1     1     1
    ## # … with 1 more variable: R7 <dbl>
    ## 
    ## $CCF$CRUK0097
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE      0.995  0.98
    ## 
    ## $CCF$CRUK0098
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       1     1        1
    ## 2 3           1 TRUE      FALSE      0.96  0.91     0
    ## 
    ## $CCF$CRUK0099
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R3    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.95  0.97  0.91     1
    ## 
    ## $CCF$CRUK0100
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1     1     1
    ## 
    ## 
    ## $n
    ## $n$patients
    ## [1] 99
    ## 
    ## $n$variants
    ## [1] 450
    ## 
    ## $n$drivers
    ## [1] 79
    ## 
    ## 
    ## $CCF_parser
    ## <srcref: file "/Users/gcaravagna/Documents/Github/revolver/R/CCF_parser.R" chars 25:14 to 36:1>
    ## <bytecode: 0x7f868f5a9d78>
    ## <environment: namespace:revolver>
    ## 
    ## $phylogenies
    ## $phylogenies$CRUK0001
    ## $phylogenies$CRUK0001$`1`
    ##  [ ctree - ctree rank 1/3 for CRUK0001 ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 3           4 TRUE      TRUE       0.99  0.99  1   
    ## 2 1           1 TRUE      FALSE      0.86  0     0   
    ## 3 2           1 TRUE      FALSE      0.19  0     0.95
    ## 4 5           1 TRUE      FALSE      0.82  0     0.71
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-3 [R2] :: TP53, MGA, WRN, EGFR
    ##     |-1 :: NF1
    ##     | \-5 :: PASK
    ##     \-2 :: ARHGAP35
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> MGA 
    ##    GL ---> WRN 
    ##    GL ---> EGFR 
    ##    TP53 ---> NF1 
    ##    MGA ---> NF1 
    ##    WRN ---> NF1 
    ##    EGFR ---> NF1 
    ##    TP53 ---> ARHGAP35 
    ##    MGA ---> ARHGAP35 
    ##    WRN ---> ARHGAP35 
    ##    EGFR ---> ARHGAP35 
    ##    NF1 ---> PASK 
    ## 
    ## Tree score 0.111111111111111 
    ## 
    ## $phylogenies$CRUK0001$`2`
    ##  [ ctree - ctree rank 2/3 for CRUK0001 ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 3           4 TRUE      TRUE       0.99  0.99  1   
    ## 2 1           1 TRUE      FALSE      0.86  0     0   
    ## 3 2           1 TRUE      FALSE      0.19  0     0.95
    ## 4 5           1 TRUE      FALSE      0.82  0     0.71
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-3 [R2] :: TP53, MGA, WRN, EGFR
    ##     |-2 :: ARHGAP35
    ##     | \-5 :: PASK
    ##     \-1 :: NF1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> MGA 
    ##    GL ---> WRN 
    ##    GL ---> EGFR 
    ##    TP53 ---> NF1 
    ##    MGA ---> NF1 
    ##    WRN ---> NF1 
    ##    EGFR ---> NF1 
    ##    TP53 ---> ARHGAP35 
    ##    MGA ---> ARHGAP35 
    ##    WRN ---> ARHGAP35 
    ##    EGFR ---> ARHGAP35 
    ##    ARHGAP35 ---> PASK 
    ## 
    ## Tree score 0.111111111111111 
    ## 
    ## $phylogenies$CRUK0001$`3`
    ##  [ ctree - ctree rank 3/3 for CRUK0001 ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 3           4 TRUE      TRUE       0.99  0.99  1   
    ## 2 1           1 TRUE      FALSE      0.86  0     0   
    ## 3 2           1 TRUE      FALSE      0.19  0     0.95
    ## 4 5           1 TRUE      FALSE      0.82  0     0.71
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-3 [R2] :: TP53, MGA, WRN, EGFR
    ##     \-1 :: NF1
    ##      \-5 :: PASK
    ##       \-2 :: ARHGAP35
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> MGA 
    ##    GL ---> WRN 
    ##    GL ---> EGFR 
    ##    TP53 ---> NF1 
    ##    MGA ---> NF1 
    ##    WRN ---> NF1 
    ##    EGFR ---> NF1 
    ##    PASK ---> ARHGAP35 
    ##    NF1 ---> PASK 
    ## 
    ## Tree score 0.111111111111111 
    ## 
    ## 
    ## $phylogenies$CRUK0002
    ## $phylogenies$CRUK0002$`1`
    ##  [ ctree - ctree rank 1/2 for CRUK0002 ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      FALSE      0     0.92  0   
    ## 2 2           2 TRUE      TRUE       0.99  0.98  0.99
    ## 3 5           1 TRUE      FALSE      0.78  0     0   
    ## 4 6           1 TRUE      FALSE      0.96  0.03  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 :: MET, TERT
    ##     |-6 :: EP300
    ##     | \-5 :: NF1
    ##     \-1 :: RB1, IKZF1, KRAS
    ## 
    ## Information transfer  
    ## 
    ##    MET ---> RB1 
    ##    MET ---> IKZF1 
    ##    MET ---> KRAS 
    ##    TERT ---> RB1 
    ##    TERT ---> IKZF1 
    ##    TERT ---> KRAS 
    ##    GL ---> MET 
    ##    GL ---> TERT 
    ##    EP300 ---> NF1 
    ##    MET ---> EP300 
    ##    TERT ---> EP300 
    ## 
    ## Tree score 0.75 
    ## 
    ## $phylogenies$CRUK0002$`2`
    ##  [ ctree - ctree rank 2/2 for CRUK0002 ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      FALSE      0     0.92  0   
    ## 2 2           2 TRUE      TRUE       0.99  0.98  0.99
    ## 3 5           1 TRUE      FALSE      0.78  0     0   
    ## 4 6           1 TRUE      FALSE      0.96  0.03  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 :: MET, TERT
    ##     \-1 :: RB1, IKZF1, KRAS
    ##      \-6 :: EP300
    ##       \-5 :: NF1
    ## 
    ## Information transfer  
    ## 
    ##    MET ---> RB1 
    ##    MET ---> IKZF1 
    ##    MET ---> KRAS 
    ##    TERT ---> RB1 
    ##    TERT ---> IKZF1 
    ##    TERT ---> KRAS 
    ##    GL ---> MET 
    ##    GL ---> TERT 
    ##    EP300 ---> NF1 
    ##    RB1 ---> EP300 
    ##    IKZF1 ---> EP300 
    ##    KRAS ---> EP300 
    ## 
    ## Tree score 0.0833333333333333 
    ## 
    ## 
    ## $phylogenies$CRUK0003
    ## $phylogenies$CRUK0003$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0003 ] 
    ## 
    ## # A tibble: 2 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.97  0.87  0.97  0.99
    ## 2 4           1 TRUE      FALSE      0     0     0.49  0     0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R4] :: PIK3CA, EGFR, CDKN2A
    ##     \-4 :: CTNNB1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> EGFR 
    ##    GL ---> CDKN2A 
    ##    PIK3CA ---> CTNNB1 
    ##    EGFR ---> CTNNB1 
    ##    CDKN2A ---> CTNNB1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0004
    ## $phylogenies$CRUK0004$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0004 ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      FALSE      0    0      0.95  0.01
    ## 2 2           2 TRUE      TRUE       0.99 0.985  0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R1, R2] :: TP53, EGFR
    ##     \-1 :: SMAD4, NOTCH1
    ## 
    ## Information transfer  
    ## 
    ##    TP53 ---> SMAD4 
    ##    TP53 ---> NOTCH1 
    ##    EGFR ---> SMAD4 
    ##    EGFR ---> NOTCH1 
    ##    GL ---> TP53 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0005
    ## $phylogenies$CRUK0005$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0005 ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 2           5 TRUE      TRUE          1     1  0.97     1
    ## 2 1           1 TRUE      FALSE         0     0  0.8      0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R1, R2, R4] :: CMTR2, TP53, BRAF, PASK, TERT
    ##     \-1 :: NRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CMTR2 
    ##    GL ---> TP53 
    ##    GL ---> BRAF 
    ##    GL ---> PASK 
    ##    GL ---> TERT 
    ##    CMTR2 ---> NRAS 
    ##    TP53 ---> NRAS 
    ##    BRAF ---> NRAS 
    ##    PASK ---> NRAS 
    ##    TERT ---> NRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0006
    ## $phylogenies$CRUK0006$`1`
    ##  [ ctree - ctree rank 1/2 for CRUK0006 ] 
    ## 
    ## # A tibble: 3 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1   
    ## 2 2           1 TRUE      FALSE      0     0.93
    ## 3 7           1 TRUE      FALSE      0.99  0.06
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: PLXNB2, TP53, KEAP1, TERT
    ##     |-7 :: FANCC
    ##     \-2 :: MAP3K1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PLXNB2 
    ##    GL ---> TP53 
    ##    GL ---> KEAP1 
    ##    GL ---> TERT 
    ##    PLXNB2 ---> MAP3K1 
    ##    TP53 ---> MAP3K1 
    ##    KEAP1 ---> MAP3K1 
    ##    TERT ---> MAP3K1 
    ##    PLXNB2 ---> FANCC 
    ##    TP53 ---> FANCC 
    ##    KEAP1 ---> FANCC 
    ##    TERT ---> FANCC 
    ## 
    ## Tree score 0.666666666666667 
    ## 
    ## $phylogenies$CRUK0006$`2`
    ##  [ ctree - ctree rank 2/2 for CRUK0006 ] 
    ## 
    ## # A tibble: 3 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1   
    ## 2 2           1 TRUE      FALSE      0     0.93
    ## 3 7           1 TRUE      FALSE      0.99  0.06
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: PLXNB2, TP53, KEAP1, TERT
    ##     \-2 :: MAP3K1
    ##      \-7 :: FANCC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PLXNB2 
    ##    GL ---> TP53 
    ##    GL ---> KEAP1 
    ##    GL ---> TERT 
    ##    PLXNB2 ---> MAP3K1 
    ##    TP53 ---> MAP3K1 
    ##    KEAP1 ---> MAP3K1 
    ##    TERT ---> MAP3K1 
    ##    MAP3K1 ---> FANCC 
    ## 
    ## Tree score 0.166666666666667 
    ## 
    ## 
    ## $phylogenies$CRUK0007
    ## $phylogenies$CRUK0007$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0007 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.93
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: PIK3CA, EGFR, SGK223
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> EGFR 
    ##    GL ---> SGK223 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0008
    ## $phylogenies$CRUK0008$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0008 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 2           5 TRUE      TRUE       0.99     1
    ## 2 3           1 TRUE      FALSE      0.86     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R2] :: KEAP1, STK11, PRDM1, U2AF1, MYC
    ##     \-3 :: ARID2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> STK11 
    ##    GL ---> PRDM1 
    ##    GL ---> U2AF1 
    ##    GL ---> MYC 
    ##    KEAP1 ---> ARID2 
    ##    STK11 ---> ARID2 
    ##    PRDM1 ---> ARID2 
    ##    U2AF1 ---> ARID2 
    ##    MYC ---> ARID2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0009
    ## $phylogenies$CRUK0009$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0009 ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99  0.98  0.99
    ## 2 2           1 TRUE      FALSE      0     0.93  0     0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: BRAF, TP53, ARHGAP35, KMT2C, NFE2L2, MET
    ##     \-2 :: TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> BRAF 
    ##    GL ---> TP53 
    ##    GL ---> ARHGAP35 
    ##    GL ---> KMT2C 
    ##    GL ---> NFE2L2 
    ##    GL ---> MET 
    ##    BRAF ---> TERT 
    ##    TP53 ---> TERT 
    ##    ARHGAP35 ---> TERT 
    ##    KMT2C ---> TERT 
    ##    NFE2L2 ---> TERT 
    ##    MET ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0010
    ## $phylogenies$CRUK0010$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0010 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.95  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: SETD2, EGFR, TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SETD2 
    ##    GL ---> EGFR 
    ##    GL ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0011
    ## $phylogenies$CRUK0011$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0011 ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.97     1
    ## 2 3           1 TRUE      FALSE      0.95  0        0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R3] :: KRAS
    ##     \-3 :: FLT4
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    KRAS ---> FLT4 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0012
    ## $phylogenies$CRUK0012$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0012 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.98  0.95
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0013
    ## $phylogenies$CRUK0013$`1`
    ##  [ ctree - ctree rank 1/4 for CRUK0013 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal   LN1   LN2    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99  0.99 0.99   0.99
    ## 2 2           1 TRUE      FALSE      0     0     0    0.75   0   
    ## 3 3           1 TRUE      FALSE      0.97  0.96  0.01 0.580  0.94
    ## 4 4           1 TRUE      FALSE      0     0     0.97 0.37   0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: STK11
    ##     |-3 :: KRAS
    ##     |-4 :: EGFR
    ##     \-2 :: NOTCH1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    STK11 ---> NOTCH1 
    ##    STK11 ---> KRAS 
    ##    STK11 ---> EGFR 
    ## 
    ## Tree score 0.3 
    ## 
    ## $phylogenies$CRUK0013$`2`
    ##  [ ctree - ctree rank 2/4 for CRUK0013 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal   LN1   LN2    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99  0.99 0.99   0.99
    ## 2 2           1 TRUE      FALSE      0     0     0    0.75   0   
    ## 3 3           1 TRUE      FALSE      0.97  0.96  0.01 0.580  0.94
    ## 4 4           1 TRUE      FALSE      0     0     0.97 0.37   0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: STK11
    ##     |-3 :: KRAS
    ##     | \-4 :: EGFR
    ##     \-2 :: NOTCH1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    STK11 ---> NOTCH1 
    ##    STK11 ---> KRAS 
    ##    KRAS ---> EGFR 
    ## 
    ## Tree score 0.24 
    ## 
    ## $phylogenies$CRUK0013$`3`
    ##  [ ctree - ctree rank 3/4 for CRUK0013 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal   LN1   LN2    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99  0.99 0.99   0.99
    ## 2 2           1 TRUE      FALSE      0     0     0    0.75   0   
    ## 3 3           1 TRUE      FALSE      0.97  0.96  0.01 0.580  0.94
    ## 4 4           1 TRUE      FALSE      0     0     0.97 0.37   0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: STK11
    ##     |-2 :: NOTCH1
    ##     | \-3 :: KRAS
    ##     \-4 :: EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    STK11 ---> NOTCH1 
    ##    NOTCH1 ---> KRAS 
    ##    STK11 ---> EGFR 
    ## 
    ## Tree score 0.02 
    ## 
    ## $phylogenies$CRUK0013$`4`
    ##  [ ctree - ctree rank 4/4 for CRUK0013 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal   LN1   LN2    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99  0.99 0.99   0.99
    ## 2 2           1 TRUE      FALSE      0     0     0    0.75   0   
    ## 3 3           1 TRUE      FALSE      0.97  0.96  0.01 0.580  0.94
    ## 4 4           1 TRUE      FALSE      0     0     0.97 0.37   0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: STK11
    ##     \-2 :: NOTCH1
    ##      \-3 :: KRAS
    ##       \-4 :: EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    STK11 ---> NOTCH1 
    ##    NOTCH1 ---> KRAS 
    ##    KRAS ---> EGFR 
    ## 
    ## Tree score 0.02 
    ## 
    ## 
    ## $phylogenies$CRUK0014
    ## $phylogenies$CRUK0014$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0014 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.96  0.96
    ## 2 2           1 TRUE      FALSE      0.35  0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, KRAS
    ##     \-2 :: RNF43
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> KRAS 
    ##    TP53 ---> RNF43 
    ##    KRAS ---> RNF43 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0015
    ## $phylogenies$CRUK0015$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0015 ] 
    ## 
    ## # A tibble: 3 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.99
    ## 2 2           1 TRUE      FALSE      0.94  0.01
    ## 3 3           1 TRUE      FALSE      0.01  0.65
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: BAP1, EGFR
    ##     |-2 :: TP53
    ##     \-3 :: RB1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> BAP1 
    ##    GL ---> EGFR 
    ##    BAP1 ---> TP53 
    ##    EGFR ---> TP53 
    ##    BAP1 ---> RB1 
    ##    EGFR ---> RB1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0016
    ## $phylogenies$CRUK0016$`1`
    ##  [ ctree - ctree rank 1/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     |-16 :: LATS1, ARID1B
    ##     | \-2 :: ASXL1
    ##     |-10 :: DNM2
    ##     \-6 :: PTPRC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    TP53 ---> DNM2 
    ##    FAT1 ---> DNM2 
    ##    SPEN ---> DNM2 
    ##    CBLB ---> DNM2 
    ##    TERT ---> DNM2 
    ##    CDKN2A ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    TP53 ---> PTPRC 
    ##    FAT1 ---> PTPRC 
    ##    SPEN ---> PTPRC 
    ##    CBLB ---> PTPRC 
    ##    TERT ---> PTPRC 
    ##    CDKN2A ---> PTPRC 
    ## 
    ## Tree score 0.03125 
    ## 
    ## $phylogenies$CRUK0016$`2`
    ##  [ ctree - ctree rank 2/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     \-16 :: LATS1, ARID1B
    ##      |-2 :: ASXL1
    ##      | \-10 :: DNM2
    ##      \-6 :: PTPRC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    ASXL1 ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    LATS1 ---> PTPRC 
    ##    ARID1B ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`3`
    ##  [ ctree - ctree rank 3/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     \-16 :: LATS1, ARID1B
    ##      \-2 :: ASXL1
    ##       \-6 :: PTPRC
    ##        \-10 :: DNM2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    PTPRC ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    ASXL1 ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`4`
    ##  [ ctree - ctree rank 4/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     \-16 :: LATS1, ARID1B
    ##      |-10 :: DNM2
    ##      | \-6 :: PTPRC
    ##      \-2 :: ASXL1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    LATS1 ---> DNM2 
    ##    ARID1B ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    DNM2 ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`5`
    ##  [ ctree - ctree rank 5/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     \-16 :: LATS1, ARID1B
    ##      \-2 :: ASXL1
    ##       \-10 :: DNM2
    ##        \-6 :: PTPRC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    ASXL1 ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    DNM2 ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`6`
    ##  [ ctree - ctree rank 6/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     |-16 :: LATS1, ARID1B
    ##     | \-2 :: ASXL1
    ##     |  \-10 :: DNM2
    ##     \-6 :: PTPRC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    ASXL1 ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    TP53 ---> PTPRC 
    ##    FAT1 ---> PTPRC 
    ##    SPEN ---> PTPRC 
    ##    CBLB ---> PTPRC 
    ##    TERT ---> PTPRC 
    ##    CDKN2A ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`7`
    ##  [ ctree - ctree rank 7/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     |-16 :: LATS1, ARID1B
    ##     | |-6 :: PTPRC
    ##     | \-2 :: ASXL1
    ##     \-10 :: DNM2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    TP53 ---> DNM2 
    ##    FAT1 ---> DNM2 
    ##    SPEN ---> DNM2 
    ##    CBLB ---> DNM2 
    ##    TERT ---> DNM2 
    ##    CDKN2A ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    LATS1 ---> PTPRC 
    ##    ARID1B ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`8`
    ##  [ ctree - ctree rank 8/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     |-10 :: DNM2
    ##     | \-6 :: PTPRC
    ##     \-16 :: LATS1, ARID1B
    ##      \-2 :: ASXL1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    TP53 ---> DNM2 
    ##    FAT1 ---> DNM2 
    ##    SPEN ---> DNM2 
    ##    CBLB ---> DNM2 
    ##    TERT ---> DNM2 
    ##    CDKN2A ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    DNM2 ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`9`
    ##  [ ctree - ctree rank 9/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     |-16 :: LATS1, ARID1B
    ##     | |-10 :: DNM2
    ##     | \-2 :: ASXL1
    ##     \-6 :: PTPRC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    LATS1 ---> DNM2 
    ##    ARID1B ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    TP53 ---> PTPRC 
    ##    FAT1 ---> PTPRC 
    ##    SPEN ---> PTPRC 
    ##    CBLB ---> PTPRC 
    ##    TERT ---> PTPRC 
    ##    CDKN2A ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`10`
    ##  [ ctree - ctree rank 10/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     \-16 :: LATS1, ARID1B
    ##      |-6 :: PTPRC
    ##      | \-10 :: DNM2
    ##      \-2 :: ASXL1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    PTPRC ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    LATS1 ---> PTPRC 
    ##    ARID1B ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`11`
    ##  [ ctree - ctree rank 11/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     |-6 :: PTPRC
    ##     | \-10 :: DNM2
    ##     \-16 :: LATS1, ARID1B
    ##      \-2 :: ASXL1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    PTPRC ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    TP53 ---> PTPRC 
    ##    FAT1 ---> PTPRC 
    ##    SPEN ---> PTPRC 
    ##    CBLB ---> PTPRC 
    ##    TERT ---> PTPRC 
    ##    CDKN2A ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`12`
    ##  [ ctree - ctree rank 12/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     \-16 :: LATS1, ARID1B
    ##      |-2 :: ASXL1
    ##      | \-6 :: PTPRC
    ##      \-10 :: DNM2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    LATS1 ---> DNM2 
    ##    ARID1B ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    ASXL1 ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## $phylogenies$CRUK0016$`13`
    ##  [ ctree - ctree rank 13/13 for CRUK0016 ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     |-16 :: LATS1, ARID1B
    ##     | \-2 :: ASXL1
    ##     |  \-6 :: PTPRC
    ##     \-10 :: DNM2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> SPEN 
    ##    GL ---> CBLB 
    ##    GL ---> TERT 
    ##    GL ---> CDKN2A 
    ##    TP53 ---> LATS1 
    ##    TP53 ---> ARID1B 
    ##    FAT1 ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> LATS1 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> LATS1 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> LATS1 
    ##    TERT ---> ARID1B 
    ##    CDKN2A ---> LATS1 
    ##    CDKN2A ---> ARID1B 
    ##    TP53 ---> DNM2 
    ##    FAT1 ---> DNM2 
    ##    SPEN ---> DNM2 
    ##    CBLB ---> DNM2 
    ##    TERT ---> DNM2 
    ##    CDKN2A ---> DNM2 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ##    ASXL1 ---> PTPRC 
    ## 
    ## Tree score 0.015625 
    ## 
    ## 
    ## $phylogenies$CRUK0017
    ## $phylogenies$CRUK0017$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0017 ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1  1     1     1   
    ## 2 3           1 TRUE      FALSE         0  0.94  0.95  0.59
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: TP53, ARID1B, ARID2, KEAP1, MYC
    ##     \-3 :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> ARID1B 
    ##    GL ---> ARID2 
    ##    GL ---> KEAP1 
    ##    GL ---> MYC 
    ##    TP53 ---> KRAS 
    ##    ARID1B ---> KRAS 
    ##    ARID2 ---> KRAS 
    ##    KEAP1 ---> KRAS 
    ##    MYC ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0018
    ## $phylogenies$CRUK0018$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0018 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: CMTR2, KRAS, MGA, COL5A2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CMTR2 
    ##    GL ---> KRAS 
    ##    GL ---> MGA 
    ##    GL ---> COL5A2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0019
    ## $phylogenies$CRUK0019$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0019 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.97  0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0020
    ## $phylogenies$CRUK0020$`1`
    ##  [ ctree - ctree rank 1/2 for CRUK0020 ] 
    ## 
    ## # A tibble: 4 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       1     1   
    ## 2 2           1 TRUE      FALSE      0.87  0   
    ## 3 3           1 TRUE      FALSE      0.9   0.08
    ## 4 4           1 TRUE      FALSE      0     0.85
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: KEAP1, TP53, MGA, ARID2, COL2A1, PRF1, KRAS
    ##     |-3 :: BAP1
    ##     | \-2 :: PIK3CA
    ##     \-4 :: NCOR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> TP53 
    ##    GL ---> MGA 
    ##    GL ---> ARID2 
    ##    GL ---> COL2A1 
    ##    GL ---> PRF1 
    ##    GL ---> KRAS 
    ##    BAP1 ---> PIK3CA 
    ##    KEAP1 ---> BAP1 
    ##    TP53 ---> BAP1 
    ##    MGA ---> BAP1 
    ##    ARID2 ---> BAP1 
    ##    COL2A1 ---> BAP1 
    ##    PRF1 ---> BAP1 
    ##    KRAS ---> BAP1 
    ##    KEAP1 ---> NCOR1 
    ##    TP53 ---> NCOR1 
    ##    MGA ---> NCOR1 
    ##    ARID2 ---> NCOR1 
    ##    COL2A1 ---> NCOR1 
    ##    PRF1 ---> NCOR1 
    ##    KRAS ---> NCOR1 
    ## 
    ## Tree score 0.666666666666667 
    ## 
    ## $phylogenies$CRUK0020$`2`
    ##  [ ctree - ctree rank 2/2 for CRUK0020 ] 
    ## 
    ## # A tibble: 4 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       1     1   
    ## 2 2           1 TRUE      FALSE      0.87  0   
    ## 3 3           1 TRUE      FALSE      0.9   0.08
    ## 4 4           1 TRUE      FALSE      0     0.85
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: KEAP1, TP53, MGA, ARID2, COL2A1, PRF1, KRAS
    ##     \-4 :: NCOR1
    ##      \-3 :: BAP1
    ##       \-2 :: PIK3CA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> TP53 
    ##    GL ---> MGA 
    ##    GL ---> ARID2 
    ##    GL ---> COL2A1 
    ##    GL ---> PRF1 
    ##    GL ---> KRAS 
    ##    BAP1 ---> PIK3CA 
    ##    NCOR1 ---> BAP1 
    ##    KEAP1 ---> NCOR1 
    ##    TP53 ---> NCOR1 
    ##    MGA ---> NCOR1 
    ##    ARID2 ---> NCOR1 
    ##    COL2A1 ---> NCOR1 
    ##    PRF1 ---> NCOR1 
    ##    KRAS ---> NCOR1 
    ## 
    ## Tree score 0.166666666666667 
    ## 
    ## 
    ## $phylogenies$CRUK0021
    ## $phylogenies$CRUK0021$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0021 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: EGFR, TP53, CHEK2, CDKN2A
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> TP53 
    ##    GL ---> CHEK2 
    ##    GL ---> CDKN2A 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0022
    ## $phylogenies$CRUK0022$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0022 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.99
    ## 2 2           1 TRUE      FALSE      0.85  0   
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2] :: TP53, EGFR
    ##     \-2 :: CIC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> EGFR 
    ##    TP53 ---> CIC 
    ##    EGFR ---> CIC 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0023
    ## $phylogenies$CRUK0023$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0023 ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99 0.98   0.99  0.95
    ## 2 4           2 TRUE      FALSE      0.01 0.945  0     0   
    ## 3 2           1 TRUE      FALSE      0.81 0      0     0   
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3, R4] :: WRN, KRAS, CDKN2A
    ##     |-2 :: TP53
    ##     \-4 :: PTPRC, KMT2D
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> WRN 
    ##    GL ---> KRAS 
    ##    GL ---> CDKN2A 
    ##    WRN ---> PTPRC 
    ##    WRN ---> KMT2D 
    ##    KRAS ---> PTPRC 
    ##    KRAS ---> KMT2D 
    ##    CDKN2A ---> PTPRC 
    ##    CDKN2A ---> KMT2D 
    ##    WRN ---> TP53 
    ##    KRAS ---> TP53 
    ##    CDKN2A ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0024
    ## $phylogenies$CRUK0024$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0024 ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R3    R4    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1        1
    ## 2 3           1 TRUE      FALSE      0.88  0.97  0.95     0
    ## 3 4           1 TRUE      FALSE      0.83  0     0        0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R6] :: TP53, STK11, POLE, EGFR
    ##     \-3 :: ATM
    ##      \-4 :: NCOR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> STK11 
    ##    GL ---> POLE 
    ##    GL ---> EGFR 
    ##    TP53 ---> ATM 
    ##    STK11 ---> ATM 
    ##    POLE ---> ATM 
    ##    EGFR ---> ATM 
    ##    ATM ---> NCOR1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0025
    ## $phylogenies$CRUK0025$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0025 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: KRAS, TP53, MGA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    GL ---> MGA 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0026
    ## $phylogenies$CRUK0026$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0026 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.98  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: TP53, EGFR, RB1, SERPINB13
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> EGFR 
    ##    GL ---> RB1 
    ##    GL ---> SERPINB13 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0027
    ## $phylogenies$CRUK0027$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0027 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.96  1   
    ## 2 2           1 TRUE      FALSE      0     0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: KRAS, TP53
    ##     \-2 :: PLXNB2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    KRAS ---> PLXNB2 
    ##    TP53 ---> PLXNB2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0028
    ## $phylogenies$CRUK0028$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0028 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE      0.975  0.95
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: APC, EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> APC 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0029
    ## $phylogenies$CRUK0029$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0029 ] 
    ## 
    ## # A tibble: 1 x 10
    ##   cluster nMuts is.driver is.clonal    R2    R4    R5    R6    R7    R8
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99  0.98     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R4, R5, R6, R7, R8] :: TP53, NRAS, MGA, CCND1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> NRAS 
    ##    GL ---> MGA 
    ##    GL ---> CCND1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0030
    ## $phylogenies$CRUK0030$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0030 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.98  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: KRAS, TSC2, U2AF1, TP53, FBXW7, NF1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> TSC2 
    ##    GL ---> U2AF1 
    ##    GL ---> TP53 
    ##    GL ---> FBXW7 
    ##    GL ---> NF1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0031
    ## $phylogenies$CRUK0031$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0031 ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1        1
    ## 2 6           1 TRUE      FALSE      0.88  0.05     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3] :: KEAP1, CDKN2A, PRF1, FGFR1
    ##     \-6 :: NF1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> CDKN2A 
    ##    GL ---> PRF1 
    ##    GL ---> FGFR1 
    ##    KEAP1 ---> NF1 
    ##    CDKN2A ---> NF1 
    ##    PRF1 ---> NF1 
    ##    FGFR1 ---> NF1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0032
    ## $phylogenies$CRUK0032$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0032 ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  1        1  1   
    ## 2 4           1 TRUE      FALSE         0  0.97     0  0.98
    ## 3 6           1 TRUE      FALSE         0  0        0  0.3 
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: ATM, RAD21, U2AF1, RNF43
    ##     \-4 :: CCND1
    ##      \-6 :: ARID1B
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> ATM 
    ##    GL ---> RAD21 
    ##    GL ---> U2AF1 
    ##    GL ---> RNF43 
    ##    ATM ---> CCND1 
    ##    RAD21 ---> CCND1 
    ##    U2AF1 ---> CCND1 
    ##    RNF43 ---> CCND1 
    ##    CCND1 ---> ARID1B 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0033
    ## $phylogenies$CRUK0033$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0033 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: KEAP1, CTNNB1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> CTNNB1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0034
    ## $phylogenies$CRUK0034$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0034 ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1   1       1
    ## 2 4           1 TRUE      FALSE         0   0.5     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: ATM, KRAS, PLXNB2
    ##     \-4 :: MGA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> ATM 
    ##    GL ---> KRAS 
    ##    GL ---> PLXNB2 
    ##    ATM ---> MGA 
    ##    KRAS ---> MGA 
    ##    PLXNB2 ---> MGA 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0035
    ## $phylogenies$CRUK0035$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0035 ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal   LN1    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.98  0.99  0.99
    ## 2 4           1 TRUE      FALSE      0     0.8   0     0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [LN1, R2] :: TP53, FAS
    ##     \-4 :: FLT4
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAS 
    ##    TP53 ---> FLT4 
    ##    FAS ---> FLT4 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0036
    ## $phylogenies$CRUK0036$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0036 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  0.98  0.97     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: KRAS, PIK3CA, KEAP1, ARHGAP35, TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> PIK3CA 
    ##    GL ---> KEAP1 
    ##    GL ---> ARHGAP35 
    ##    GL ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0037
    ## $phylogenies$CRUK0037$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0037 ] 
    ## 
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99     1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4, R5] :: NCOA6, CREBBP, KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> NCOA6 
    ##    GL ---> CREBBP 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0038
    ## $phylogenies$CRUK0038$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0038 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99
    ## 2 3           1 TRUE      FALSE      0     0.38
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: KRAS
    ##     \-3 :: KMT2D
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    KRAS ---> KMT2D 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0039
    ## $phylogenies$CRUK0039$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0039 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: KRAS, CMTR2, NF1, PHOX2B
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> CMTR2 
    ##    GL ---> NF1 
    ##    GL ---> PHOX2B 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0040
    ## $phylogenies$CRUK0040$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0040 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.99  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: NCOR1, RAD21, KRAS, GATA3
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> NCOR1 
    ##    GL ---> RAD21 
    ##    GL ---> KRAS 
    ##    GL ---> GATA3 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0041
    ## $phylogenies$CRUK0041$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0041 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.99  0.99  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: BRAF, TERT, EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> BRAF 
    ##    GL ---> TERT 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0042
    ## $phylogenies$CRUK0042$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0042 ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           1 TRUE      TRUE       0.91
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0043
    ## $phylogenies$CRUK0043$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0043 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: MET
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> MET 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0044
    ## $phylogenies$CRUK0044$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0044 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0045
    ## $phylogenies$CRUK0045$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0045 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.98  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: BAP1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> BAP1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0046
    ## $phylogenies$CRUK0046$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0046 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1  0.98 0.995  0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: KEAP1, APC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> APC 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0047
    ## $phylogenies$CRUK0047$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0047 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.99     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: STK11, APC, KRAS, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    GL ---> APC 
    ##    GL ---> KRAS 
    ##    GL ---> MYC 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0048
    ## $phylogenies$CRUK0048$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0048 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: APC, PRDM1, ARHGAP35, TP53, BRAF, EGFR, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> APC 
    ##    GL ---> PRDM1 
    ##    GL ---> ARHGAP35 
    ##    GL ---> TP53 
    ##    GL ---> BRAF 
    ##    GL ---> EGFR 
    ##    GL ---> MYC 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0049
    ## $phylogenies$CRUK0049$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0049 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: RB1, TP53, COL2A1, EGFR, KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> RB1 
    ##    GL ---> TP53 
    ##    GL ---> COL2A1 
    ##    GL ---> EGFR 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0050
    ## $phylogenies$CRUK0050$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0050 ] 
    ## 
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99  0.99  0.99     1  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4, R5] :: KRAS, STK11, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> STK11 
    ##    GL ---> MYC 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0051
    ## $phylogenies$CRUK0051$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0051 ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1        1     1
    ## 2 3           1 TRUE      FALSE      0.97     0     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3, R4] :: KRAS, FBXW7, TP53, EGFR
    ##     \-3 :: EP300
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> FBXW7 
    ##    GL ---> TP53 
    ##    GL ---> EGFR 
    ##    KRAS ---> EP300 
    ##    FBXW7 ---> EP300 
    ##    TP53 ---> EP300 
    ##    EGFR ---> EP300 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0052
    ## $phylogenies$CRUK0052$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0052 ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1     1  1   
    ## 2 2           1 TRUE      FALSE         0     0  0.86
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: KMT2D, KRAS, NOTCH2, MGA, KEAP1, TP53, NF1, SGK223
    ##     \-2 :: UBR5
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KMT2D 
    ##    GL ---> KRAS 
    ##    GL ---> NOTCH2 
    ##    GL ---> MGA 
    ##    GL ---> KEAP1 
    ##    GL ---> TP53 
    ##    GL ---> NF1 
    ##    GL ---> SGK223 
    ##    KMT2D ---> UBR5 
    ##    KRAS ---> UBR5 
    ##    NOTCH2 ---> UBR5 
    ##    MGA ---> UBR5 
    ##    KEAP1 ---> UBR5 
    ##    TP53 ---> UBR5 
    ##    NF1 ---> UBR5 
    ##    SGK223 ---> UBR5 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0054
    ## $phylogenies$CRUK0054$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0054 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0055
    ## $phylogenies$CRUK0055$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0055 ] 
    ## 
    ## # A tibble: 2 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           2 TRUE      TRUE       1   
    ## 2 2           1 TRUE      FALSE      0.32
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: FANCM, UBR5
    ##     \-2 :: FAT1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> FANCM 
    ##    GL ---> UBR5 
    ##    FANCM ---> FAT1 
    ##    UBR5 ---> FAT1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0056
    ## $phylogenies$CRUK0056$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0056 ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1  1     1   
    ## 2 3           1 TRUE      FALSE         0  0.12  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: RASA1, CREBBP
    ##     \-3 :: TP53
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> RASA1 
    ##    GL ---> CREBBP 
    ##    RASA1 ---> TP53 
    ##    CREBBP ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0057
    ## $phylogenies$CRUK0057$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0057 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: KRAS, SMARCA4, TSC2, DNM2, TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> SMARCA4 
    ##    GL ---> TSC2 
    ##    GL ---> DNM2 
    ##    GL ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0058
    ## $phylogenies$CRUK0058$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0058 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: TP53, EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0059
    ## $phylogenies$CRUK0059$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0059 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0060
    ## $phylogenies$CRUK0060$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0060 ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1          11 TRUE      TRUE          1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: SERPINB13, ARID2, COL5A2, FANCM, PHOX2B, COL2A1, RASA1, NF1, NCOA6, NOTCH2, KMT2C
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SERPINB13 
    ##    GL ---> ARID2 
    ##    GL ---> COL5A2 
    ##    GL ---> FANCM 
    ##    GL ---> PHOX2B 
    ##    GL ---> COL2A1 
    ##    GL ---> RASA1 
    ##    GL ---> NF1 
    ##    GL ---> NCOA6 
    ##    GL ---> NOTCH2 
    ##    GL ---> KMT2C 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0061
    ## $phylogenies$CRUK0061$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0061 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: STK11
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0062
    ## $phylogenies$CRUK0062$`1`
    ##  [ ctree - ctree rank 1/2 for CRUK0062 ] 
    ## 
    ## # A tibble: 4 x 11
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 4           4 TRUE      TRUE       0.99  0.99  0.98  0.97  0.99  0.99
    ## 2 1           1 TRUE      FALSE      0     0.01  0     0     0     0.94
    ## 3 16          1 TRUE      FALSE      0.93  0.86  0.08  0.02  0.12  0   
    ## 4 2           1 TRUE      FALSE      0.84  0.83  0.02  0     0     0   
    ## # … with 1 more variable: R7 <dbl>
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-4 :: TP53, PIK3CA, SOX2, CCND1
    ##     |-16 :: UBR5
    ##     | \-2 :: PLXNB2
    ##     \-1 :: FAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> CCND1 
    ##    TP53 ---> FAS 
    ##    PIK3CA ---> FAS 
    ##    SOX2 ---> FAS 
    ##    CCND1 ---> FAS 
    ##    TP53 ---> UBR5 
    ##    PIK3CA ---> UBR5 
    ##    SOX2 ---> UBR5 
    ##    CCND1 ---> UBR5 
    ##    UBR5 ---> PLXNB2 
    ## 
    ## Tree score 0.75 
    ## 
    ## $phylogenies$CRUK0062$`2`
    ##  [ ctree - ctree rank 2/2 for CRUK0062 ] 
    ## 
    ## # A tibble: 4 x 11
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 4           4 TRUE      TRUE       0.99  0.99  0.98  0.97  0.99  0.99
    ## 2 1           1 TRUE      FALSE      0     0.01  0     0     0     0.94
    ## 3 16          1 TRUE      FALSE      0.93  0.86  0.08  0.02  0.12  0   
    ## 4 2           1 TRUE      FALSE      0.84  0.83  0.02  0     0     0   
    ## # … with 1 more variable: R7 <dbl>
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-4 :: TP53, PIK3CA, SOX2, CCND1
    ##     |-2 :: PLXNB2
    ##     |-16 :: UBR5
    ##     \-1 :: FAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> CCND1 
    ##    TP53 ---> FAS 
    ##    PIK3CA ---> FAS 
    ##    SOX2 ---> FAS 
    ##    CCND1 ---> FAS 
    ##    TP53 ---> UBR5 
    ##    PIK3CA ---> UBR5 
    ##    SOX2 ---> UBR5 
    ##    CCND1 ---> UBR5 
    ##    TP53 ---> PLXNB2 
    ##    PIK3CA ---> PLXNB2 
    ##    SOX2 ---> PLXNB2 
    ##    CCND1 ---> PLXNB2 
    ## 
    ## Tree score 0.178571428571429 
    ## 
    ## 
    ## $phylogenies$CRUK0063
    ## $phylogenies$CRUK0063$`1`
    ##  [ ctree - ctree rank 1/6 for CRUK0063 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 2           7 TRUE      TRUE       0.93  0.99  0.99  0.99  1   
    ## 2 1           2 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 3 10          1 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 4 6           1 TRUE      FALSE      0     0.02  0.7   0.36  0.55
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R3] :: PIK3CA, TP53, FBXW7, CDKN2A, SOX2, TERT, PRF1
    ##     \-10 :: EP300
    ##      \-1 :: NF1, CYLD
    ##       \-6 :: FANCM
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> TP53 
    ##    GL ---> FBXW7 
    ##    GL ---> CDKN2A 
    ##    GL ---> SOX2 
    ##    GL ---> TERT 
    ##    GL ---> PRF1 
    ##    EP300 ---> NF1 
    ##    EP300 ---> CYLD 
    ##    PIK3CA ---> EP300 
    ##    TP53 ---> EP300 
    ##    FBXW7 ---> EP300 
    ##    CDKN2A ---> EP300 
    ##    SOX2 ---> EP300 
    ##    TERT ---> EP300 
    ##    PRF1 ---> EP300 
    ##    NF1 ---> FANCM 
    ##    CYLD ---> FANCM 
    ## 
    ## Tree score 0.125 
    ## 
    ## $phylogenies$CRUK0063$`2`
    ##  [ ctree - ctree rank 2/6 for CRUK0063 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 2           7 TRUE      TRUE       0.93  0.99  0.99  0.99  1   
    ## 2 1           2 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 3 10          1 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 4 6           1 TRUE      FALSE      0     0.02  0.7   0.36  0.55
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R3] :: PIK3CA, TP53, FBXW7, CDKN2A, SOX2, TERT, PRF1
    ##     \-1 :: NF1, CYLD
    ##      \-10 :: EP300
    ##       \-6 :: FANCM
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> TP53 
    ##    GL ---> FBXW7 
    ##    GL ---> CDKN2A 
    ##    GL ---> SOX2 
    ##    GL ---> TERT 
    ##    GL ---> PRF1 
    ##    PIK3CA ---> NF1 
    ##    PIK3CA ---> CYLD 
    ##    TP53 ---> NF1 
    ##    TP53 ---> CYLD 
    ##    FBXW7 ---> NF1 
    ##    FBXW7 ---> CYLD 
    ##    CDKN2A ---> NF1 
    ##    CDKN2A ---> CYLD 
    ##    SOX2 ---> NF1 
    ##    SOX2 ---> CYLD 
    ##    TERT ---> NF1 
    ##    TERT ---> CYLD 
    ##    PRF1 ---> NF1 
    ##    PRF1 ---> CYLD 
    ##    NF1 ---> EP300 
    ##    CYLD ---> EP300 
    ##    EP300 ---> FANCM 
    ## 
    ## Tree score 0.125 
    ## 
    ## $phylogenies$CRUK0063$`3`
    ##  [ ctree - ctree rank 3/6 for CRUK0063 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 2           7 TRUE      TRUE       0.93  0.99  0.99  0.99  1   
    ## 2 1           2 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 3 10          1 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 4 6           1 TRUE      FALSE      0     0.02  0.7   0.36  0.55
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R3] :: PIK3CA, TP53, FBXW7, CDKN2A, SOX2, TERT, PRF1
    ##     \-10 :: EP300
    ##      |-1 :: NF1, CYLD
    ##      \-6 :: FANCM
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> TP53 
    ##    GL ---> FBXW7 
    ##    GL ---> CDKN2A 
    ##    GL ---> SOX2 
    ##    GL ---> TERT 
    ##    GL ---> PRF1 
    ##    EP300 ---> NF1 
    ##    EP300 ---> CYLD 
    ##    PIK3CA ---> EP300 
    ##    TP53 ---> EP300 
    ##    FBXW7 ---> EP300 
    ##    CDKN2A ---> EP300 
    ##    SOX2 ---> EP300 
    ##    TERT ---> EP300 
    ##    PRF1 ---> EP300 
    ##    EP300 ---> FANCM 
    ## 
    ## Tree score 0.025 
    ## 
    ## $phylogenies$CRUK0063$`4`
    ##  [ ctree - ctree rank 4/6 for CRUK0063 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 2           7 TRUE      TRUE       0.93  0.99  0.99  0.99  1   
    ## 2 1           2 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 3 10          1 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 4 6           1 TRUE      FALSE      0     0.02  0.7   0.36  0.55
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R3] :: PIK3CA, TP53, FBXW7, CDKN2A, SOX2, TERT, PRF1
    ##     \-1 :: NF1, CYLD
    ##      |-10 :: EP300
    ##      \-6 :: FANCM
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> TP53 
    ##    GL ---> FBXW7 
    ##    GL ---> CDKN2A 
    ##    GL ---> SOX2 
    ##    GL ---> TERT 
    ##    GL ---> PRF1 
    ##    PIK3CA ---> NF1 
    ##    PIK3CA ---> CYLD 
    ##    TP53 ---> NF1 
    ##    TP53 ---> CYLD 
    ##    FBXW7 ---> NF1 
    ##    FBXW7 ---> CYLD 
    ##    CDKN2A ---> NF1 
    ##    CDKN2A ---> CYLD 
    ##    SOX2 ---> NF1 
    ##    SOX2 ---> CYLD 
    ##    TERT ---> NF1 
    ##    TERT ---> CYLD 
    ##    PRF1 ---> NF1 
    ##    PRF1 ---> CYLD 
    ##    NF1 ---> EP300 
    ##    CYLD ---> EP300 
    ##    NF1 ---> FANCM 
    ##    CYLD ---> FANCM 
    ## 
    ## Tree score 0.025 
    ## 
    ## $phylogenies$CRUK0063$`5`
    ##  [ ctree - ctree rank 5/6 for CRUK0063 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 2           7 TRUE      TRUE       0.93  0.99  0.99  0.99  1   
    ## 2 1           2 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 3 10          1 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 4 6           1 TRUE      FALSE      0     0.02  0.7   0.36  0.55
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R3] :: PIK3CA, TP53, FBXW7, CDKN2A, SOX2, TERT, PRF1
    ##     |-1 :: NF1, CYLD
    ##     | \-6 :: FANCM
    ##     \-10 :: EP300
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> TP53 
    ##    GL ---> FBXW7 
    ##    GL ---> CDKN2A 
    ##    GL ---> SOX2 
    ##    GL ---> TERT 
    ##    GL ---> PRF1 
    ##    PIK3CA ---> NF1 
    ##    PIK3CA ---> CYLD 
    ##    TP53 ---> NF1 
    ##    TP53 ---> CYLD 
    ##    FBXW7 ---> NF1 
    ##    FBXW7 ---> CYLD 
    ##    CDKN2A ---> NF1 
    ##    CDKN2A ---> CYLD 
    ##    SOX2 ---> NF1 
    ##    SOX2 ---> CYLD 
    ##    TERT ---> NF1 
    ##    TERT ---> CYLD 
    ##    PRF1 ---> NF1 
    ##    PRF1 ---> CYLD 
    ##    PIK3CA ---> EP300 
    ##    TP53 ---> EP300 
    ##    FBXW7 ---> EP300 
    ##    CDKN2A ---> EP300 
    ##    SOX2 ---> EP300 
    ##    TERT ---> EP300 
    ##    PRF1 ---> EP300 
    ##    NF1 ---> FANCM 
    ##    CYLD ---> FANCM 
    ## 
    ## Tree score 0.025 
    ## 
    ## $phylogenies$CRUK0063$`6`
    ##  [ ctree - ctree rank 6/6 for CRUK0063 ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 2           7 TRUE      TRUE       0.93  0.99  0.99  0.99  1   
    ## 2 1           2 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 3 10          1 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 4 6           1 TRUE      FALSE      0     0.02  0.7   0.36  0.55
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R3] :: PIK3CA, TP53, FBXW7, CDKN2A, SOX2, TERT, PRF1
    ##     |-10 :: EP300
    ##     | \-6 :: FANCM
    ##     \-1 :: NF1, CYLD
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> TP53 
    ##    GL ---> FBXW7 
    ##    GL ---> CDKN2A 
    ##    GL ---> SOX2 
    ##    GL ---> TERT 
    ##    GL ---> PRF1 
    ##    PIK3CA ---> NF1 
    ##    PIK3CA ---> CYLD 
    ##    TP53 ---> NF1 
    ##    TP53 ---> CYLD 
    ##    FBXW7 ---> NF1 
    ##    FBXW7 ---> CYLD 
    ##    CDKN2A ---> NF1 
    ##    CDKN2A ---> CYLD 
    ##    SOX2 ---> NF1 
    ##    SOX2 ---> CYLD 
    ##    TERT ---> NF1 
    ##    TERT ---> CYLD 
    ##    PRF1 ---> NF1 
    ##    PRF1 ---> CYLD 
    ##    PIK3CA ---> EP300 
    ##    TP53 ---> EP300 
    ##    FBXW7 ---> EP300 
    ##    CDKN2A ---> EP300 
    ##    SOX2 ---> EP300 
    ##    TERT ---> EP300 
    ##    PRF1 ---> EP300 
    ##    EP300 ---> FANCM 
    ## 
    ## Tree score 0.025 
    ## 
    ## 
    ## $phylogenies$CRUK0064
    ## $phylogenies$CRUK0064$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0064 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 2           2 TRUE      FALSE      0.64  0.11
    ## 2 1           1 TRUE      TRUE       1     1   
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53
    ##     \-2 :: MLH1, FAT1
    ## 
    ## Information transfer  
    ## 
    ##    TP53 ---> MLH1 
    ##    TP53 ---> FAT1 
    ##    GL ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0065
    ## $phylogenies$CRUK0065$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0065 ] 
    ## 
    ## # A tibble: 3 x 10
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99  0.99     1  1     1   
    ## 2 2           3 TRUE      FALSE         0  0     0        0  0.48  0   
    ## 3 6           2 TRUE      FALSE         0  0     0        0  0.01  0.83
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: TP53, NFE2L2, PIK3CA, SOX2
    ##     |-2 :: MLH1, PTPRC, UBR5
    ##     \-6 :: NOTCH1, NCOA6
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> NFE2L2 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    TP53 ---> MLH1 
    ##    TP53 ---> PTPRC 
    ##    TP53 ---> UBR5 
    ##    NFE2L2 ---> MLH1 
    ##    NFE2L2 ---> PTPRC 
    ##    NFE2L2 ---> UBR5 
    ##    PIK3CA ---> MLH1 
    ##    PIK3CA ---> PTPRC 
    ##    PIK3CA ---> UBR5 
    ##    SOX2 ---> MLH1 
    ##    SOX2 ---> PTPRC 
    ##    SOX2 ---> UBR5 
    ##    TP53 ---> NOTCH1 
    ##    TP53 ---> NCOA6 
    ##    NFE2L2 ---> NOTCH1 
    ##    NFE2L2 ---> NCOA6 
    ##    PIK3CA ---> NOTCH1 
    ##    PIK3CA ---> NCOA6 
    ##    SOX2 ---> NOTCH1 
    ##    SOX2 ---> NCOA6 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0066
    ## $phylogenies$CRUK0066$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0066 ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       0.99  1     1     0.99
    ## 2 9           1 TRUE      FALSE      0     0.91  0.01  0   
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R4] :: TP53, NOTCH1, CDKN2A, WRN, PDGFRA, TERT, NCOA6
    ##     \-9 :: COL5A2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> NOTCH1 
    ##    GL ---> CDKN2A 
    ##    GL ---> WRN 
    ##    GL ---> PDGFRA 
    ##    GL ---> TERT 
    ##    GL ---> NCOA6 
    ##    TP53 ---> COL5A2 
    ##    NOTCH1 ---> COL5A2 
    ##    CDKN2A ---> COL5A2 
    ##    WRN ---> COL5A2 
    ##    PDGFRA ---> COL5A2 
    ##    TERT ---> COL5A2 
    ##    NCOA6 ---> COL5A2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0067
    ## $phylogenies$CRUK0067$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0067 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1   
    ## 2 2           1 TRUE      FALSE      0.61  0.83
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: NOTCH1, TP53, PIK3CA, SOX2, CDKN2A
    ##     \-2 :: NFE2L2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> NOTCH1 
    ##    GL ---> TP53 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> CDKN2A 
    ##    NOTCH1 ---> NFE2L2 
    ##    TP53 ---> NFE2L2 
    ##    PIK3CA ---> NFE2L2 
    ##    SOX2 ---> NFE2L2 
    ##    CDKN2A ---> NFE2L2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0068
    ## $phylogenies$CRUK0068$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0068 ] 
    ## 
    ## # A tibble: 4 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1     1     1   
    ## 2 3           1 TRUE      FALSE      0.5   0     0     0   
    ## 3 4           1 TRUE      FALSE      0.98  0.37  0.99  0.01
    ## 4 9           1 TRUE      FALSE      0     0     0     0.69
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, PTEN, KMT2D, PIK3CA, SOX2
    ##     |-4 :: SETD2
    ##     | \-3 :: MGA
    ##     \-9 :: TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PTEN 
    ##    GL ---> KMT2D 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    SETD2 ---> MGA 
    ##    TP53 ---> SETD2 
    ##    PTEN ---> SETD2 
    ##    KMT2D ---> SETD2 
    ##    PIK3CA ---> SETD2 
    ##    SOX2 ---> SETD2 
    ##    TP53 ---> TERT 
    ##    PTEN ---> TERT 
    ##    KMT2D ---> TERT 
    ##    PIK3CA ---> TERT 
    ##    SOX2 ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0069
    ## $phylogenies$CRUK0069$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0069 ] 
    ## 
    ## # A tibble: 2 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1     1     1   
    ## 2 13          1 TRUE      FALSE      0.93  0.42  0.32  0.94  0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, PDGFRA, FGFR1
    ##     \-13 :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> PDGFRA 
    ##    GL ---> FGFR1 
    ##    TP53 ---> KRAS 
    ##    FAT1 ---> KRAS 
    ##    PDGFRA ---> KRAS 
    ##    FGFR1 ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0070
    ## $phylogenies$CRUK0070$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0070 ] 
    ## 
    ## # A tibble: 3 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1     1     1   
    ## 2 2           1 TRUE      FALSE      0     0     0     0.95  0.98
    ## 3 3           1 TRUE      FALSE      0.95  0.96  0.98  0     0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: DNM2, TP53, COL5A2, SOX2
    ##     |-3 :: NFE2L2
    ##     \-2 :: CBLB
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> DNM2 
    ##    GL ---> TP53 
    ##    GL ---> COL5A2 
    ##    GL ---> SOX2 
    ##    DNM2 ---> CBLB 
    ##    TP53 ---> CBLB 
    ##    COL5A2 ---> CBLB 
    ##    SOX2 ---> CBLB 
    ##    DNM2 ---> NFE2L2 
    ##    TP53 ---> NFE2L2 
    ##    COL5A2 ---> NFE2L2 
    ##    SOX2 ---> NFE2L2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0071
    ## $phylogenies$CRUK0071$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0071 ] 
    ## 
    ## # A tibble: 2 x 10
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1 0.99      1     1     1     1
    ## 2 4           1 TRUE      FALSE         0 0.570     0     0     0     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3, R5, R6, R7] :: CMTR2, PIK3CA, SOX2
    ##     \-4 :: UBR5
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CMTR2 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    CMTR2 ---> UBR5 
    ##    PIK3CA ---> UBR5 
    ##    SOX2 ---> UBR5 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0072
    ## $phylogenies$CRUK0072$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0072 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.99  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R4] :: TP53, NFE2L2, PIK3CA, SOX2, EGFR, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> NFE2L2 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> EGFR 
    ##    GL ---> MYC 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0073
    ## $phylogenies$CRUK0073$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0073 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1  1   
    ## 2 2           1 TRUE      FALSE         0  0.93
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: CDKN2A, DICER1, NFE2L2, FAT1, KMT2D, NOTCH2, FGFR1, MYC
    ##     \-2 :: PLXNB2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> DICER1 
    ##    GL ---> NFE2L2 
    ##    GL ---> FAT1 
    ##    GL ---> KMT2D 
    ##    GL ---> NOTCH2 
    ##    GL ---> FGFR1 
    ##    GL ---> MYC 
    ##    CDKN2A ---> PLXNB2 
    ##    DICER1 ---> PLXNB2 
    ##    NFE2L2 ---> PLXNB2 
    ##    FAT1 ---> PLXNB2 
    ##    KMT2D ---> PLXNB2 
    ##    NOTCH2 ---> PLXNB2 
    ##    FGFR1 ---> PLXNB2 
    ##    MYC ---> PLXNB2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0074
    ## $phylogenies$CRUK0074$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0074 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1   
    ## 2 3           1 TRUE      FALSE      0     0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: TP53, NFE2L2, PIK3CA, SOX2, CCND1
    ##     \-3 :: UBR5
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> NFE2L2 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> CCND1 
    ##    TP53 ---> UBR5 
    ##    NFE2L2 ---> UBR5 
    ##    PIK3CA ---> UBR5 
    ##    SOX2 ---> UBR5 
    ##    CCND1 ---> UBR5 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0075
    ## $phylogenies$CRUK0075$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0075 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       1     0.99
    ## 2 2           1 TRUE      FALSE      0.15  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: NOTCH1, RASA1, TP53, FAT1, MGA, PIK3CA, FGFR1
    ##     \-2 :: NFE2L2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> NOTCH1 
    ##    GL ---> RASA1 
    ##    GL ---> TP53 
    ##    GL ---> FAT1 
    ##    GL ---> MGA 
    ##    GL ---> PIK3CA 
    ##    GL ---> FGFR1 
    ##    NOTCH1 ---> NFE2L2 
    ##    RASA1 ---> NFE2L2 
    ##    TP53 ---> NFE2L2 
    ##    FAT1 ---> NFE2L2 
    ##    MGA ---> NFE2L2 
    ##    PIK3CA ---> NFE2L2 
    ##    FGFR1 ---> NFE2L2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0076
    ## $phylogenies$CRUK0076$`1`
    ##  [ ctree - ctree rank 1/3 for CRUK0076 ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       1        1  1        1
    ## 2 2           1 TRUE      FALSE      0.93     0  0.28     0
    ## 3 3           1 TRUE      FALSE      0.93     0  0.81     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R4] :: SERPINB13, TP53, ARID1B, PIK3CA, SOX2, FGFR1
    ##     \-3 :: COL5A2
    ##      \-2 :: NCOR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SERPINB13 
    ##    GL ---> TP53 
    ##    GL ---> ARID1B 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ##    COL5A2 ---> NCOR1 
    ##    SERPINB13 ---> COL5A2 
    ##    TP53 ---> COL5A2 
    ##    ARID1B ---> COL5A2 
    ##    PIK3CA ---> COL5A2 
    ##    SOX2 ---> COL5A2 
    ##    FGFR1 ---> COL5A2 
    ## 
    ## Tree score 0.444444444444444 
    ## 
    ## $phylogenies$CRUK0076$`2`
    ##  [ ctree - ctree rank 2/3 for CRUK0076 ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       1        1  1        1
    ## 2 2           1 TRUE      FALSE      0.93     0  0.28     0
    ## 3 3           1 TRUE      FALSE      0.93     0  0.81     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R4] :: SERPINB13, TP53, ARID1B, PIK3CA, SOX2, FGFR1
    ##     |-2 :: NCOR1
    ##     \-3 :: COL5A2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SERPINB13 
    ##    GL ---> TP53 
    ##    GL ---> ARID1B 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ##    SERPINB13 ---> NCOR1 
    ##    TP53 ---> NCOR1 
    ##    ARID1B ---> NCOR1 
    ##    PIK3CA ---> NCOR1 
    ##    SOX2 ---> NCOR1 
    ##    FGFR1 ---> NCOR1 
    ##    SERPINB13 ---> COL5A2 
    ##    TP53 ---> COL5A2 
    ##    ARID1B ---> COL5A2 
    ##    PIK3CA ---> COL5A2 
    ##    SOX2 ---> COL5A2 
    ##    FGFR1 ---> COL5A2 
    ## 
    ## Tree score 0.111111111111111 
    ## 
    ## $phylogenies$CRUK0076$`3`
    ##  [ ctree - ctree rank 3/3 for CRUK0076 ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       1        1  1        1
    ## 2 2           1 TRUE      FALSE      0.93     0  0.28     0
    ## 3 3           1 TRUE      FALSE      0.93     0  0.81     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R4] :: SERPINB13, TP53, ARID1B, PIK3CA, SOX2, FGFR1
    ##     \-2 :: NCOR1
    ##      \-3 :: COL5A2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SERPINB13 
    ##    GL ---> TP53 
    ##    GL ---> ARID1B 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ##    SERPINB13 ---> NCOR1 
    ##    TP53 ---> NCOR1 
    ##    ARID1B ---> NCOR1 
    ##    PIK3CA ---> NCOR1 
    ##    SOX2 ---> NCOR1 
    ##    FGFR1 ---> NCOR1 
    ##    NCOR1 ---> COL5A2 
    ## 
    ## Tree score 0.0833333333333333 
    ## 
    ## 
    ## $phylogenies$CRUK0077
    ## $phylogenies$CRUK0077$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0077 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: TP53, LATS1, KEAP1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> LATS1 
    ##    GL ---> KEAP1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0078
    ## $phylogenies$CRUK0078$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0078 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R3, R4] :: PLXNB2, PTEN, PIK3CA, SOX2, FGFR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PLXNB2 
    ##    GL ---> PTEN 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0079
    ## $phylogenies$CRUK0079$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0079 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.99     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: FAT1, TP53, POLE, PIK3CA, SOX2, FGFR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> FAT1 
    ##    GL ---> TP53 
    ##    GL ---> POLE 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0080
    ## $phylogenies$CRUK0080$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0080 ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1  1     1   
    ## 2 3           1 TRUE      FALSE         0     0  0.97  0.83
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3, R4] :: TP53, WT1, EGFR, CCND1
    ##     \-3 :: IKZF1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> WT1 
    ##    GL ---> EGFR 
    ##    GL ---> CCND1 
    ##    TP53 ---> IKZF1 
    ##    WT1 ---> IKZF1 
    ##    EGFR ---> IKZF1 
    ##    CCND1 ---> IKZF1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0081
    ## $phylogenies$CRUK0081$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0081 ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       1     0.99
    ## 2 3           1 TRUE      FALSE      0.93  0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: NOTCH1, TP53, CDKN2A, FAT1, FANCC
    ##     \-3 :: CYLD
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> NOTCH1 
    ##    GL ---> TP53 
    ##    GL ---> CDKN2A 
    ##    GL ---> FAT1 
    ##    GL ---> FANCC 
    ##    NOTCH1 ---> CYLD 
    ##    TP53 ---> CYLD 
    ##    CDKN2A ---> CYLD 
    ##    FAT1 ---> CYLD 
    ##    FANCC ---> CYLD 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0082
    ## $phylogenies$CRUK0082$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0082 ] 
    ## 
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1     1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4, R5] :: TP53, WT1, PTEN, COL5A2, KMT2D, PIK3CA, SOX2, FGFR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> WT1 
    ##    GL ---> PTEN 
    ##    GL ---> COL5A2 
    ##    GL ---> KMT2D 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0083
    ## $phylogenies$CRUK0083$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0083 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE          1     1     1  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: TP53, FBXW7, RASA1, PIK3CA, SOX2, FGFR1, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> FBXW7 
    ##    GL ---> RASA1 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ##    GL ---> MYC 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0084
    ## $phylogenies$CRUK0084$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0084 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE          1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: CREBBP
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CREBBP 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0085
    ## $phylogenies$CRUK0085$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0085 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: CHEK2, CREBBP, LATS1, FANCM
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CHEK2 
    ##    GL ---> CREBBP 
    ##    GL ---> LATS1 
    ##    GL ---> FANCM 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0086
    ## $phylogenies$CRUK0086$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0086 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R4] :: TP53, ARID2, FAT1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> ARID2 
    ##    GL ---> FAT1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0087
    ## $phylogenies$CRUK0087$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0087 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: NFE2L2, TP53, ASXL1, PIK3CA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> NFE2L2 
    ##    GL ---> TP53 
    ##    GL ---> ASXL1 
    ##    GL ---> PIK3CA 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0088
    ## $phylogenies$CRUK0088$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0088 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: CUX1, TP53
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CUX1 
    ##    GL ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0089
    ## $phylogenies$CRUK0089$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0089 ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           3 TRUE      TRUE       0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2] :: PIK3CA, SMAD4, KEAP1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> SMAD4 
    ##    GL ---> KEAP1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0090
    ## $phylogenies$CRUK0090$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0090 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: CDKN2A, NCOA6, CUX1, COL2A1, NRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> NCOA6 
    ##    GL ---> CUX1 
    ##    GL ---> COL2A1 
    ##    GL ---> NRAS 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0091
    ## $phylogenies$CRUK0091$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0091 ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           3 TRUE      TRUE          1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2] :: TP53, SMARCA4, CDKN2A
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> SMARCA4 
    ##    GL ---> CDKN2A 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0092
    ## $phylogenies$CRUK0092$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0092 ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           5 TRUE      TRUE          1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: TP53, SMAD4, RASA1, CBLB, PIK3CA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> SMAD4 
    ##    GL ---> RASA1 
    ##    GL ---> CBLB 
    ##    GL ---> PIK3CA 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0093
    ## $phylogenies$CRUK0093$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0093 ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           7 TRUE      TRUE       0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: DICER1, CDKN2A, COL2A1, GATA3, CIC, COL5A2, TP53
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> DICER1 
    ##    GL ---> CDKN2A 
    ##    GL ---> COL2A1 
    ##    GL ---> GATA3 
    ##    GL ---> CIC 
    ##    GL ---> COL5A2 
    ##    GL ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0094
    ## $phylogenies$CRUK0094$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0094 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.98  0.97  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: SMARCA4, TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SMARCA4 
    ##    GL ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0095
    ## $phylogenies$CRUK0095$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0095 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99  0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: TP53, NF1, RASA1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> NF1 
    ##    GL ---> RASA1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0096
    ## $phylogenies$CRUK0096$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0096 ] 
    ## 
    ## # A tibble: 1 x 11
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1     1     1     1
    ## # … with 1 more variable: R7 <dbl>
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4, R5, R6, R7] :: KRAS, SGK223, MAP3K1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> SGK223 
    ##    GL ---> MAP3K1 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0097
    ## $phylogenies$CRUK0097$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0097 ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE      0.995  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: TP53, PTEN
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PTEN 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0098
    ## $phylogenies$CRUK0098$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0098 ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       1     1        1
    ## 2 3           1 TRUE      FALSE      0.96  0.91     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3] :: TP53, PTEN
    ##     \-3 :: UBR5
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PTEN 
    ##    TP53 ---> UBR5 
    ##    PTEN ---> UBR5 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0099
    ## $phylogenies$CRUK0099$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0099 ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R3    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.95  0.97  0.91     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3, R6, R7] :: STK11, KEAP1, TP53
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    GL ---> KEAP1 
    ##    GL ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $phylogenies$CRUK0100
    ## $phylogenies$CRUK0100$`1`
    ##  [ ctree - ctree rank 1/1 for CRUK0100 ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: TP53, PHOX2B, COL5A2, STK11, SPEN, CDKN2A
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PHOX2B 
    ##    GL ---> COL5A2 
    ##    GL ---> STK11 
    ##    GL ---> SPEN 
    ##    GL ---> CDKN2A 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## 
    ## $fit
    ## $fit$fit_table
    ## # A tibble: 99 x 9
    ##    patientID hasTrees numTrees maxScore minScore combInfTransf Solution
    ##    <chr>     <lgl>       <int>    <dbl>    <dbl>         <int>    <int>
    ##  1 CRUK0001  TRUE            3    0.111   0.111              3        1
    ##  2 CRUK0002  TRUE            2    0.75    0.0833             2        1
    ##  3 CRUK0003  TRUE            1    1       1                  1        1
    ##  4 CRUK0004  TRUE            1    1       1                  1        1
    ##  5 CRUK0005  TRUE            1    1       1                  1        1
    ##  6 CRUK0006  TRUE            2    0.667   0.167              2        1
    ##  7 CRUK0007  TRUE            1    1       1                  1        1
    ##  8 CRUK0008  TRUE            1    1       1                  1        1
    ##  9 CRUK0009  TRUE            1    1       1                  1        1
    ## 10 CRUK0010  TRUE            1    1       1                  1        1
    ## # … with 89 more rows, and 2 more variables: converged <lgl>,
    ## #   penalty <dbl>
    ## 
    ## $fit$penalty
    ## # A tibble: 262 x 4
    ##    from     to     count penalty
    ##    <chr>    <chr>  <int>   <dbl>
    ##  1 ARHGAP35 TERT       2  0.08  
    ##  2 ARID1B   ASXL1      1  0.333 
    ##  3 ARID1B   COL5A2     1  0.0455
    ##  4 ARID1B   KRAS       1  0.0222
    ##  5 ARID2    KRAS       2  0.0444
    ##  6 ATM      CCND1      1  0.125 
    ##  7 ATM      MGA        1  0.1   
    ##  8 ATM      NCOR1      1  0.125 
    ##  9 BAP1     PIK3CA     1  0.0476
    ## 10 BAP1     RB1        1  0.2   
    ## # … with 252 more rows
    ## 
    ## $fit$phylogenies
    ## $fit$phylogenies$CRUK0001
    ##  [ ctree - ctree rank 1/3 for CRUK0001 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 3           4 TRUE      TRUE       0.99  0.99  1   
    ## 2 1           1 TRUE      FALSE      0.86  0     0   
    ## 3 2           1 TRUE      FALSE      0.19  0     0.95
    ## 4 5           1 TRUE      FALSE      0.82  0     0.71
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-3 [R2] :: TP53, MGA, WRN, EGFR
    ##     |-1 :: NF1
    ##     | \-5 :: PASK
    ##     \-2 :: ARHGAP35
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> WRN 
    ##    GL ---> MGA 
    ##    EGFR ---> TP53 
    ##    WRN ---> TP53 
    ##    TP53 ---> NF1 
    ##    MGA ---> NF1 
    ##    TP53 ---> ARHGAP35 
    ##    MGA ---> ARHGAP35 
    ##    NF1 ---> PASK 
    ## 
    ## Tree score 0.111111111111111 
    ## 
    ## $fit$phylogenies$CRUK0002
    ##  [ ctree - ctree rank 1/2 for CRUK0002 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      FALSE      0     0.92  0   
    ## 2 2           2 TRUE      TRUE       0.99  0.98  0.99
    ## 3 5           1 TRUE      FALSE      0.78  0     0   
    ## 4 6           1 TRUE      FALSE      0.96  0.03  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 :: MET, TERT
    ##     |-6 :: EP300
    ##     | \-5 :: NF1
    ##     \-1 :: RB1, IKZF1, KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> MET 
    ##    MET ---> TERT 
    ##    TERT ---> EP300 
    ##    TERT ---> RB1 
    ##    TERT ---> IKZF1 
    ##    TERT ---> KRAS 
    ##    EP300 ---> NF1 
    ## 
    ## Tree score 0.75 
    ## 
    ## $fit$phylogenies$CRUK0003
    ##  [ ctree - ctree rank 1/1 for CRUK0003 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.97  0.87  0.97  0.99
    ## 2 4           1 TRUE      FALSE      0     0     0.49  0     0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R4] :: PIK3CA, EGFR, CDKN2A
    ##     \-4 :: CTNNB1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> EGFR 
    ##    GL ---> CDKN2A 
    ##    PIK3CA ---> CTNNB1 
    ##    EGFR ---> CTNNB1 
    ##    CDKN2A ---> CTNNB1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0004
    ##  [ ctree - ctree rank 1/1 for CRUK0004 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      FALSE      0    0      0.95  0.01
    ## 2 2           2 TRUE      TRUE       0.99 0.985  0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R1, R2] :: TP53, EGFR
    ##     \-1 :: SMAD4, NOTCH1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    EGFR ---> TP53 
    ##    TP53 ---> SMAD4 
    ##    TP53 ---> NOTCH1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0005
    ##  [ ctree - ctree rank 1/1 for CRUK0005 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 2           5 TRUE      TRUE          1     1  0.97     1
    ## 2 1           1 TRUE      FALSE         0     0  0.8      0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R1, R2, R4] :: CMTR2, TP53, BRAF, PASK, TERT
    ##     \-1 :: NRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> BRAF 
    ##    GL ---> TP53 
    ##    GL ---> CMTR2 
    ##    GL ---> PASK 
    ##    BRAF ---> TERT 
    ##    TP53 ---> TERT 
    ##    CMTR2 ---> NRAS 
    ##    PASK ---> NRAS 
    ##    TERT ---> NRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0006
    ##  [ ctree - ctree rank 1/2 for CRUK0006 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 3 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1   
    ## 2 2           1 TRUE      FALSE      0     0.93
    ## 3 7           1 TRUE      FALSE      0.99  0.06
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: PLXNB2, TP53, KEAP1, TERT
    ##     |-7 :: FANCC
    ##     \-2 :: MAP3K1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> KEAP1 
    ##    TP53 ---> PLXNB2 
    ##    TP53 ---> TERT 
    ##    PLXNB2 ---> MAP3K1 
    ##    KEAP1 ---> MAP3K1 
    ##    TERT ---> MAP3K1 
    ##    PLXNB2 ---> FANCC 
    ##    KEAP1 ---> FANCC 
    ##    TERT ---> FANCC 
    ## 
    ## Tree score 0.666666666666667 
    ## 
    ## $fit$phylogenies$CRUK0007
    ##  [ ctree - ctree rank 1/1 for CRUK0007 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.93
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: PIK3CA, EGFR, SGK223
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> EGFR 
    ##    GL ---> SGK223 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0008
    ##  [ ctree - ctree rank 1/1 for CRUK0008 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 2           5 TRUE      TRUE       0.99     1
    ## 2 3           1 TRUE      FALSE      0.86     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R2] :: KEAP1, STK11, PRDM1, U2AF1, MYC
    ##     \-3 :: ARID2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> STK11 
    ##    GL ---> PRDM1 
    ##    GL ---> U2AF1 
    ##    GL ---> MYC 
    ##    KEAP1 ---> ARID2 
    ##    STK11 ---> ARID2 
    ##    PRDM1 ---> ARID2 
    ##    U2AF1 ---> ARID2 
    ##    MYC ---> ARID2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0009
    ##  [ ctree - ctree rank 1/1 for CRUK0009 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99  0.98  0.99
    ## 2 2           1 TRUE      FALSE      0     0.93  0     0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: BRAF, TP53, ARHGAP35, KMT2C, NFE2L2, MET
    ##     \-2 :: TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> BRAF 
    ##    GL ---> KMT2C 
    ##    GL ---> MET 
    ##    TP53 ---> ARHGAP35 
    ##    TP53 ---> NFE2L2 
    ##    BRAF ---> TERT 
    ##    ARHGAP35 ---> TERT 
    ##    KMT2C ---> TERT 
    ##    NFE2L2 ---> TERT 
    ##    MET ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0010
    ##  [ ctree - ctree rank 1/1 for CRUK0010 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.95  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: SETD2, EGFR, TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SETD2 
    ##    GL ---> EGFR 
    ##    GL ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0011
    ##  [ ctree - ctree rank 1/1 for CRUK0011 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.97     1
    ## 2 3           1 TRUE      FALSE      0.95  0        0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R3] :: KRAS
    ##     \-3 :: FLT4
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    KRAS ---> FLT4 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0012
    ##  [ ctree - ctree rank 1/1 for CRUK0012 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.98  0.95
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0013
    ##  [ ctree - ctree rank 1/4 for CRUK0013 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal   LN1   LN2    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99  0.99 0.99   0.99
    ## 2 2           1 TRUE      FALSE      0     0     0    0.75   0   
    ## 3 3           1 TRUE      FALSE      0.97  0.96  0.01 0.580  0.94
    ## 4 4           1 TRUE      FALSE      0     0     0.97 0.37   0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: STK11
    ##     |-3 :: KRAS
    ##     |-4 :: EGFR
    ##     \-2 :: NOTCH1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    STK11 ---> NOTCH1 
    ##    STK11 ---> KRAS 
    ##    STK11 ---> EGFR 
    ## 
    ## Tree score 0.3 
    ## 
    ## $fit$phylogenies$CRUK0014
    ##  [ ctree - ctree rank 1/1 for CRUK0014 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.96  0.96
    ## 2 2           1 TRUE      FALSE      0.35  0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, KRAS
    ##     \-2 :: RNF43
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    KRAS ---> TP53 
    ##    TP53 ---> KRAS 
    ##    KRAS ---> RNF43 
    ##    TP53 ---> RNF43 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0015
    ##  [ ctree - ctree rank 1/1 for CRUK0015 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 3 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.99
    ## 2 2           1 TRUE      FALSE      0.94  0.01
    ## 3 3           1 TRUE      FALSE      0.01  0.65
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: BAP1, EGFR
    ##     |-2 :: TP53
    ##     \-3 :: RB1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> BAP1 
    ##    GL ---> EGFR 
    ##    BAP1 ---> TP53 
    ##    EGFR ---> TP53 
    ##    BAP1 ---> RB1 
    ##    EGFR ---> RB1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0016
    ##  [ ctree - ctree rank 1/13 for CRUK0016 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 5 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       0.99  0.99
    ## 2 16          2 TRUE      FALSE      0.97  0   
    ## 3 10          1 TRUE      FALSE      0.34  0.3 
    ## 4 2           1 TRUE      FALSE      0.53  0   
    ## 5 6           1 TRUE      FALSE      0.31  0.53
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, SPEN, CBLB, TERT, CDKN2A
    ##     |-16 :: LATS1, ARID1B
    ##     | \-2 :: ASXL1
    ##     |-10 :: DNM2
    ##     \-6 :: PTPRC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> SPEN 
    ##    CDKN2A ---> TP53 
    ##    TP53 ---> FAT1 
    ##    TP53 ---> CBLB 
    ##    TP53 ---> TERT 
    ##    FAT1 ---> LATS1 
    ##    SPEN ---> LATS1 
    ##    CBLB ---> LATS1 
    ##    TERT ---> LATS1 
    ##    FAT1 ---> ARID1B 
    ##    SPEN ---> ARID1B 
    ##    CBLB ---> ARID1B 
    ##    TERT ---> ARID1B 
    ##    FAT1 ---> DNM2 
    ##    SPEN ---> DNM2 
    ##    CBLB ---> DNM2 
    ##    TERT ---> DNM2 
    ##    FAT1 ---> PTPRC 
    ##    SPEN ---> PTPRC 
    ##    CBLB ---> PTPRC 
    ##    TERT ---> PTPRC 
    ##    LATS1 ---> ASXL1 
    ##    ARID1B ---> ASXL1 
    ## 
    ## Tree score 0.03125 
    ## 
    ## $fit$phylogenies$CRUK0017
    ##  [ ctree - ctree rank 1/1 for CRUK0017 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1  1     1     1   
    ## 2 3           1 TRUE      FALSE         0  0.94  0.95  0.59
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: TP53, ARID1B, ARID2, KEAP1, MYC
    ##     \-3 :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> MYC 
    ##    GL ---> TP53 
    ##    KEAP1 ---> ARID2 
    ##    MYC ---> ARID2 
    ##    TP53 ---> ARID1B 
    ##    ARID1B ---> KRAS 
    ##    ARID2 ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0018
    ##  [ ctree - ctree rank 1/1 for CRUK0018 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: CMTR2, KRAS, MGA, COL5A2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> CMTR2 
    ##    GL ---> COL5A2 
    ##    KRAS ---> MGA 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0019
    ##  [ ctree - ctree rank 1/1 for CRUK0019 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.97  0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0020
    ##  [ ctree - ctree rank 1/2 for CRUK0020 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 4 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       1     1   
    ## 2 2           1 TRUE      FALSE      0.87  0   
    ## 3 3           1 TRUE      FALSE      0.9   0.08
    ## 4 4           1 TRUE      FALSE      0     0.85
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: KEAP1, TP53, MGA, ARID2, COL2A1, PRF1, KRAS
    ##     |-3 :: BAP1
    ##     | \-2 :: PIK3CA
    ##     \-4 :: NCOR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> COL2A1 
    ##    GL ---> PRF1 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    ARID2 ---> KRAS 
    ##    KEAP1 ---> ARID2 
    ##    KEAP1 ---> KRAS 
    ##    KRAS ---> TP53 
    ##    KRAS ---> MGA 
    ##    TP53 ---> KRAS 
    ##    MGA ---> BAP1 
    ##    COL2A1 ---> BAP1 
    ##    PRF1 ---> BAP1 
    ##    KRAS ---> BAP1 
    ##    TP53 ---> BAP1 
    ##    MGA ---> NCOR1 
    ##    COL2A1 ---> NCOR1 
    ##    PRF1 ---> NCOR1 
    ##    KRAS ---> NCOR1 
    ##    TP53 ---> NCOR1 
    ##    BAP1 ---> PIK3CA 
    ## 
    ## Tree score 0.666666666666667 
    ## 
    ## $fit$phylogenies$CRUK0021
    ##  [ ctree - ctree rank 1/1 for CRUK0021 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: EGFR, TP53, CHEK2, CDKN2A
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> EGFR 
    ##    GL ---> CHEK2 
    ##    CDKN2A ---> TP53 
    ##    EGFR ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0022
    ##  [ ctree - ctree rank 1/1 for CRUK0022 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.99
    ## 2 2           1 TRUE      FALSE      0.85  0   
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2] :: TP53, EGFR
    ##     \-2 :: CIC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    EGFR ---> TP53 
    ##    TP53 ---> CIC 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0023
    ##  [ ctree - ctree rank 1/1 for CRUK0023 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99 0.98   0.99  0.95
    ## 2 4           2 TRUE      FALSE      0.01 0.945  0     0   
    ## 3 2           1 TRUE      FALSE      0.81 0      0     0   
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3, R4] :: WRN, KRAS, CDKN2A
    ##     |-2 :: TP53
    ##     \-4 :: PTPRC, KMT2D
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> WRN 
    ##    GL ---> KRAS 
    ##    GL ---> CDKN2A 
    ##    WRN ---> PTPRC 
    ##    KRAS ---> PTPRC 
    ##    CDKN2A ---> PTPRC 
    ##    WRN ---> KMT2D 
    ##    KRAS ---> KMT2D 
    ##    CDKN2A ---> KMT2D 
    ##    WRN ---> TP53 
    ##    KRAS ---> TP53 
    ##    CDKN2A ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0024
    ##  [ ctree - ctree rank 1/1 for CRUK0024 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R3    R4    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1        1
    ## 2 3           1 TRUE      FALSE      0.88  0.97  0.95     0
    ## 3 4           1 TRUE      FALSE      0.83  0     0        0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R6] :: TP53, STK11, POLE, EGFR
    ##     \-3 :: ATM
    ##      \-4 :: NCOR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    GL ---> POLE 
    ##    EGFR ---> TP53 
    ##    STK11 ---> EGFR 
    ##    TP53 ---> ATM 
    ##    POLE ---> ATM 
    ##    ATM ---> NCOR1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0025
    ##  [ ctree - ctree rank 1/1 for CRUK0025 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: KRAS, TP53, MGA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    KRAS ---> TP53 
    ##    KRAS ---> MGA 
    ##    TP53 ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0026
    ##  [ ctree - ctree rank 1/1 for CRUK0026 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.98  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: TP53, EGFR, RB1, SERPINB13
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> SERPINB13 
    ##    EGFR ---> TP53 
    ##    EGFR ---> RB1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0027
    ##  [ ctree - ctree rank 1/1 for CRUK0027 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.96  1   
    ## 2 2           1 TRUE      FALSE      0     0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: KRAS, TP53
    ##     \-2 :: PLXNB2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    KRAS ---> TP53 
    ##    TP53 ---> KRAS 
    ##    KRAS ---> PLXNB2 
    ##    TP53 ---> PLXNB2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0028
    ##  [ ctree - ctree rank 1/1 for CRUK0028 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE      0.975  0.95
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: APC, EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> APC 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0029
    ##  [ ctree - ctree rank 1/1 for CRUK0029 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 10
    ##   cluster nMuts is.driver is.clonal    R2    R4    R5    R6    R7    R8
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99  0.98     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R4, R5, R6, R7, R8] :: TP53, NRAS, MGA, CCND1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> MGA 
    ##    GL ---> CCND1 
    ##    TP53 ---> NRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0030
    ##  [ ctree - ctree rank 1/1 for CRUK0030 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.98  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: KRAS, TSC2, U2AF1, TP53, FBXW7, NF1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TSC2 
    ##    GL ---> U2AF1 
    ##    GL ---> FBXW7 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    KRAS ---> TP53 
    ##    TP53 ---> KRAS 
    ##    TP53 ---> NF1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0031
    ##  [ ctree - ctree rank 1/1 for CRUK0031 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1        1
    ## 2 6           1 TRUE      FALSE      0.88  0.05     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3] :: KEAP1, CDKN2A, PRF1, FGFR1
    ##     \-6 :: NF1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> CDKN2A 
    ##    GL ---> PRF1 
    ##    GL ---> FGFR1 
    ##    KEAP1 ---> NF1 
    ##    CDKN2A ---> NF1 
    ##    PRF1 ---> NF1 
    ##    FGFR1 ---> NF1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0032
    ##  [ ctree - ctree rank 1/1 for CRUK0032 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  1        1  1   
    ## 2 4           1 TRUE      FALSE         0  0.97     0  0.98
    ## 3 6           1 TRUE      FALSE         0  0        0  0.3 
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: ATM, RAD21, U2AF1, RNF43
    ##     \-4 :: CCND1
    ##      \-6 :: ARID1B
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> ATM 
    ##    GL ---> RAD21 
    ##    GL ---> U2AF1 
    ##    GL ---> RNF43 
    ##    ATM ---> CCND1 
    ##    RAD21 ---> CCND1 
    ##    U2AF1 ---> CCND1 
    ##    RNF43 ---> CCND1 
    ##    CCND1 ---> ARID1B 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0033
    ##  [ ctree - ctree rank 1/1 for CRUK0033 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: KEAP1, CTNNB1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> CTNNB1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0034
    ##  [ ctree - ctree rank 1/1 for CRUK0034 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1   1       1
    ## 2 4           1 TRUE      FALSE         0   0.5     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: ATM, KRAS, PLXNB2
    ##     \-4 :: MGA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> ATM 
    ##    KRAS ---> PLXNB2 
    ##    ATM ---> MGA 
    ##    PLXNB2 ---> MGA 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0035
    ##  [ ctree - ctree rank 1/1 for CRUK0035 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal   LN1    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.98  0.99  0.99
    ## 2 4           1 TRUE      FALSE      0     0.8   0     0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [LN1, R2] :: TP53, FAS
    ##     \-4 :: FLT4
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    TP53 ---> FAS 
    ##    FAS ---> FLT4 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0036
    ##  [ ctree - ctree rank 1/1 for CRUK0036 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  0.98  0.97     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: KRAS, PIK3CA, KEAP1, ARHGAP35, TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> ARHGAP35 
    ##    GL ---> KEAP1 
    ##    GL ---> PIK3CA 
    ##    ARHGAP35 ---> TERT 
    ##    KEAP1 ---> KRAS 
    ##    PIK3CA ---> TERT 
    ##    TERT ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0037
    ##  [ ctree - ctree rank 1/1 for CRUK0037 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99     1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4, R5] :: NCOA6, CREBBP, KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> NCOA6 
    ##    GL ---> CREBBP 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0038
    ##  [ ctree - ctree rank 1/1 for CRUK0038 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99
    ## 2 3           1 TRUE      FALSE      0     0.38
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: KRAS
    ##     \-3 :: KMT2D
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    KRAS ---> KMT2D 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0039
    ##  [ ctree - ctree rank 1/1 for CRUK0039 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: KRAS, CMTR2, NF1, PHOX2B
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> CMTR2 
    ##    GL ---> NF1 
    ##    GL ---> PHOX2B 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0040
    ##  [ ctree - ctree rank 1/1 for CRUK0040 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.99  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: NCOR1, RAD21, KRAS, GATA3
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> RAD21 
    ##    GL ---> GATA3 
    ##    KRAS ---> NCOR1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0041
    ##  [ ctree - ctree rank 1/1 for CRUK0041 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.98  0.99  0.99  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: BRAF, TERT, EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> BRAF 
    ##    GL ---> EGFR 
    ##    BRAF ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0042
    ##  [ ctree - ctree rank 1/1 for CRUK0042 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           1 TRUE      TRUE       0.91
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0043
    ##  [ ctree - ctree rank 1/1 for CRUK0043 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: MET
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> MET 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0044
    ##  [ ctree - ctree rank 1/1 for CRUK0044 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0045
    ##  [ ctree - ctree rank 1/1 for CRUK0045 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.98  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: BAP1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> BAP1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0046
    ##  [ ctree - ctree rank 1/1 for CRUK0046 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1  0.98 0.995  0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: KEAP1, APC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> APC 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0047
    ##  [ ctree - ctree rank 1/1 for CRUK0047 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       0.99     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: STK11, APC, KRAS, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> MYC 
    ##    GL ---> STK11 
    ##    GL ---> APC 
    ##    MYC ---> KRAS 
    ##    STK11 ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0048
    ##  [ ctree - ctree rank 1/1 for CRUK0048 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: APC, PRDM1, ARHGAP35, TP53, BRAF, EGFR, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> APC 
    ##    GL ---> PRDM1 
    ##    GL ---> BRAF 
    ##    GL ---> MYC 
    ##    EGFR ---> TP53 
    ##    EGFR ---> ARHGAP35 
    ##    TP53 ---> ARHGAP35 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0049
    ##  [ ctree - ctree rank 1/1 for CRUK0049 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: RB1, TP53, COL2A1, EGFR, KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> COL2A1 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    EGFR ---> TP53 
    ##    EGFR ---> RB1 
    ##    KRAS ---> TP53 
    ##    TP53 ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0050
    ##  [ ctree - ctree rank 1/1 for CRUK0050 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99  0.99  0.99     1  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4, R5] :: KRAS, STK11, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> MYC 
    ##    GL ---> STK11 
    ##    MYC ---> KRAS 
    ##    STK11 ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0051
    ##  [ ctree - ctree rank 1/1 for CRUK0051 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1        1     1
    ## 2 3           1 TRUE      FALSE      0.97     0     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3, R4] :: KRAS, FBXW7, TP53, EGFR
    ##     \-3 :: EP300
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> FBXW7 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    EGFR ---> TP53 
    ##    KRAS ---> TP53 
    ##    TP53 ---> KRAS 
    ##    FBXW7 ---> EP300 
    ##    KRAS ---> EP300 
    ##    TP53 ---> EP300 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0052
    ##  [ ctree - ctree rank 1/1 for CRUK0052 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1     1  1   
    ## 2 2           1 TRUE      FALSE         0     0  0.86
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3] :: KMT2D, KRAS, NOTCH2, MGA, KEAP1, TP53, NF1, SGK223
    ##     \-2 :: UBR5
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KEAP1 
    ##    GL ---> NOTCH2 
    ##    GL ---> SGK223 
    ##    GL ---> KRAS 
    ##    GL ---> TP53 
    ##    KEAP1 ---> KRAS 
    ##    KEAP1 ---> NF1 
    ##    KRAS ---> MGA 
    ##    KRAS ---> TP53 
    ##    KRAS ---> KMT2D 
    ##    MGA ---> NF1 
    ##    TP53 ---> KRAS 
    ##    TP53 ---> NF1 
    ##    KMT2D ---> UBR5 
    ##    NOTCH2 ---> UBR5 
    ##    NF1 ---> UBR5 
    ##    SGK223 ---> UBR5 
    ##    KRAS ---> UBR5 
    ##    TP53 ---> UBR5 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0054
    ##  [ ctree - ctree rank 1/1 for CRUK0054 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0055
    ##  [ ctree - ctree rank 1/1 for CRUK0055 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           2 TRUE      TRUE       1   
    ## 2 2           1 TRUE      FALSE      0.32
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: FANCM, UBR5
    ##     \-2 :: FAT1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> FANCM 
    ##    GL ---> UBR5 
    ##    FANCM ---> FAT1 
    ##    UBR5 ---> FAT1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0056
    ##  [ ctree - ctree rank 1/1 for CRUK0056 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1  1     1   
    ## 2 3           1 TRUE      FALSE         0  0.12  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: RASA1, CREBBP
    ##     \-3 :: TP53
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> RASA1 
    ##    GL ---> CREBBP 
    ##    RASA1 ---> TP53 
    ##    CREBBP ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0057
    ##  [ ctree - ctree rank 1/1 for CRUK0057 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: KRAS, SMARCA4, TSC2, DNM2, TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TERT 
    ##    GL ---> SMARCA4 
    ##    GL ---> TSC2 
    ##    TERT ---> KRAS 
    ##    TERT ---> DNM2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0058
    ##  [ ctree - ctree rank 1/1 for CRUK0058 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: TP53, EGFR
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    EGFR ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0059
    ##  [ ctree - ctree rank 1/1 for CRUK0059 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0060
    ##  [ ctree - ctree rank 1/1 for CRUK0060 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1          11 TRUE      TRUE          1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: SERPINB13, ARID2, COL5A2, FANCM, PHOX2B, COL2A1, RASA1, NF1, NCOA6, NOTCH2, KMT2C
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> NCOA6 
    ##    GL ---> NF1 
    ##    GL ---> SERPINB13 
    ##    GL ---> ARID2 
    ##    GL ---> PHOX2B 
    ##    GL ---> COL2A1 
    ##    GL ---> RASA1 
    ##    GL ---> NOTCH2 
    ##    GL ---> KMT2C 
    ##    NCOA6 ---> COL5A2 
    ##    NF1 ---> FANCM 
    ##    SERPINB13 ---> COL5A2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0061
    ##  [ ctree - ctree rank 1/1 for CRUK0061 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE       0.99     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: STK11
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0062
    ##  [ ctree - ctree rank 1/2 for CRUK0062 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 4 x 11
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 4           4 TRUE      TRUE       0.99  0.99  0.98  0.97  0.99  0.99
    ## 2 1           1 TRUE      FALSE      0     0.01  0     0     0     0.94
    ## 3 16          1 TRUE      FALSE      0.93  0.86  0.08  0.02  0.12  0   
    ## 4 2           1 TRUE      FALSE      0.84  0.83  0.02  0     0     0   
    ## # … with 1 more variable: R7 <dbl>
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-4 :: TP53, PIK3CA, SOX2, CCND1
    ##     |-16 :: UBR5
    ##     | \-2 :: PLXNB2
    ##     \-1 :: FAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> CCND1 
    ##    TP53 ---> UBR5 
    ##    PIK3CA ---> UBR5 
    ##    SOX2 ---> UBR5 
    ##    CCND1 ---> UBR5 
    ##    TP53 ---> FAS 
    ##    PIK3CA ---> FAS 
    ##    SOX2 ---> FAS 
    ##    CCND1 ---> FAS 
    ##    UBR5 ---> PLXNB2 
    ## 
    ## Tree score 0.75 
    ## 
    ## $fit$phylogenies$CRUK0063
    ##  [ ctree - ctree rank 1/6 for CRUK0063 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 4 x 9
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 2           7 TRUE      TRUE       0.93  0.99  0.99  0.99  1   
    ## 2 1           2 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 3 10          1 TRUE      FALSE      0     0.99  0.99  0.98  1   
    ## 4 6           1 TRUE      FALSE      0     0.02  0.7   0.36  0.55
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 [R3] :: PIK3CA, TP53, FBXW7, CDKN2A, SOX2, TERT, PRF1
    ##     \-10 :: EP300
    ##      \-1 :: NF1, CYLD
    ##       \-6 :: FANCM
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FBXW7 
    ##    GL ---> PRF1 
    ##    CDKN2A ---> TP53 
    ##    PIK3CA ---> TERT 
    ##    SOX2 ---> TERT 
    ##    TP53 ---> TERT 
    ##    FBXW7 ---> EP300 
    ##    TERT ---> EP300 
    ##    PRF1 ---> EP300 
    ##    EP300 ---> NF1 
    ##    EP300 ---> CYLD 
    ##    NF1 ---> FANCM 
    ##    CYLD ---> FANCM 
    ## 
    ## Tree score 0.125 
    ## 
    ## $fit$phylogenies$CRUK0064
    ##  [ ctree - ctree rank 1/1 for CRUK0064 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 2           2 TRUE      FALSE      0.64  0.11
    ## 2 1           1 TRUE      TRUE       1     1   
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53
    ##     \-2 :: MLH1, FAT1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    TP53 ---> MLH1 
    ##    TP53 ---> FAT1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0065
    ##  [ ctree - ctree rank 1/1 for CRUK0065 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 3 x 10
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1  0.99  0.99     1  1     1   
    ## 2 2           3 TRUE      FALSE         0  0     0        0  0.48  0   
    ## 3 6           2 TRUE      FALSE         0  0     0        0  0.01  0.83
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: TP53, NFE2L2, PIK3CA, SOX2
    ##     |-2 :: MLH1, PTPRC, UBR5
    ##     \-6 :: NOTCH1, NCOA6
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> TP53 
    ##    PIK3CA ---> NFE2L2 
    ##    SOX2 ---> NFE2L2 
    ##    TP53 ---> NFE2L2 
    ##    NFE2L2 ---> MLH1 
    ##    NFE2L2 ---> PTPRC 
    ##    NFE2L2 ---> UBR5 
    ##    NFE2L2 ---> NOTCH1 
    ##    NFE2L2 ---> NCOA6 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0066
    ##  [ ctree - ctree rank 1/1 for CRUK0066 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       0.99  1     1     0.99
    ## 2 9           1 TRUE      FALSE      0     0.91  0.01  0   
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R4] :: TP53, NOTCH1, CDKN2A, WRN, PDGFRA, TERT, NCOA6
    ##     \-9 :: COL5A2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> WRN 
    ##    GL ---> PDGFRA 
    ##    CDKN2A ---> TP53 
    ##    TP53 ---> NOTCH1 
    ##    TP53 ---> TERT 
    ##    TP53 ---> NCOA6 
    ##    WRN ---> TP53 
    ##    NOTCH1 ---> COL5A2 
    ##    PDGFRA ---> COL5A2 
    ##    TERT ---> COL5A2 
    ##    NCOA6 ---> COL5A2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0067
    ##  [ ctree - ctree rank 1/1 for CRUK0067 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1   
    ## 2 2           1 TRUE      FALSE      0.61  0.83
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: NOTCH1, TP53, PIK3CA, SOX2, CDKN2A
    ##     \-2 :: NFE2L2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    CDKN2A ---> TP53 
    ##    PIK3CA ---> NOTCH1 
    ##    SOX2 ---> NOTCH1 
    ##    TP53 ---> NOTCH1 
    ##    NOTCH1 ---> NFE2L2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0068
    ##  [ ctree - ctree rank 1/1 for CRUK0068 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 4 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1     1     1   
    ## 2 3           1 TRUE      FALSE      0.5   0     0     0   
    ## 3 4           1 TRUE      FALSE      0.98  0.37  0.99  0.01
    ## 4 9           1 TRUE      FALSE      0     0     0     0.69
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, PTEN, KMT2D, PIK3CA, SOX2
    ##     |-4 :: SETD2
    ##     | \-3 :: MGA
    ##     \-9 :: TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PTEN 
    ##    GL ---> KMT2D 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    TP53 ---> SETD2 
    ##    PTEN ---> SETD2 
    ##    KMT2D ---> SETD2 
    ##    PIK3CA ---> SETD2 
    ##    SOX2 ---> SETD2 
    ##    TP53 ---> TERT 
    ##    PTEN ---> TERT 
    ##    KMT2D ---> TERT 
    ##    PIK3CA ---> TERT 
    ##    SOX2 ---> TERT 
    ##    SETD2 ---> MGA 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0069
    ##  [ ctree - ctree rank 1/1 for CRUK0069 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1     1     1   
    ## 2 13          1 TRUE      FALSE      0.93  0.42  0.32  0.94  0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: TP53, FAT1, PDGFRA, FGFR1
    ##     \-13 :: KRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PDGFRA 
    ##    GL ---> FGFR1 
    ##    TP53 ---> FAT1 
    ##    FAT1 ---> KRAS 
    ##    PDGFRA ---> KRAS 
    ##    FGFR1 ---> KRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0070
    ##  [ ctree - ctree rank 1/1 for CRUK0070 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 3 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE       1     1     1     1     1   
    ## 2 2           1 TRUE      FALSE      0     0     0     0.95  0.98
    ## 3 3           1 TRUE      FALSE      0.95  0.96  0.98  0     0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: DNM2, TP53, COL5A2, SOX2
    ##     |-3 :: NFE2L2
    ##     \-2 :: CBLB
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SOX2 
    ##    GL ---> TP53 
    ##    SOX2 ---> COL5A2 
    ##    TP53 ---> DNM2 
    ##    TP53 ---> COL5A2 
    ##    DNM2 ---> CBLB 
    ##    COL5A2 ---> CBLB 
    ##    DNM2 ---> NFE2L2 
    ##    COL5A2 ---> NFE2L2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0071
    ##  [ ctree - ctree rank 1/1 for CRUK0071 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 10
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R5    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1 0.99      1     1     1     1
    ## 2 4           1 TRUE      FALSE         0 0.570     0     0     0     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3, R5, R6, R7] :: CMTR2, PIK3CA, SOX2
    ##     \-4 :: UBR5
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CMTR2 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    CMTR2 ---> UBR5 
    ##    PIK3CA ---> UBR5 
    ##    SOX2 ---> UBR5 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0072
    ##  [ ctree - ctree rank 1/1 for CRUK0072 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.99  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R4] :: TP53, NFE2L2, PIK3CA, SOX2, EGFR, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> MYC 
    ##    EGFR ---> TP53 
    ##    PIK3CA ---> NFE2L2 
    ##    SOX2 ---> NFE2L2 
    ##    TP53 ---> NFE2L2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0073
    ##  [ ctree - ctree rank 1/1 for CRUK0073 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1  1   
    ## 2 2           1 TRUE      FALSE         0  0.93
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: CDKN2A, DICER1, NFE2L2, FAT1, KMT2D, NOTCH2, FGFR1, MYC
    ##     \-2 :: PLXNB2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> FAT1 
    ##    GL ---> FGFR1 
    ##    GL ---> DICER1 
    ##    GL ---> NOTCH2 
    ##    GL ---> MYC 
    ##    CDKN2A ---> NFE2L2 
    ##    CDKN2A ---> KMT2D 
    ##    FAT1 ---> NFE2L2 
    ##    FGFR1 ---> NFE2L2 
    ##    DICER1 ---> PLXNB2 
    ##    NFE2L2 ---> PLXNB2 
    ##    KMT2D ---> PLXNB2 
    ##    NOTCH2 ---> PLXNB2 
    ##    MYC ---> PLXNB2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0074
    ##  [ ctree - ctree rank 1/1 for CRUK0074 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       0.99  1   
    ## 2 3           1 TRUE      FALSE      0     0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: TP53, NFE2L2, PIK3CA, SOX2, CCND1
    ##     \-3 :: UBR5
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> TP53 
    ##    GL ---> CCND1 
    ##    PIK3CA ---> NFE2L2 
    ##    SOX2 ---> NFE2L2 
    ##    TP53 ---> NFE2L2 
    ##    NFE2L2 ---> UBR5 
    ##    CCND1 ---> UBR5 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0075
    ##  [ ctree - ctree rank 1/1 for CRUK0075 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE       1     0.99
    ## 2 2           1 TRUE      FALSE      0.15  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: NOTCH1, RASA1, TP53, FAT1, MGA, PIK3CA, FGFR1
    ##     \-2 :: NFE2L2
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> RASA1 
    ##    GL ---> MGA 
    ##    GL ---> FGFR1 
    ##    PIK3CA ---> NOTCH1 
    ##    RASA1 ---> TP53 
    ##    TP53 ---> NOTCH1 
    ##    TP53 ---> FAT1 
    ##    NOTCH1 ---> NFE2L2 
    ##    FAT1 ---> NFE2L2 
    ##    MGA ---> NFE2L2 
    ##    FGFR1 ---> NFE2L2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0076
    ##  [ ctree - ctree rank 1/3 for CRUK0076 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 3 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE       1        1  1        1
    ## 2 2           1 TRUE      FALSE      0.93     0  0.28     0
    ## 3 3           1 TRUE      FALSE      0.93     0  0.81     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R4] :: SERPINB13, TP53, ARID1B, PIK3CA, SOX2, FGFR1
    ##     \-3 :: COL5A2
    ##      \-2 :: NCOR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> SERPINB13 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ##    TP53 ---> ARID1B 
    ##    SERPINB13 ---> COL5A2 
    ##    ARID1B ---> COL5A2 
    ##    PIK3CA ---> COL5A2 
    ##    SOX2 ---> COL5A2 
    ##    FGFR1 ---> COL5A2 
    ##    COL5A2 ---> NCOR1 
    ## 
    ## Tree score 0.444444444444444 
    ## 
    ## $fit$phylogenies$CRUK0077
    ##  [ ctree - ctree rank 1/1 for CRUK0077 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: TP53, LATS1, KEAP1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> KEAP1 
    ##    TP53 ---> LATS1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0078
    ##  [ ctree - ctree rank 1/1 for CRUK0078 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2, R3, R4] :: PLXNB2, PTEN, PIK3CA, SOX2, FGFR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> FGFR1 
    ##    GL ---> PTEN 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    FGFR1 ---> PLXNB2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0079
    ##  [ ctree - ctree rank 1/1 for CRUK0079 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1  0.99     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: FAT1, TP53, POLE, PIK3CA, SOX2, FGFR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> POLE 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ##    TP53 ---> FAT1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0080
    ##  [ ctree - ctree rank 1/1 for CRUK0080 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 8
    ##   cluster nMuts is.driver is.clonal    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1  1     1   
    ## 2 3           1 TRUE      FALSE         0     0  0.97  0.83
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3, R4] :: TP53, WT1, EGFR, CCND1
    ##     \-3 :: IKZF1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> WT1 
    ##    GL ---> CCND1 
    ##    EGFR ---> TP53 
    ##    TP53 ---> IKZF1 
    ##    WT1 ---> IKZF1 
    ##    CCND1 ---> IKZF1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0081
    ##  [ ctree - ctree rank 1/1 for CRUK0081 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE       1     0.99
    ## 2 3           1 TRUE      FALSE      0.93  0.01
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 :: NOTCH1, TP53, CDKN2A, FAT1, FANCC
    ##     \-3 :: CYLD
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    CDKN2A ---> TP53 
    ##    TP53 ---> NOTCH1 
    ##    TP53 ---> FAT1 
    ##    TP53 ---> FANCC 
    ##    NOTCH1 ---> CYLD 
    ##    FAT1 ---> CYLD 
    ##    FANCC ---> CYLD 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0082
    ##  [ ctree - ctree rank 1/1 for CRUK0082 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 9
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           8 TRUE      TRUE          1     1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4, R5] :: TP53, WT1, PTEN, COL5A2, KMT2D, PIK3CA, SOX2, FGFR1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> FGFR1 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> TP53 
    ##    GL ---> WT1 
    ##    GL ---> PTEN 
    ##    GL ---> KMT2D 
    ##    FGFR1 ---> COL5A2 
    ##    PIK3CA ---> COL5A2 
    ##    SOX2 ---> COL5A2 
    ##    TP53 ---> COL5A2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0083
    ##  [ ctree - ctree rank 1/1 for CRUK0083 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           7 TRUE      TRUE          1     1     1  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: TP53, FBXW7, RASA1, PIK3CA, SOX2, FGFR1, MYC
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> RASA1 
    ##    GL ---> FBXW7 
    ##    GL ---> PIK3CA 
    ##    GL ---> SOX2 
    ##    GL ---> FGFR1 
    ##    GL ---> MYC 
    ##    RASA1 ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0084
    ##  [ ctree - ctree rank 1/1 for CRUK0084 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           1 TRUE      TRUE          1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: CREBBP
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CREBBP 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0085
    ##  [ ctree - ctree rank 1/1 for CRUK0085 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: CHEK2, CREBBP, LATS1, FANCM
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CHEK2 
    ##    GL ---> CREBBP 
    ##    GL ---> LATS1 
    ##    GL ---> FANCM 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0086
    ##  [ ctree - ctree rank 1/1 for CRUK0086 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R4] :: TP53, ARID2, FAT1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> ARID2 
    ##    TP53 ---> FAT1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0087
    ##  [ ctree - ctree rank 1/1 for CRUK0087 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           4 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: NFE2L2, TP53, ASXL1, PIK3CA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> TP53 
    ##    GL ---> ASXL1 
    ##    PIK3CA ---> NFE2L2 
    ##    TP53 ---> NFE2L2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0088
    ##  [ ctree - ctree rank 1/1 for CRUK0088 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: CUX1, TP53
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CUX1 
    ##    GL ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0089
    ##  [ ctree - ctree rank 1/1 for CRUK0089 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           3 TRUE      TRUE       0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2] :: PIK3CA, SMAD4, KEAP1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> PIK3CA 
    ##    GL ---> SMAD4 
    ##    GL ---> KEAP1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0090
    ##  [ ctree - ctree rank 1/1 for CRUK0090 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           5 TRUE      TRUE          1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: CDKN2A, NCOA6, CUX1, COL2A1, NRAS
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> NCOA6 
    ##    GL ---> CUX1 
    ##    GL ---> COL2A1 
    ##    GL ---> NRAS 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0091
    ##  [ ctree - ctree rank 1/1 for CRUK0091 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           3 TRUE      TRUE          1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R2] :: TP53, SMARCA4, CDKN2A
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> SMARCA4 
    ##    CDKN2A ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0092
    ##  [ ctree - ctree rank 1/1 for CRUK0092 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           5 TRUE      TRUE          1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: TP53, SMAD4, RASA1, CBLB, PIK3CA
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> RASA1 
    ##    GL ---> PIK3CA 
    ##    RASA1 ---> TP53 
    ##    TP53 ---> SMAD4 
    ##    TP53 ---> CBLB 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0093
    ##  [ ctree - ctree rank 1/1 for CRUK0093 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 5
    ##   cluster nMuts is.driver is.clonal    R1
    ##   <chr>   <int> <lgl>     <lgl>     <dbl>
    ## 1 1           7 TRUE      TRUE       0.96
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1] :: DICER1, CDKN2A, COL2A1, GATA3, CIC, COL5A2, TP53
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> DICER1 
    ##    GL ---> COL2A1 
    ##    GL ---> GATA3 
    ##    CDKN2A ---> TP53 
    ##    CDKN2A ---> COL5A2 
    ##    TP53 ---> CIC 
    ##    TP53 ---> COL5A2 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0094
    ##  [ ctree - ctree rank 1/1 for CRUK0094 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       0.98  0.98  0.97  0.99
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4] :: SMARCA4, TERT
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> SMARCA4 
    ##    GL ---> TERT 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0095
    ##  [ ctree - ctree rank 1/1 for CRUK0095 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.99  0.99  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: TP53, NF1, RASA1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> RASA1 
    ##    RASA1 ---> TP53 
    ##    TP53 ---> NF1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0096
    ##  [ ctree - ctree rank 1/1 for CRUK0096 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 11
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3    R4    R5    R6
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE          1     1     1     1     1     1
    ## # … with 1 more variable: R7 <dbl>
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3, R4, R5, R6, R7] :: KRAS, SGK223, MAP3K1
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> KRAS 
    ##    GL ---> SGK223 
    ##    GL ---> MAP3K1 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0097
    ##  [ ctree - ctree rank 1/1 for CRUK0097 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 6
    ##   cluster nMuts is.driver is.clonal    R1    R2
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE      0.995  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2] :: TP53, PTEN
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PTEN 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0098
    ##  [ ctree - ctree rank 1/1 for CRUK0098 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 2 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           2 TRUE      TRUE       1     1        1
    ## 2 3           1 TRUE      FALSE      0.96  0.91     0
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R3] :: TP53, PTEN
    ##     \-3 :: UBR5
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> PTEN 
    ##    TP53 ---> UBR5 
    ##    PTEN ---> UBR5 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0099
    ##  [ ctree - ctree rank 1/1 for CRUK0099 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 8
    ##   cluster nMuts is.driver is.clonal    R1    R3    R6    R7
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      TRUE       0.95  0.97  0.91     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R3, R6, R7] :: STK11, KEAP1, TP53
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> STK11 
    ##    GL ---> KEAP1 
    ##    GL ---> TP53 
    ## 
    ## Tree score 1 
    ## 
    ## $fit$phylogenies$CRUK0100
    ##  [ ctree - ctree rank 1/1 for CRUK0100 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 1 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           6 TRUE      TRUE          1     1     1
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-1 [R1, R2, R3] :: TP53, PHOX2B, COL5A2, STK11, SPEN, CDKN2A
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> CDKN2A 
    ##    GL ---> PHOX2B 
    ##    GL ---> STK11 
    ##    GL ---> SPEN 
    ##    CDKN2A ---> TP53 
    ##    CDKN2A ---> COL5A2 
    ##    TP53 ---> COL5A2 
    ## 
    ## Tree score 1 
    ## 
    ## 
    ## $fit$clones_to_expand
    ## $fit$clones_to_expand$CRUK0001
    ## $fit$clones_to_expand$CRUK0001$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NF1    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0001$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster 
    ##   <chr>   
    ## 1 ARHGAP35
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0001$`3`
    ## # A tbl_graph: 4 nodes and 2 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 WRN    
    ## 3 TP53   
    ## 4 MGA    
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1     0.5
    ## 2     2     3     1     0.5
    ## 
    ## $fit$clones_to_expand$CRUK0001$`5`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PASK   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0002
    ## $fit$clones_to_expand$CRUK0002$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 RB1    
    ## 2 IKZF1  
    ## 3 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0002$`2`
    ## # A tbl_graph: 2 nodes and 1 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MET    
    ## 2 TERT   
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## $fit$clones_to_expand$CRUK0002$`5`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NF1    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0002$`6`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EP300  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0003
    ## $fit$clones_to_expand$CRUK0003$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PIK3CA 
    ## 2 EGFR   
    ## 3 CDKN2A 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0003$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CTNNB1 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0004
    ## $fit$clones_to_expand$CRUK0004$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 SMAD4  
    ## 2 NOTCH1 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0004$`2`
    ## # A tbl_graph: 2 nodes and 1 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 TP53   
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0005
    ## $fit$clones_to_expand$CRUK0005$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0005$`2`
    ## # A tbl_graph: 5 nodes and 2 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 BRAF   
    ## 2 TP53   
    ## 3 CMTR2  
    ## 4 PASK   
    ## 5 TERT   
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     5     1   0.333
    ## 2     2     5     2   0.667
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0006
    ## $fit$clones_to_expand$CRUK0006$`1`
    ## # A tbl_graph: 4 nodes and 2 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 PLXNB2 
    ## 3 KEAP1  
    ## 4 TERT   
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 2     1     4     2       1
    ## 
    ## $fit$clones_to_expand$CRUK0006$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MAP3K1 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0006$`7`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FANCC  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0007
    ## $fit$clones_to_expand$CRUK0007$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PIK3CA 
    ## 2 EGFR   
    ## 3 SGK223 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0008
    ## $fit$clones_to_expand$CRUK0008$`2`
    ## # A tbl_graph: 5 nodes and 0 edges
    ## #
    ## # A rooted forest with 5 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KEAP1  
    ## 2 STK11  
    ## 3 PRDM1  
    ## 4 U2AF1  
    ## 5 MYC    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0008$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 ARID2  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0009
    ## $fit$clones_to_expand$CRUK0009$`1`
    ## # A tbl_graph: 6 nodes and 2 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 6 x 1 (active)
    ##   cluster 
    ##   <chr>   
    ## 1 TP53    
    ## 2 BRAF    
    ## 3 ARHGAP35
    ## 4 KMT2C   
    ## 5 NFE2L2  
    ## 6 MET     
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1       1
    ## 2     1     5     3       1
    ## 
    ## $fit$clones_to_expand$CRUK0009$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TERT   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0010
    ## $fit$clones_to_expand$CRUK0010$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 SETD2  
    ## 2 EGFR   
    ## 3 TERT   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0011
    ## $fit$clones_to_expand$CRUK0011$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0011$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FLT4   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0012
    ## $fit$clones_to_expand$CRUK0012$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0013
    ## $fit$clones_to_expand$CRUK0013$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 STK11  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0013$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NOTCH1 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0013$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0013$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0014
    ## $fit$clones_to_expand$CRUK0014$`1`
    ## # A tbl_graph: 2 nodes and 2 edges
    ## #
    ## # A directed simple graph with 1 component
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 TP53   
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 2     2     1     2       1
    ## 
    ## $fit$clones_to_expand$CRUK0014$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 RNF43  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0015
    ## $fit$clones_to_expand$CRUK0015$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 BAP1   
    ## 2 EGFR   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0015$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0015$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 RB1    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0016
    ## $fit$clones_to_expand$CRUK0016$`1`
    ## # A tbl_graph: 6 nodes and 4 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 6 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 TP53   
    ## 3 FAT1   
    ## 4 SPEN   
    ## 5 CBLB   
    ## 6 TERT   
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 2     2     5     1       1
    ## 3     2     3     1       1
    ## # … with 1 more row
    ## 
    ## $fit$clones_to_expand$CRUK0016$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 ASXL1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0016$`6`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PTPRC  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0016$`10`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 DNM2   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0016$`16`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 LATS1  
    ## 2 ARID1B 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0017
    ## $fit$clones_to_expand$CRUK0017$`1`
    ## # A tbl_graph: 5 nodes and 3 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KEAP1  
    ## 2 MYC    
    ## 3 TP53   
    ## 4 ARID1B 
    ## 5 ARID2  
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     5     1     0.5
    ## 2     2     5     1     0.5
    ## 3     3     4     1     1  
    ## 
    ## $fit$clones_to_expand$CRUK0017$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0018
    ## $fit$clones_to_expand$CRUK0018$`1`
    ## # A tbl_graph: 4 nodes and 1 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 CMTR2  
    ## 3 MGA    
    ## 4 COL5A2 
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0019
    ## $fit$clones_to_expand$CRUK0019$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0020
    ## $fit$clones_to_expand$CRUK0020$`1`
    ## # A tbl_graph: 7 nodes and 6 edges
    ## #
    ## # A directed simple graph with 3 components
    ## #
    ## # Node Data: 7 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 ARID2  
    ## 2 KEAP1  
    ## 3 KRAS   
    ## 4 TP53   
    ## 5 MGA    
    ## 6 COL2A1 
    ## # … with 1 more row
    ## #
    ## # Edge Data: 6 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1    0.25
    ## 2     2     1     1    1   
    ## 3     2     3     1    0.25
    ## # … with 3 more rows
    ## 
    ## $fit$clones_to_expand$CRUK0020$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PIK3CA 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0020$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 BAP1   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0020$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NCOR1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0021
    ## $fit$clones_to_expand$CRUK0021$`1`
    ## # A tbl_graph: 4 nodes and 2 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 EGFR   
    ## 3 TP53   
    ## 4 CHEK2  
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1     0.5
    ## 2     2     3     1     0.5
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0022
    ## $fit$clones_to_expand$CRUK0022$`1`
    ## # A tbl_graph: 2 nodes and 1 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 TP53   
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## $fit$clones_to_expand$CRUK0022$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CIC    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0023
    ## $fit$clones_to_expand$CRUK0023$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 WRN    
    ## 2 KRAS   
    ## 3 CDKN2A 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0023$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0023$`4`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PTPRC  
    ## 2 KMT2D  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0024
    ## $fit$clones_to_expand$CRUK0024$`1`
    ## # A tbl_graph: 4 nodes and 2 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 STK11  
    ## 3 TP53   
    ## 4 POLE   
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1       1
    ## 2     2     1     1       1
    ## 
    ## $fit$clones_to_expand$CRUK0024$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 ATM    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0024$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NCOR1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0025
    ## $fit$clones_to_expand$CRUK0025$`1`
    ## # A tbl_graph: 3 nodes and 3 edges
    ## #
    ## # A directed simple graph with 1 component
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 TP53   
    ## 3 MGA    
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1       1
    ## 2     1     2     1       1
    ## 3     2     1     2       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0026
    ## $fit$clones_to_expand$CRUK0026$`1`
    ## # A tbl_graph: 4 nodes and 2 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster  
    ##   <chr>    
    ## 1 EGFR     
    ## 2 TP53     
    ## 3 RB1      
    ## 4 SERPINB13
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1       1
    ## 2     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0027
    ## $fit$clones_to_expand$CRUK0027$`1`
    ## # A tbl_graph: 2 nodes and 2 edges
    ## #
    ## # A directed simple graph with 1 component
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 TP53   
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 2     2     1     2       1
    ## 
    ## $fit$clones_to_expand$CRUK0027$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PLXNB2 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0028
    ## $fit$clones_to_expand$CRUK0028$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 APC    
    ## 2 EGFR   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0029
    ## $fit$clones_to_expand$CRUK0029$`1`
    ## # A tbl_graph: 4 nodes and 1 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 NRAS   
    ## 3 MGA    
    ## 4 CCND1  
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0030
    ## $fit$clones_to_expand$CRUK0030$`1`
    ## # A tbl_graph: 6 nodes and 3 edges
    ## #
    ## # A directed simple graph with 4 components
    ## #
    ## # Node Data: 6 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 TP53   
    ## 3 TSC2   
    ## 4 U2AF1  
    ## 5 FBXW7  
    ## 6 NF1    
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 2     2     1     2       1
    ## 3     2     6     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0031
    ## $fit$clones_to_expand$CRUK0031$`1`
    ## # A tbl_graph: 4 nodes and 0 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KEAP1  
    ## 2 CDKN2A 
    ## 3 PRF1   
    ## 4 FGFR1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0031$`6`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NF1    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0032
    ## $fit$clones_to_expand$CRUK0032$`1`
    ## # A tbl_graph: 4 nodes and 0 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 ATM    
    ## 2 RAD21  
    ## 3 U2AF1  
    ## 4 RNF43  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0032$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CCND1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0032$`6`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 ARID1B 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0033
    ## $fit$clones_to_expand$CRUK0033$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KEAP1  
    ## 2 CTNNB1 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0034
    ## $fit$clones_to_expand$CRUK0034$`1`
    ## # A tbl_graph: 3 nodes and 1 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 ATM    
    ## 3 PLXNB2 
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1       1
    ## 
    ## $fit$clones_to_expand$CRUK0034$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MGA    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0035
    ## $fit$clones_to_expand$CRUK0035$`1`
    ## # A tbl_graph: 2 nodes and 1 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 FAS    
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## $fit$clones_to_expand$CRUK0035$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FLT4   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0036
    ## $fit$clones_to_expand$CRUK0036$`1`
    ## # A tbl_graph: 5 nodes and 4 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster 
    ##   <chr>   
    ## 1 ARHGAP35
    ## 2 KEAP1   
    ## 3 PIK3CA  
    ## 4 TERT    
    ## 5 KRAS    
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1     0.5
    ## 2     2     5     1     0.5
    ## 3     3     4     1     0.5
    ## # … with 1 more row
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0037
    ## $fit$clones_to_expand$CRUK0037$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NCOA6  
    ## 2 CREBBP 
    ## 3 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0038
    ## $fit$clones_to_expand$CRUK0038$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0038$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KMT2D  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0039
    ## $fit$clones_to_expand$CRUK0039$`1`
    ## # A tbl_graph: 4 nodes and 0 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 CMTR2  
    ## 3 NF1    
    ## 4 PHOX2B 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0040
    ## $fit$clones_to_expand$CRUK0040$`1`
    ## # A tbl_graph: 4 nodes and 1 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 NCOR1  
    ## 3 RAD21  
    ## 4 GATA3  
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0041
    ## $fit$clones_to_expand$CRUK0041$`1`
    ## # A tbl_graph: 3 nodes and 1 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 BRAF   
    ## 2 TERT   
    ## 3 EGFR   
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0042
    ## $fit$clones_to_expand$CRUK0042$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0043
    ## $fit$clones_to_expand$CRUK0043$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MET    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0044
    ## $fit$clones_to_expand$CRUK0044$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0045
    ## $fit$clones_to_expand$CRUK0045$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 BAP1   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0046
    ## $fit$clones_to_expand$CRUK0046$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KEAP1  
    ## 2 APC    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0047
    ## $fit$clones_to_expand$CRUK0047$`1`
    ## # A tbl_graph: 4 nodes and 2 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MYC    
    ## 2 STK11  
    ## 3 APC    
    ## 4 KRAS   
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1     0.5
    ## 2     2     4     1     0.5
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0048
    ## $fit$clones_to_expand$CRUK0048$`1`
    ## # A tbl_graph: 7 nodes and 3 edges
    ## #
    ## # A directed acyclic simple graph with 5 components
    ## #
    ## # Node Data: 7 x 1 (active)
    ##   cluster 
    ##   <chr>   
    ## 1 EGFR    
    ## 2 TP53    
    ## 3 APC     
    ## 4 PRDM1   
    ## 5 ARHGAP35
    ## 6 BRAF    
    ## # … with 1 more row
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     5     1     0.5
    ## 2     1     2     1     1  
    ## 3     2     5     1     0.5
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0049
    ## $fit$clones_to_expand$CRUK0049$`1`
    ## # A tbl_graph: 5 nodes and 4 edges
    ## #
    ## # A directed simple graph with 2 components
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 KRAS   
    ## 3 TP53   
    ## 4 RB1    
    ## 5 COL2A1 
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1     1  
    ## 2     1     3     1     0.5
    ## 3     2     3     1     0.5
    ## # … with 1 more row
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0050
    ## $fit$clones_to_expand$CRUK0050$`1`
    ## # A tbl_graph: 3 nodes and 2 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MYC    
    ## 2 STK11  
    ## 3 KRAS   
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1     0.5
    ## 2     2     3     1     0.5
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0051
    ## $fit$clones_to_expand$CRUK0051$`1`
    ## # A tbl_graph: 4 nodes and 3 edges
    ## #
    ## # A directed simple graph with 2 components
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 KRAS   
    ## 3 TP53   
    ## 4 FBXW7  
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1     0.5
    ## 2     2     3     1     0.5
    ## 3     3     2     2     1  
    ## 
    ## $fit$clones_to_expand$CRUK0051$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EP300  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0052
    ## $fit$clones_to_expand$CRUK0052$`1`
    ## # A tbl_graph: 8 nodes and 8 edges
    ## #
    ## # A directed simple graph with 3 components
    ## #
    ## # Node Data: 8 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KEAP1  
    ## 2 KRAS   
    ## 3 MGA    
    ## 4 TP53   
    ## 5 KMT2D  
    ## 6 NOTCH2 
    ## # … with 2 more rows
    ## #
    ## # Edge Data: 8 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1   0.333
    ## 2     1     7     1   0.333
    ## 3     2     5     2   1    
    ## # … with 5 more rows
    ## 
    ## $fit$clones_to_expand$CRUK0052$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 UBR5   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0054
    ## $fit$clones_to_expand$CRUK0054$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0055
    ## $fit$clones_to_expand$CRUK0055$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FANCM  
    ## 2 UBR5   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0055$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FAT1   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0056
    ## $fit$clones_to_expand$CRUK0056$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 RASA1  
    ## 2 CREBBP 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0056$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0057
    ## $fit$clones_to_expand$CRUK0057$`1`
    ## # A tbl_graph: 5 nodes and 2 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TERT   
    ## 2 KRAS   
    ## 3 SMARCA4
    ## 4 TSC2   
    ## 5 DNM2   
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     5     1       1
    ## 2     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0058
    ## $fit$clones_to_expand$CRUK0058$`1`
    ## # A tbl_graph: 2 nodes and 1 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 TP53   
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0059
    ## $fit$clones_to_expand$CRUK0059$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0060
    ## $fit$clones_to_expand$CRUK0060$`1`
    ## # A tbl_graph: 11 nodes and 3 edges
    ## #
    ## # A rooted forest with 8 trees
    ## #
    ## # Node Data: 11 x 1 (active)
    ##   cluster  
    ##   <chr>    
    ## 1 NCOA6    
    ## 2 NF1      
    ## 3 SERPINB13
    ## 4 ARID2    
    ## 5 COL5A2   
    ## 6 FANCM    
    ## # … with 5 more rows
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     5     1     0.5
    ## 2     2     6     1     1  
    ## 3     3     5     1     0.5
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0061
    ## $fit$clones_to_expand$CRUK0061$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 STK11  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0062
    ## $fit$clones_to_expand$CRUK0062$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FAS    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0062$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PLXNB2 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0062$`4`
    ## # A tbl_graph: 4 nodes and 0 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 PIK3CA 
    ## 3 SOX2   
    ## 4 CCND1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0062$`16`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 UBR5   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0063
    ## $fit$clones_to_expand$CRUK0063$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NF1    
    ## 2 CYLD   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0063$`2`
    ## # A tbl_graph: 7 nodes and 4 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 7 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 PIK3CA 
    ## 3 SOX2   
    ## 4 TP53   
    ## 5 FBXW7  
    ## 6 TERT   
    ## # … with 1 more row
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1    1   
    ## 2     2     6     1    0.25
    ## 3     3     6     1    0.25
    ## # … with 1 more row
    ## 
    ## $fit$clones_to_expand$CRUK0063$`6`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FANCM  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0063$`10`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EP300  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0064
    ## $fit$clones_to_expand$CRUK0064$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0064$`2`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MLH1   
    ## 2 FAT1   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0065
    ## $fit$clones_to_expand$CRUK0065$`1`
    ## # A tbl_graph: 4 nodes and 3 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PIK3CA 
    ## 2 SOX2   
    ## 3 TP53   
    ## 4 NFE2L2 
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     2   0.286
    ## 2     2     4     2   0.286
    ## 3     3     4     3   0.429
    ## 
    ## $fit$clones_to_expand$CRUK0065$`2`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MLH1   
    ## 2 PTPRC  
    ## 3 UBR5   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0065$`6`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NOTCH1 
    ## 2 NCOA6  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0066
    ## $fit$clones_to_expand$CRUK0066$`1`
    ## # A tbl_graph: 7 nodes and 5 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 7 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 TP53   
    ## 3 WRN    
    ## 4 NOTCH1 
    ## 5 PDGFRA 
    ## 6 TERT   
    ## # … with 1 more row
    ## #
    ## # Edge Data: 5 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1     0.5
    ## 2     2     7     1     1  
    ## 3     2     4     2     1  
    ## # … with 2 more rows
    ## 
    ## $fit$clones_to_expand$CRUK0066$`9`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 COL5A2 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0067
    ## $fit$clones_to_expand$CRUK0067$`1`
    ## # A tbl_graph: 5 nodes and 4 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 PIK3CA 
    ## 3 SOX2   
    ## 4 TP53   
    ## 5 NOTCH1 
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1    1   
    ## 2     2     5     1    0.25
    ## 3     3     5     1    0.25
    ## # … with 1 more row
    ## 
    ## $fit$clones_to_expand$CRUK0067$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NFE2L2 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0068
    ## $fit$clones_to_expand$CRUK0068$`1`
    ## # A tbl_graph: 5 nodes and 0 edges
    ## #
    ## # A rooted forest with 5 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 PTEN   
    ## 3 KMT2D  
    ## 4 PIK3CA 
    ## 5 SOX2   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0068$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 MGA    
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0068$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 SETD2  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0068$`9`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TERT   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0069
    ## $fit$clones_to_expand$CRUK0069$`1`
    ## # A tbl_graph: 4 nodes and 1 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 FAT1   
    ## 3 PDGFRA 
    ## 4 FGFR1  
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## $fit$clones_to_expand$CRUK0069$`13`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0070
    ## $fit$clones_to_expand$CRUK0070$`1`
    ## # A tbl_graph: 4 nodes and 3 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 SOX2   
    ## 2 TP53   
    ## 3 DNM2   
    ## 4 COL5A2 
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1   0.333
    ## 2     2     4     2   0.667
    ## 3     2     3     1   1    
    ## 
    ## $fit$clones_to_expand$CRUK0070$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CBLB   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0070$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NFE2L2 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0071
    ## $fit$clones_to_expand$CRUK0071$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CMTR2  
    ## 2 PIK3CA 
    ## 3 SOX2   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0071$`4`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 UBR5   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0072
    ## $fit$clones_to_expand$CRUK0072$`1`
    ## # A tbl_graph: 6 nodes and 4 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 6 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 PIK3CA 
    ## 3 SOX2   
    ## 4 TP53   
    ## 5 NFE2L2 
    ## 6 MYC    
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1   1    
    ## 2     2     5     2   0.286
    ## 3     3     5     2   0.286
    ## # … with 1 more row
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0073
    ## $fit$clones_to_expand$CRUK0073$`1`
    ## # A tbl_graph: 8 nodes and 4 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 8 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 FAT1   
    ## 3 FGFR1  
    ## 4 DICER1 
    ## 5 NFE2L2 
    ## 6 KMT2D  
    ## # … with 2 more rows
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     6     1   1    
    ## 2     1     5     1   0.333
    ## 3     2     5     1   0.333
    ## # … with 1 more row
    ## 
    ## $fit$clones_to_expand$CRUK0073$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PLXNB2 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0074
    ## $fit$clones_to_expand$CRUK0074$`1`
    ## # A tbl_graph: 5 nodes and 3 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PIK3CA 
    ## 2 SOX2   
    ## 3 TP53   
    ## 4 NFE2L2 
    ## 5 CCND1  
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     2   0.286
    ## 2     2     4     2   0.286
    ## 3     3     4     3   0.429
    ## 
    ## $fit$clones_to_expand$CRUK0074$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 UBR5   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0075
    ## $fit$clones_to_expand$CRUK0075$`1`
    ## # A tbl_graph: 7 nodes and 4 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 7 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PIK3CA 
    ## 2 RASA1  
    ## 3 TP53   
    ## 4 NOTCH1 
    ## 5 FAT1   
    ## 6 MGA    
    ## # … with 1 more row
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1   0.333
    ## 2     2     3     1   1    
    ## 3     3     5     1   1    
    ## # … with 1 more row
    ## 
    ## $fit$clones_to_expand$CRUK0075$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NFE2L2 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0076
    ## $fit$clones_to_expand$CRUK0076$`1`
    ## # A tbl_graph: 6 nodes and 1 edges
    ## #
    ## # A rooted forest with 5 trees
    ## #
    ## # Node Data: 6 x 1 (active)
    ##   cluster  
    ##   <chr>    
    ## 1 TP53     
    ## 2 SERPINB13
    ## 3 ARID1B   
    ## 4 PIK3CA   
    ## 5 SOX2     
    ## 6 FGFR1    
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1       1
    ## 
    ## $fit$clones_to_expand$CRUK0076$`2`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 NCOR1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0076$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 COL5A2 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0077
    ## $fit$clones_to_expand$CRUK0077$`1`
    ## # A tbl_graph: 3 nodes and 1 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 LATS1  
    ## 3 KEAP1  
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0078
    ## $fit$clones_to_expand$CRUK0078$`1`
    ## # A tbl_graph: 5 nodes and 1 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FGFR1  
    ## 2 PLXNB2 
    ## 3 PTEN   
    ## 4 PIK3CA 
    ## 5 SOX2   
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0079
    ## $fit$clones_to_expand$CRUK0079$`1`
    ## # A tbl_graph: 6 nodes and 1 edges
    ## #
    ## # A rooted forest with 5 trees
    ## #
    ## # Node Data: 6 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 FAT1   
    ## 3 POLE   
    ## 4 PIK3CA 
    ## 5 SOX2   
    ## 6 FGFR1  
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0080
    ## $fit$clones_to_expand$CRUK0080$`1`
    ## # A tbl_graph: 4 nodes and 1 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 EGFR   
    ## 2 TP53   
    ## 3 WT1    
    ## 4 CCND1  
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## $fit$clones_to_expand$CRUK0080$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 IKZF1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0081
    ## $fit$clones_to_expand$CRUK0081$`1`
    ## # A tbl_graph: 5 nodes and 4 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 TP53   
    ## 3 NOTCH1 
    ## 4 FAT1   
    ## 5 FANCC  
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 2     2     5     1       1
    ## 3     2     4     1       1
    ## # … with 1 more row
    ## 
    ## $fit$clones_to_expand$CRUK0081$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CYLD   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0082
    ## $fit$clones_to_expand$CRUK0082$`1`
    ## # A tbl_graph: 8 nodes and 4 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 8 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 FGFR1  
    ## 2 PIK3CA 
    ## 3 SOX2   
    ## 4 TP53   
    ## 5 WT1    
    ## 6 PTEN   
    ## # … with 2 more rows
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     7     1     0.2
    ## 2     2     7     1     0.2
    ## 3     3     7     1     0.2
    ## # … with 1 more row
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0083
    ## $fit$clones_to_expand$CRUK0083$`1`
    ## # A tbl_graph: 7 nodes and 1 edges
    ## #
    ## # A rooted forest with 6 trees
    ## #
    ## # Node Data: 7 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 RASA1  
    ## 2 TP53   
    ## 3 FBXW7  
    ## 4 PIK3CA 
    ## 5 SOX2   
    ## 6 FGFR1  
    ## # … with 1 more row
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0084
    ## $fit$clones_to_expand$CRUK0084$`1`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CREBBP 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0085
    ## $fit$clones_to_expand$CRUK0085$`1`
    ## # A tbl_graph: 4 nodes and 0 edges
    ## #
    ## # A rooted forest with 4 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CHEK2  
    ## 2 CREBBP 
    ## 3 LATS1  
    ## 4 FANCM  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0086
    ## $fit$clones_to_expand$CRUK0086$`1`
    ## # A tbl_graph: 3 nodes and 1 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 ARID2  
    ## 3 FAT1   
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0087
    ## $fit$clones_to_expand$CRUK0087$`1`
    ## # A tbl_graph: 4 nodes and 2 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 4 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PIK3CA 
    ## 2 TP53   
    ## 3 NFE2L2 
    ## 4 ASXL1  
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     3     2     0.4
    ## 2     2     3     3     0.6
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0088
    ## $fit$clones_to_expand$CRUK0088$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CUX1   
    ## 2 TP53   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0089
    ## $fit$clones_to_expand$CRUK0089$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 PIK3CA 
    ## 2 SMAD4  
    ## 3 KEAP1  
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0090
    ## $fit$clones_to_expand$CRUK0090$`1`
    ## # A tbl_graph: 5 nodes and 0 edges
    ## #
    ## # A rooted forest with 5 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 NCOA6  
    ## 3 CUX1   
    ## 4 COL2A1 
    ## 5 NRAS   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0091
    ## $fit$clones_to_expand$CRUK0091$`1`
    ## # A tbl_graph: 3 nodes and 1 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 TP53   
    ## 3 SMARCA4
    ## #
    ## # Edge Data: 1 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0092
    ## $fit$clones_to_expand$CRUK0092$`1`
    ## # A tbl_graph: 5 nodes and 3 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 5 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 RASA1  
    ## 2 TP53   
    ## 3 SMAD4  
    ## 4 CBLB   
    ## 5 PIK3CA 
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 2     2     4     1       1
    ## 3     2     3     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0093
    ## $fit$clones_to_expand$CRUK0093$`1`
    ## # A tbl_graph: 7 nodes and 4 edges
    ## #
    ## # A directed acyclic simple graph with 4 components
    ## #
    ## # Node Data: 7 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 TP53   
    ## 3 DICER1 
    ## 4 COL2A1 
    ## 5 GATA3  
    ## 6 CIC    
    ## # … with 1 more row
    ## #
    ## # Edge Data: 4 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     7     1   0.333
    ## 2     1     2     1   1    
    ## 3     2     6     1   1    
    ## # … with 1 more row
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0094
    ## $fit$clones_to_expand$CRUK0094$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 SMARCA4
    ## 2 TERT   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0095
    ## $fit$clones_to_expand$CRUK0095$`1`
    ## # A tbl_graph: 3 nodes and 2 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 RASA1  
    ## 2 TP53   
    ## 3 NF1    
    ## #
    ## # Edge Data: 2 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     2     1       1
    ## 2     2     3     1       1
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0096
    ## $fit$clones_to_expand$CRUK0096$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 KRAS   
    ## 2 SGK223 
    ## 3 MAP3K1 
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0097
    ## $fit$clones_to_expand$CRUK0097$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 PTEN   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0098
    ## $fit$clones_to_expand$CRUK0098$`1`
    ## # A tbl_graph: 2 nodes and 0 edges
    ## #
    ## # A rooted forest with 2 trees
    ## #
    ## # Node Data: 2 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 TP53   
    ## 2 PTEN   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## $fit$clones_to_expand$CRUK0098$`3`
    ## # A tbl_graph: 1 nodes and 0 edges
    ## #
    ## # A rooted tree
    ## #
    ## # Node Data: 1 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 UBR5   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0099
    ## $fit$clones_to_expand$CRUK0099$`1`
    ## # A tbl_graph: 3 nodes and 0 edges
    ## #
    ## # A rooted forest with 3 trees
    ## #
    ## # Node Data: 3 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 STK11  
    ## 2 KEAP1  
    ## 3 TP53   
    ## #
    ## # Edge Data: 0 x 4
    ## # … with 4 variables: from <int>, to <int>, count <int>, penalty <dbl>
    ## 
    ## 
    ## $fit$clones_to_expand$CRUK0100
    ## $fit$clones_to_expand$CRUK0100$`1`
    ## # A tbl_graph: 6 nodes and 3 edges
    ## #
    ## # A directed acyclic simple graph with 4 components
    ## #
    ## # Node Data: 6 x 1 (active)
    ##   cluster
    ##   <chr>  
    ## 1 CDKN2A 
    ## 2 TP53   
    ## 3 PHOX2B 
    ## 4 COL5A2 
    ## 5 STK11  
    ## 6 SPEN   
    ## #
    ## # Edge Data: 3 x 4
    ##    from    to count penalty
    ##   <int> <int> <int>   <dbl>
    ## 1     1     4     1   0.333
    ## 2     1     2     1   1    
    ## 3     2     4     2   0.667
    ## 
    ## 
    ## 
    ## $fit$clones_expansions
    ## $fit$clones_expansions$CRUK0001
    ## # A tibble: 10 x 2
    ##    from  to      
    ##    <chr> <chr>   
    ##  1 GL    EGFR    
    ##  2 GL    WRN     
    ##  3 GL    MGA     
    ##  4 EGFR  TP53    
    ##  5 WRN   TP53    
    ##  6 TP53  NF1     
    ##  7 MGA   NF1     
    ##  8 TP53  ARHGAP35
    ##  9 MGA   ARHGAP35
    ## 10 NF1   PASK    
    ## 
    ## $fit$clones_expansions$CRUK0002
    ## # A tibble: 7 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    MET  
    ## 2 MET   TERT 
    ## 3 TERT  EP300
    ## 4 TERT  RB1  
    ## 5 TERT  IKZF1
    ## 6 TERT  KRAS 
    ## 7 EP300 NF1  
    ## 
    ## $fit$clones_expansions$CRUK0003
    ## # A tibble: 6 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     PIK3CA
    ## 2 GL     EGFR  
    ## 3 GL     CDKN2A
    ## 4 PIK3CA CTNNB1
    ## 5 EGFR   CTNNB1
    ## 6 CDKN2A CTNNB1
    ## 
    ## $fit$clones_expansions$CRUK0004
    ## # A tibble: 4 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    EGFR  
    ## 2 EGFR  TP53  
    ## 3 TP53  SMAD4 
    ## 4 TP53  NOTCH1
    ## 
    ## $fit$clones_expansions$CRUK0005
    ## # A tibble: 9 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    BRAF 
    ## 2 GL    TP53 
    ## 3 GL    CMTR2
    ## 4 GL    PASK 
    ## 5 BRAF  TERT 
    ## 6 TP53  TERT 
    ## 7 CMTR2 NRAS 
    ## 8 PASK  NRAS 
    ## 9 TERT  NRAS 
    ## 
    ## $fit$clones_expansions$CRUK0006
    ## # A tibble: 10 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     TP53  
    ##  2 GL     KEAP1 
    ##  3 TP53   PLXNB2
    ##  4 TP53   TERT  
    ##  5 PLXNB2 MAP3K1
    ##  6 KEAP1  MAP3K1
    ##  7 TERT   MAP3K1
    ##  8 PLXNB2 FANCC 
    ##  9 KEAP1  FANCC 
    ## 10 TERT   FANCC 
    ## 
    ## $fit$clones_expansions$CRUK0007
    ## # A tibble: 3 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    PIK3CA
    ## 2 GL    EGFR  
    ## 3 GL    SGK223
    ## 
    ## $fit$clones_expansions$CRUK0008
    ## # A tibble: 10 x 2
    ##    from  to   
    ##    <chr> <chr>
    ##  1 GL    KEAP1
    ##  2 GL    STK11
    ##  3 GL    PRDM1
    ##  4 GL    U2AF1
    ##  5 GL    MYC  
    ##  6 KEAP1 ARID2
    ##  7 STK11 ARID2
    ##  8 PRDM1 ARID2
    ##  9 U2AF1 ARID2
    ## 10 MYC   ARID2
    ## 
    ## $fit$clones_expansions$CRUK0009
    ## # A tibble: 11 x 2
    ##    from     to      
    ##    <chr>    <chr>   
    ##  1 GL       TP53    
    ##  2 GL       BRAF    
    ##  3 GL       KMT2C   
    ##  4 GL       MET     
    ##  5 TP53     ARHGAP35
    ##  6 TP53     NFE2L2  
    ##  7 BRAF     TERT    
    ##  8 ARHGAP35 TERT    
    ##  9 KMT2C    TERT    
    ## 10 NFE2L2   TERT    
    ## 11 MET      TERT    
    ## 
    ## $fit$clones_expansions$CRUK0010
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    SETD2
    ## 2 GL    EGFR 
    ## 3 GL    TERT 
    ## 
    ## $fit$clones_expansions$CRUK0011
    ## # A tibble: 2 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KRAS 
    ## 2 KRAS  FLT4 
    ## 
    ## $fit$clones_expansions$CRUK0012
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    EGFR 
    ## 
    ## $fit$clones_expansions$CRUK0013
    ## # A tibble: 4 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    STK11 
    ## 2 STK11 NOTCH1
    ## 3 STK11 KRAS  
    ## 4 STK11 EGFR  
    ## 
    ## $fit$clones_expansions$CRUK0014
    ## # A tibble: 6 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KRAS 
    ## 2 GL    TP53 
    ## 3 KRAS  TP53 
    ## 4 TP53  KRAS 
    ## 5 KRAS  RNF43
    ## 6 TP53  RNF43
    ## 
    ## $fit$clones_expansions$CRUK0015
    ## # A tibble: 6 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    BAP1 
    ## 2 GL    EGFR 
    ## 3 BAP1  TP53 
    ## 4 EGFR  TP53 
    ## 5 BAP1  RB1  
    ## 6 EGFR  RB1  
    ## 
    ## $fit$clones_expansions$CRUK0016
    ## # A tibble: 24 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     CDKN2A
    ##  2 GL     SPEN  
    ##  3 CDKN2A TP53  
    ##  4 TP53   FAT1  
    ##  5 TP53   CBLB  
    ##  6 TP53   TERT  
    ##  7 FAT1   LATS1 
    ##  8 SPEN   LATS1 
    ##  9 CBLB   LATS1 
    ## 10 TERT   LATS1 
    ## # … with 14 more rows
    ## 
    ## $fit$clones_expansions$CRUK0017
    ## # A tibble: 8 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     KEAP1 
    ## 2 GL     MYC   
    ## 3 GL     TP53  
    ## 4 KEAP1  ARID2 
    ## 5 MYC    ARID2 
    ## 6 TP53   ARID1B
    ## 7 ARID1B KRAS  
    ## 8 ARID2  KRAS  
    ## 
    ## $fit$clones_expansions$CRUK0018
    ## # A tibble: 4 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    KRAS  
    ## 2 GL    CMTR2 
    ## 3 GL    COL5A2
    ## 4 KRAS  MGA   
    ## 
    ## $fit$clones_expansions$CRUK0019
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    EGFR 
    ## 
    ## $fit$clones_expansions$CRUK0020
    ## # A tibble: 22 x 2
    ##    from  to    
    ##    <chr> <chr> 
    ##  1 GL    KEAP1 
    ##  2 GL    COL2A1
    ##  3 GL    PRF1  
    ##  4 GL    KRAS  
    ##  5 GL    TP53  
    ##  6 ARID2 KRAS  
    ##  7 KEAP1 ARID2 
    ##  8 KEAP1 KRAS  
    ##  9 KRAS  TP53  
    ## 10 KRAS  MGA   
    ## # … with 12 more rows
    ## 
    ## $fit$clones_expansions$CRUK0021
    ## # A tibble: 5 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     CDKN2A
    ## 2 GL     EGFR  
    ## 3 GL     CHEK2 
    ## 4 CDKN2A TP53  
    ## 5 EGFR   TP53  
    ## 
    ## $fit$clones_expansions$CRUK0022
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    EGFR 
    ## 2 EGFR  TP53 
    ## 3 TP53  CIC  
    ## 
    ## $fit$clones_expansions$CRUK0023
    ## # A tibble: 12 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     WRN   
    ##  2 GL     KRAS  
    ##  3 GL     CDKN2A
    ##  4 WRN    PTPRC 
    ##  5 KRAS   PTPRC 
    ##  6 CDKN2A PTPRC 
    ##  7 WRN    KMT2D 
    ##  8 KRAS   KMT2D 
    ##  9 CDKN2A KMT2D 
    ## 10 WRN    TP53  
    ## 11 KRAS   TP53  
    ## 12 CDKN2A TP53  
    ## 
    ## $fit$clones_expansions$CRUK0024
    ## # A tibble: 7 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    STK11
    ## 2 GL    POLE 
    ## 3 EGFR  TP53 
    ## 4 STK11 EGFR 
    ## 5 TP53  ATM  
    ## 6 POLE  ATM  
    ## 7 ATM   NCOR1
    ## 
    ## $fit$clones_expansions$CRUK0025
    ## # A tibble: 5 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KRAS 
    ## 2 GL    TP53 
    ## 3 KRAS  TP53 
    ## 4 KRAS  MGA  
    ## 5 TP53  KRAS 
    ## 
    ## $fit$clones_expansions$CRUK0026
    ## # A tibble: 4 x 2
    ##   from  to       
    ##   <chr> <chr>    
    ## 1 GL    EGFR     
    ## 2 GL    SERPINB13
    ## 3 EGFR  TP53     
    ## 4 EGFR  RB1      
    ## 
    ## $fit$clones_expansions$CRUK0027
    ## # A tibble: 6 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    KRAS  
    ## 2 GL    TP53  
    ## 3 KRAS  TP53  
    ## 4 TP53  KRAS  
    ## 5 KRAS  PLXNB2
    ## 6 TP53  PLXNB2
    ## 
    ## $fit$clones_expansions$CRUK0028
    ## # A tibble: 2 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    APC  
    ## 2 GL    EGFR 
    ## 
    ## $fit$clones_expansions$CRUK0029
    ## # A tibble: 4 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    TP53 
    ## 2 GL    MGA  
    ## 3 GL    CCND1
    ## 4 TP53  NRAS 
    ## 
    ## $fit$clones_expansions$CRUK0030
    ## # A tibble: 8 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    TSC2 
    ## 2 GL    U2AF1
    ## 3 GL    FBXW7
    ## 4 GL    KRAS 
    ## 5 GL    TP53 
    ## 6 KRAS  TP53 
    ## 7 TP53  KRAS 
    ## 8 TP53  NF1  
    ## 
    ## $fit$clones_expansions$CRUK0031
    ## # A tibble: 8 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     KEAP1 
    ## 2 GL     CDKN2A
    ## 3 GL     PRF1  
    ## 4 GL     FGFR1 
    ## 5 KEAP1  NF1   
    ## 6 CDKN2A NF1   
    ## 7 PRF1   NF1   
    ## 8 FGFR1  NF1   
    ## 
    ## $fit$clones_expansions$CRUK0032
    ## # A tibble: 9 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    ATM   
    ## 2 GL    RAD21 
    ## 3 GL    U2AF1 
    ## 4 GL    RNF43 
    ## 5 ATM   CCND1 
    ## 6 RAD21 CCND1 
    ## 7 U2AF1 CCND1 
    ## 8 RNF43 CCND1 
    ## 9 CCND1 ARID1B
    ## 
    ## $fit$clones_expansions$CRUK0033
    ## # A tibble: 2 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    KEAP1 
    ## 2 GL    CTNNB1
    ## 
    ## $fit$clones_expansions$CRUK0034
    ## # A tibble: 5 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     KRAS  
    ## 2 GL     ATM   
    ## 3 KRAS   PLXNB2
    ## 4 ATM    MGA   
    ## 5 PLXNB2 MGA   
    ## 
    ## $fit$clones_expansions$CRUK0035
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    TP53 
    ## 2 TP53  FAS  
    ## 3 FAS   FLT4 
    ## 
    ## $fit$clones_expansions$CRUK0036
    ## # A tibble: 7 x 2
    ##   from     to      
    ##   <chr>    <chr>   
    ## 1 GL       ARHGAP35
    ## 2 GL       KEAP1   
    ## 3 GL       PIK3CA  
    ## 4 ARHGAP35 TERT    
    ## 5 KEAP1    KRAS    
    ## 6 PIK3CA   TERT    
    ## 7 TERT     KRAS    
    ## 
    ## $fit$clones_expansions$CRUK0037
    ## # A tibble: 3 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    NCOA6 
    ## 2 GL    CREBBP
    ## 3 GL    KRAS  
    ## 
    ## $fit$clones_expansions$CRUK0038
    ## # A tibble: 2 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KRAS 
    ## 2 KRAS  KMT2D
    ## 
    ## $fit$clones_expansions$CRUK0039
    ## # A tibble: 4 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    KRAS  
    ## 2 GL    CMTR2 
    ## 3 GL    NF1   
    ## 4 GL    PHOX2B
    ## 
    ## $fit$clones_expansions$CRUK0040
    ## # A tibble: 4 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KRAS 
    ## 2 GL    RAD21
    ## 3 GL    GATA3
    ## 4 KRAS  NCOR1
    ## 
    ## $fit$clones_expansions$CRUK0041
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    BRAF 
    ## 2 GL    EGFR 
    ## 3 BRAF  TERT 
    ## 
    ## $fit$clones_expansions$CRUK0042
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KRAS 
    ## 
    ## $fit$clones_expansions$CRUK0043
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    MET  
    ## 
    ## $fit$clones_expansions$CRUK0044
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KRAS 
    ## 
    ## $fit$clones_expansions$CRUK0045
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    BAP1 
    ## 
    ## $fit$clones_expansions$CRUK0046
    ## # A tibble: 2 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KEAP1
    ## 2 GL    APC  
    ## 
    ## $fit$clones_expansions$CRUK0047
    ## # A tibble: 5 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    MYC  
    ## 2 GL    STK11
    ## 3 GL    APC  
    ## 4 MYC   KRAS 
    ## 5 STK11 KRAS 
    ## 
    ## $fit$clones_expansions$CRUK0048
    ## # A tibble: 8 x 2
    ##   from  to      
    ##   <chr> <chr>   
    ## 1 GL    EGFR    
    ## 2 GL    APC     
    ## 3 GL    PRDM1   
    ## 4 GL    BRAF    
    ## 5 GL    MYC     
    ## 6 EGFR  TP53    
    ## 7 EGFR  ARHGAP35
    ## 8 TP53  ARHGAP35
    ## 
    ## $fit$clones_expansions$CRUK0049
    ## # A tibble: 8 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    EGFR  
    ## 2 GL    COL2A1
    ## 3 GL    KRAS  
    ## 4 GL    TP53  
    ## 5 EGFR  TP53  
    ## 6 EGFR  RB1   
    ## 7 KRAS  TP53  
    ## 8 TP53  KRAS  
    ## 
    ## $fit$clones_expansions$CRUK0050
    ## # A tibble: 4 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    MYC  
    ## 2 GL    STK11
    ## 3 MYC   KRAS 
    ## 4 STK11 KRAS 
    ## 
    ## $fit$clones_expansions$CRUK0051
    ## # A tibble: 10 x 2
    ##    from  to   
    ##    <chr> <chr>
    ##  1 GL    EGFR 
    ##  2 GL    FBXW7
    ##  3 GL    KRAS 
    ##  4 GL    TP53 
    ##  5 EGFR  TP53 
    ##  6 KRAS  TP53 
    ##  7 TP53  KRAS 
    ##  8 FBXW7 EP300
    ##  9 KRAS  EP300
    ## 10 TP53  EP300
    ## 
    ## $fit$clones_expansions$CRUK0052
    ## # A tibble: 19 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     KEAP1 
    ##  2 GL     NOTCH2
    ##  3 GL     SGK223
    ##  4 GL     KRAS  
    ##  5 GL     TP53  
    ##  6 KEAP1  KRAS  
    ##  7 KEAP1  NF1   
    ##  8 KRAS   MGA   
    ##  9 KRAS   TP53  
    ## 10 KRAS   KMT2D 
    ## 11 MGA    NF1   
    ## 12 TP53   KRAS  
    ## 13 TP53   NF1   
    ## 14 KMT2D  UBR5  
    ## 15 NOTCH2 UBR5  
    ## 16 NF1    UBR5  
    ## 17 SGK223 UBR5  
    ## 18 KRAS   UBR5  
    ## 19 TP53   UBR5  
    ## 
    ## $fit$clones_expansions$CRUK0054
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    EGFR 
    ## 
    ## $fit$clones_expansions$CRUK0055
    ## # A tibble: 4 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    FANCM
    ## 2 GL    UBR5 
    ## 3 FANCM FAT1 
    ## 4 UBR5  FAT1 
    ## 
    ## $fit$clones_expansions$CRUK0056
    ## # A tibble: 4 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     RASA1 
    ## 2 GL     CREBBP
    ## 3 RASA1  TP53  
    ## 4 CREBBP TP53  
    ## 
    ## $fit$clones_expansions$CRUK0057
    ## # A tibble: 5 x 2
    ##   from  to     
    ##   <chr> <chr>  
    ## 1 GL    TERT   
    ## 2 GL    SMARCA4
    ## 3 GL    TSC2   
    ## 4 TERT  KRAS   
    ## 5 TERT  DNM2   
    ## 
    ## $fit$clones_expansions$CRUK0058
    ## # A tibble: 2 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    EGFR 
    ## 2 EGFR  TP53 
    ## 
    ## $fit$clones_expansions$CRUK0059
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    KRAS 
    ## 
    ## $fit$clones_expansions$CRUK0060
    ## # A tibble: 12 x 2
    ##    from      to       
    ##    <chr>     <chr>    
    ##  1 GL        NCOA6    
    ##  2 GL        NF1      
    ##  3 GL        SERPINB13
    ##  4 GL        ARID2    
    ##  5 GL        PHOX2B   
    ##  6 GL        COL2A1   
    ##  7 GL        RASA1    
    ##  8 GL        NOTCH2   
    ##  9 GL        KMT2C    
    ## 10 NCOA6     COL5A2   
    ## 11 NF1       FANCM    
    ## 12 SERPINB13 COL5A2   
    ## 
    ## $fit$clones_expansions$CRUK0061
    ## # A tibble: 1 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    STK11
    ## 
    ## $fit$clones_expansions$CRUK0062
    ## # A tibble: 13 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     TP53  
    ##  2 GL     PIK3CA
    ##  3 GL     SOX2  
    ##  4 GL     CCND1 
    ##  5 TP53   UBR5  
    ##  6 PIK3CA UBR5  
    ##  7 SOX2   UBR5  
    ##  8 CCND1  UBR5  
    ##  9 TP53   FAS   
    ## 10 PIK3CA FAS   
    ## 11 SOX2   FAS   
    ## 12 CCND1  FAS   
    ## 13 UBR5   PLXNB2
    ## 
    ## $fit$clones_expansions$CRUK0063
    ## # A tibble: 16 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     CDKN2A
    ##  2 GL     PIK3CA
    ##  3 GL     SOX2  
    ##  4 GL     FBXW7 
    ##  5 GL     PRF1  
    ##  6 CDKN2A TP53  
    ##  7 PIK3CA TERT  
    ##  8 SOX2   TERT  
    ##  9 TP53   TERT  
    ## 10 FBXW7  EP300 
    ## 11 TERT   EP300 
    ## 12 PRF1   EP300 
    ## 13 EP300  NF1   
    ## 14 EP300  CYLD  
    ## 15 NF1    FANCM 
    ## 16 CYLD   FANCM 
    ## 
    ## $fit$clones_expansions$CRUK0064
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    TP53 
    ## 2 TP53  MLH1 
    ## 3 TP53  FAT1 
    ## 
    ## $fit$clones_expansions$CRUK0065
    ## # A tibble: 11 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     PIK3CA
    ##  2 GL     SOX2  
    ##  3 GL     TP53  
    ##  4 PIK3CA NFE2L2
    ##  5 SOX2   NFE2L2
    ##  6 TP53   NFE2L2
    ##  7 NFE2L2 MLH1  
    ##  8 NFE2L2 PTPRC 
    ##  9 NFE2L2 UBR5  
    ## 10 NFE2L2 NOTCH1
    ## 11 NFE2L2 NCOA6 
    ## 
    ## $fit$clones_expansions$CRUK0066
    ## # A tibble: 12 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     CDKN2A
    ##  2 GL     WRN   
    ##  3 GL     PDGFRA
    ##  4 CDKN2A TP53  
    ##  5 TP53   NOTCH1
    ##  6 TP53   TERT  
    ##  7 TP53   NCOA6 
    ##  8 WRN    TP53  
    ##  9 NOTCH1 COL5A2
    ## 10 PDGFRA COL5A2
    ## 11 TERT   COL5A2
    ## 12 NCOA6  COL5A2
    ## 
    ## $fit$clones_expansions$CRUK0067
    ## # A tibble: 8 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     CDKN2A
    ## 2 GL     PIK3CA
    ## 3 GL     SOX2  
    ## 4 CDKN2A TP53  
    ## 5 PIK3CA NOTCH1
    ## 6 SOX2   NOTCH1
    ## 7 TP53   NOTCH1
    ## 8 NOTCH1 NFE2L2
    ## 
    ## $fit$clones_expansions$CRUK0068
    ## # A tibble: 16 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     TP53  
    ##  2 GL     PTEN  
    ##  3 GL     KMT2D 
    ##  4 GL     PIK3CA
    ##  5 GL     SOX2  
    ##  6 TP53   SETD2 
    ##  7 PTEN   SETD2 
    ##  8 KMT2D  SETD2 
    ##  9 PIK3CA SETD2 
    ## 10 SOX2   SETD2 
    ## 11 TP53   TERT  
    ## 12 PTEN   TERT  
    ## 13 KMT2D  TERT  
    ## 14 PIK3CA TERT  
    ## 15 SOX2   TERT  
    ## 16 SETD2  MGA   
    ## 
    ## $fit$clones_expansions$CRUK0069
    ## # A tibble: 7 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     TP53  
    ## 2 GL     PDGFRA
    ## 3 GL     FGFR1 
    ## 4 TP53   FAT1  
    ## 5 FAT1   KRAS  
    ## 6 PDGFRA KRAS  
    ## 7 FGFR1  KRAS  
    ## 
    ## $fit$clones_expansions$CRUK0070
    ## # A tibble: 9 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     SOX2  
    ## 2 GL     TP53  
    ## 3 SOX2   COL5A2
    ## 4 TP53   DNM2  
    ## 5 TP53   COL5A2
    ## 6 DNM2   CBLB  
    ## 7 COL5A2 CBLB  
    ## 8 DNM2   NFE2L2
    ## 9 COL5A2 NFE2L2
    ## 
    ## $fit$clones_expansions$CRUK0071
    ## # A tibble: 6 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     CMTR2 
    ## 2 GL     PIK3CA
    ## 3 GL     SOX2  
    ## 4 CMTR2  UBR5  
    ## 5 PIK3CA UBR5  
    ## 6 SOX2   UBR5  
    ## 
    ## $fit$clones_expansions$CRUK0072
    ## # A tibble: 8 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     EGFR  
    ## 2 GL     PIK3CA
    ## 3 GL     SOX2  
    ## 4 GL     MYC   
    ## 5 EGFR   TP53  
    ## 6 PIK3CA NFE2L2
    ## 7 SOX2   NFE2L2
    ## 8 TP53   NFE2L2
    ## 
    ## $fit$clones_expansions$CRUK0073
    ## # A tibble: 15 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     CDKN2A
    ##  2 GL     FAT1  
    ##  3 GL     FGFR1 
    ##  4 GL     DICER1
    ##  5 GL     NOTCH2
    ##  6 GL     MYC   
    ##  7 CDKN2A NFE2L2
    ##  8 CDKN2A KMT2D 
    ##  9 FAT1   NFE2L2
    ## 10 FGFR1  NFE2L2
    ## 11 DICER1 PLXNB2
    ## 12 NFE2L2 PLXNB2
    ## 13 KMT2D  PLXNB2
    ## 14 NOTCH2 PLXNB2
    ## 15 MYC    PLXNB2
    ## 
    ## $fit$clones_expansions$CRUK0074
    ## # A tibble: 9 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     PIK3CA
    ## 2 GL     SOX2  
    ## 3 GL     TP53  
    ## 4 GL     CCND1 
    ## 5 PIK3CA NFE2L2
    ## 6 SOX2   NFE2L2
    ## 7 TP53   NFE2L2
    ## 8 NFE2L2 UBR5  
    ## 9 CCND1  UBR5  
    ## 
    ## $fit$clones_expansions$CRUK0075
    ## # A tibble: 12 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     PIK3CA
    ##  2 GL     RASA1 
    ##  3 GL     MGA   
    ##  4 GL     FGFR1 
    ##  5 PIK3CA NOTCH1
    ##  6 RASA1  TP53  
    ##  7 TP53   NOTCH1
    ##  8 TP53   FAT1  
    ##  9 NOTCH1 NFE2L2
    ## 10 FAT1   NFE2L2
    ## 11 MGA    NFE2L2
    ## 12 FGFR1  NFE2L2
    ## 
    ## $fit$clones_expansions$CRUK0076
    ## # A tibble: 12 x 2
    ##    from      to       
    ##    <chr>     <chr>    
    ##  1 GL        TP53     
    ##  2 GL        SERPINB13
    ##  3 GL        PIK3CA   
    ##  4 GL        SOX2     
    ##  5 GL        FGFR1    
    ##  6 TP53      ARID1B   
    ##  7 SERPINB13 COL5A2   
    ##  8 ARID1B    COL5A2   
    ##  9 PIK3CA    COL5A2   
    ## 10 SOX2      COL5A2   
    ## 11 FGFR1     COL5A2   
    ## 12 COL5A2    NCOR1    
    ## 
    ## $fit$clones_expansions$CRUK0077
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    TP53 
    ## 2 GL    KEAP1
    ## 3 TP53  LATS1
    ## 
    ## $fit$clones_expansions$CRUK0078
    ## # A tibble: 5 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    FGFR1 
    ## 2 GL    PTEN  
    ## 3 GL    PIK3CA
    ## 4 GL    SOX2  
    ## 5 FGFR1 PLXNB2
    ## 
    ## $fit$clones_expansions$CRUK0079
    ## # A tibble: 6 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    TP53  
    ## 2 GL    POLE  
    ## 3 GL    PIK3CA
    ## 4 GL    SOX2  
    ## 5 GL    FGFR1 
    ## 6 TP53  FAT1  
    ## 
    ## $fit$clones_expansions$CRUK0080
    ## # A tibble: 7 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    EGFR 
    ## 2 GL    WT1  
    ## 3 GL    CCND1
    ## 4 EGFR  TP53 
    ## 5 TP53  IKZF1
    ## 6 WT1   IKZF1
    ## 7 CCND1 IKZF1
    ## 
    ## $fit$clones_expansions$CRUK0081
    ## # A tibble: 8 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     CDKN2A
    ## 2 CDKN2A TP53  
    ## 3 TP53   NOTCH1
    ## 4 TP53   FAT1  
    ## 5 TP53   FANCC 
    ## 6 NOTCH1 CYLD  
    ## 7 FAT1   CYLD  
    ## 8 FANCC  CYLD  
    ## 
    ## $fit$clones_expansions$CRUK0082
    ## # A tibble: 11 x 2
    ##    from   to    
    ##    <chr>  <chr> 
    ##  1 GL     FGFR1 
    ##  2 GL     PIK3CA
    ##  3 GL     SOX2  
    ##  4 GL     TP53  
    ##  5 GL     WT1   
    ##  6 GL     PTEN  
    ##  7 GL     KMT2D 
    ##  8 FGFR1  COL5A2
    ##  9 PIK3CA COL5A2
    ## 10 SOX2   COL5A2
    ## 11 TP53   COL5A2
    ## 
    ## $fit$clones_expansions$CRUK0083
    ## # A tibble: 7 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    RASA1 
    ## 2 GL    FBXW7 
    ## 3 GL    PIK3CA
    ## 4 GL    SOX2  
    ## 5 GL    FGFR1 
    ## 6 GL    MYC   
    ## 7 RASA1 TP53  
    ## 
    ## $fit$clones_expansions$CRUK0084
    ## # A tibble: 1 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    CREBBP
    ## 
    ## $fit$clones_expansions$CRUK0085
    ## # A tibble: 4 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    CHEK2 
    ## 2 GL    CREBBP
    ## 3 GL    LATS1 
    ## 4 GL    FANCM 
    ## 
    ## $fit$clones_expansions$CRUK0086
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    TP53 
    ## 2 GL    ARID2
    ## 3 TP53  FAT1 
    ## 
    ## $fit$clones_expansions$CRUK0087
    ## # A tibble: 5 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     PIK3CA
    ## 2 GL     TP53  
    ## 3 GL     ASXL1 
    ## 4 PIK3CA NFE2L2
    ## 5 TP53   NFE2L2
    ## 
    ## $fit$clones_expansions$CRUK0088
    ## # A tibble: 2 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    CUX1 
    ## 2 GL    TP53 
    ## 
    ## $fit$clones_expansions$CRUK0089
    ## # A tibble: 3 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    PIK3CA
    ## 2 GL    SMAD4 
    ## 3 GL    KEAP1 
    ## 
    ## $fit$clones_expansions$CRUK0090
    ## # A tibble: 5 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    CDKN2A
    ## 2 GL    NCOA6 
    ## 3 GL    CUX1  
    ## 4 GL    COL2A1
    ## 5 GL    NRAS  
    ## 
    ## $fit$clones_expansions$CRUK0091
    ## # A tibble: 3 x 2
    ##   from   to     
    ##   <chr>  <chr>  
    ## 1 GL     CDKN2A 
    ## 2 GL     SMARCA4
    ## 3 CDKN2A TP53   
    ## 
    ## $fit$clones_expansions$CRUK0092
    ## # A tibble: 5 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    RASA1 
    ## 2 GL    PIK3CA
    ## 3 RASA1 TP53  
    ## 4 TP53  SMAD4 
    ## 5 TP53  CBLB  
    ## 
    ## $fit$clones_expansions$CRUK0093
    ## # A tibble: 8 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     CDKN2A
    ## 2 GL     DICER1
    ## 3 GL     COL2A1
    ## 4 GL     GATA3 
    ## 5 CDKN2A TP53  
    ## 6 CDKN2A COL5A2
    ## 7 TP53   CIC   
    ## 8 TP53   COL5A2
    ## 
    ## $fit$clones_expansions$CRUK0094
    ## # A tibble: 2 x 2
    ##   from  to     
    ##   <chr> <chr>  
    ## 1 GL    SMARCA4
    ## 2 GL    TERT   
    ## 
    ## $fit$clones_expansions$CRUK0095
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    RASA1
    ## 2 RASA1 TP53 
    ## 3 TP53  NF1  
    ## 
    ## $fit$clones_expansions$CRUK0096
    ## # A tibble: 3 x 2
    ##   from  to    
    ##   <chr> <chr> 
    ## 1 GL    KRAS  
    ## 2 GL    SGK223
    ## 3 GL    MAP3K1
    ## 
    ## $fit$clones_expansions$CRUK0097
    ## # A tibble: 2 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    TP53 
    ## 2 GL    PTEN 
    ## 
    ## $fit$clones_expansions$CRUK0098
    ## # A tibble: 4 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    TP53 
    ## 2 GL    PTEN 
    ## 3 TP53  UBR5 
    ## 4 PTEN  UBR5 
    ## 
    ## $fit$clones_expansions$CRUK0099
    ## # A tibble: 3 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    STK11
    ## 2 GL    KEAP1
    ## 3 GL    TP53 
    ## 
    ## $fit$clones_expansions$CRUK0100
    ## # A tibble: 7 x 2
    ##   from   to    
    ##   <chr>  <chr> 
    ## 1 GL     CDKN2A
    ## 2 GL     PHOX2B
    ## 3 GL     STK11 
    ## 4 GL     SPEN  
    ## 5 CDKN2A TP53  
    ## 6 CDKN2A COL5A2
    ## 7 TP53   COL5A2
    ## 
    ## 
    ## 
    ## $cluster
    ## $cluster$distances
    ## $cluster$distances$matrix
    ##          CRUK0001 CRUK0002 CRUK0003 CRUK0004 CRUK0005 CRUK0006 CRUK0007
    ## CRUK0001        0       67       90       60      105      110       76
    ## CRUK0002        0        0       71       54       66       71       57
    ## CRUK0003        0        0        0       77      109      114       60
    ## CRUK0004        0        0        0        0       92       97       63
    ## CRUK0005        0        0        0        0        0       72       95
    ## CRUK0006        0        0        0        0        0        0      100
    ## CRUK0007        0        0        0        0        0        0        0
    ## CRUK0008        0        0        0        0        0        0        0
    ## CRUK0009        0        0        0        0        0        0        0
    ## CRUK0010        0        0        0        0        0        0        0
    ## CRUK0011        0        0        0        0        0        0        0
    ## CRUK0012        0        0        0        0        0        0        0
    ## CRUK0013        0        0        0        0        0        0        0
    ## CRUK0014        0        0        0        0        0        0        0
    ## CRUK0015        0        0        0        0        0        0        0
    ## CRUK0016        0        0        0        0        0        0        0
    ## CRUK0017        0        0        0        0        0        0        0
    ## CRUK0018        0        0        0        0        0        0        0
    ## CRUK0019        0        0        0        0        0        0        0
    ## CRUK0020        0        0        0        0        0        0        0
    ## CRUK0021        0        0        0        0        0        0        0
    ## CRUK0022        0        0        0        0        0        0        0
    ## CRUK0023        0        0        0        0        0        0        0
    ## CRUK0024        0        0        0        0        0        0        0
    ## CRUK0025        0        0        0        0        0        0        0
    ## CRUK0026        0        0        0        0        0        0        0
    ## CRUK0027        0        0        0        0        0        0        0
    ## CRUK0028        0        0        0        0        0        0        0
    ## CRUK0029        0        0        0        0        0        0        0
    ## CRUK0030        0        0        0        0        0        0        0
    ## CRUK0031        0        0        0        0        0        0        0
    ## CRUK0032        0        0        0        0        0        0        0
    ## CRUK0033        0        0        0        0        0        0        0
    ## CRUK0034        0        0        0        0        0        0        0
    ## CRUK0035        0        0        0        0        0        0        0
    ## CRUK0036        0        0        0        0        0        0        0
    ## CRUK0037        0        0        0        0        0        0        0
    ## CRUK0038        0        0        0        0        0        0        0
    ## CRUK0039        0        0        0        0        0        0        0
    ## CRUK0040        0        0        0        0        0        0        0
    ## CRUK0041        0        0        0        0        0        0        0
    ## CRUK0042        0        0        0        0        0        0        0
    ## CRUK0043        0        0        0        0        0        0        0
    ## CRUK0044        0        0        0        0        0        0        0
    ## CRUK0045        0        0        0        0        0        0        0
    ## CRUK0046        0        0        0        0        0        0        0
    ## CRUK0047        0        0        0        0        0        0        0
    ## CRUK0048        0        0        0        0        0        0        0
    ## CRUK0049        0        0        0        0        0        0        0
    ## CRUK0050        0        0        0        0        0        0        0
    ## CRUK0051        0        0        0        0        0        0        0
    ## CRUK0052        0        0        0        0        0        0        0
    ## CRUK0054        0        0        0        0        0        0        0
    ## CRUK0055        0        0        0        0        0        0        0
    ## CRUK0056        0        0        0        0        0        0        0
    ## CRUK0057        0        0        0        0        0        0        0
    ## CRUK0058        0        0        0        0        0        0        0
    ## CRUK0059        0        0        0        0        0        0        0
    ## CRUK0060        0        0        0        0        0        0        0
    ## CRUK0061        0        0        0        0        0        0        0
    ## CRUK0062        0        0        0        0        0        0        0
    ## CRUK0063        0        0        0        0        0        0        0
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0008 CRUK0009 CRUK0010 CRUK0011 CRUK0012 CRUK0013 CRUK0014
    ## CRUK0001       94      107       57       74       53       67      123
    ## CRUK0002       55       66       38       35       34       28       84
    ## CRUK0003       98      114       61       78       57       71      127
    ## CRUK0004       81       97       44       61       40       54      110
    ## CRUK0005       93       71       76       73       72       66       91
    ## CRUK0006       86       83       81       78       77       71       96
    ## CRUK0007       84      100       47       64       43       57      113
    ## CRUK0008        0       98       65       62       61       47      111
    ## CRUK0009        0        0       81       78       77       71       96
    ## CRUK0010        0        0        0       45       24       38       94
    ## CRUK0011        0        0        0        0       41       35       71
    ## CRUK0012        0        0        0        0        0       34       90
    ## CRUK0013        0        0        0        0        0        0       84
    ## CRUK0014        0        0        0        0        0        0        0
    ## CRUK0015        0        0        0        0        0        0        0
    ## CRUK0016        0        0        0        0        0        0        0
    ## CRUK0017        0        0        0        0        0        0        0
    ## CRUK0018        0        0        0        0        0        0        0
    ## CRUK0019        0        0        0        0        0        0        0
    ## CRUK0020        0        0        0        0        0        0        0
    ## CRUK0021        0        0        0        0        0        0        0
    ## CRUK0022        0        0        0        0        0        0        0
    ## CRUK0023        0        0        0        0        0        0        0
    ## CRUK0024        0        0        0        0        0        0        0
    ## CRUK0025        0        0        0        0        0        0        0
    ## CRUK0026        0        0        0        0        0        0        0
    ## CRUK0027        0        0        0        0        0        0        0
    ## CRUK0028        0        0        0        0        0        0        0
    ## CRUK0029        0        0        0        0        0        0        0
    ## CRUK0030        0        0        0        0        0        0        0
    ## CRUK0031        0        0        0        0        0        0        0
    ## CRUK0032        0        0        0        0        0        0        0
    ## CRUK0033        0        0        0        0        0        0        0
    ## CRUK0034        0        0        0        0        0        0        0
    ## CRUK0035        0        0        0        0        0        0        0
    ## CRUK0036        0        0        0        0        0        0        0
    ## CRUK0037        0        0        0        0        0        0        0
    ## CRUK0038        0        0        0        0        0        0        0
    ## CRUK0039        0        0        0        0        0        0        0
    ## CRUK0040        0        0        0        0        0        0        0
    ## CRUK0041        0        0        0        0        0        0        0
    ## CRUK0042        0        0        0        0        0        0        0
    ## CRUK0043        0        0        0        0        0        0        0
    ## CRUK0044        0        0        0        0        0        0        0
    ## CRUK0045        0        0        0        0        0        0        0
    ## CRUK0046        0        0        0        0        0        0        0
    ## CRUK0047        0        0        0        0        0        0        0
    ## CRUK0048        0        0        0        0        0        0        0
    ## CRUK0049        0        0        0        0        0        0        0
    ## CRUK0050        0        0        0        0        0        0        0
    ## CRUK0051        0        0        0        0        0        0        0
    ## CRUK0052        0        0        0        0        0        0        0
    ## CRUK0054        0        0        0        0        0        0        0
    ## CRUK0055        0        0        0        0        0        0        0
    ## CRUK0056        0        0        0        0        0        0        0
    ## CRUK0057        0        0        0        0        0        0        0
    ## CRUK0058        0        0        0        0        0        0        0
    ## CRUK0059        0        0        0        0        0        0        0
    ## CRUK0060        0        0        0        0        0        0        0
    ## CRUK0061        0        0        0        0        0        0        0
    ## CRUK0062        0        0        0        0        0        0        0
    ## CRUK0063        0        0        0        0        0        0        0
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0015 CRUK0016 CRUK0017 CRUK0018 CRUK0019 CRUK0020 CRUK0021
    ## CRUK0001       60      113      114       82       53      165       79
    ## CRUK0002       54       74       75       43       34      126       73
    ## CRUK0003       77      103      118       86       57      169       82
    ## CRUK0004       47      100      101       69       40      152       66
    ## CRUK0005       92      106       82       77       72      133      111
    ## CRUK0006       97      111       75       86       77      126      116
    ## CRUK0007       63      103      104       72       43      155       82
    ## CRUK0008       81      101       77       70       61      138      100
    ## CRUK0009       97      117       87       86       77      138      116
    ## CRUK0010       44       84       85       53       24      136       63
    ## CRUK0011       61       81       82       30       41      113       80
    ## CRUK0012       40       80       81       49       20      132       59
    ## CRUK0013       54       74       75       43       34      126       73
    ## CRUK0014      110      130      100       79       90      114      129
    ## CRUK0015        0      100      101       69       40      152       66
    ## CRUK0016        0        0      121       89       80      172       95
    ## CRUK0017        0        0        0       90       81      125      120
    ## CRUK0018        0        0        0        0       49      117       88
    ## CRUK0019        0        0        0        0        0      132       59
    ## CRUK0020        0        0        0        0        0        0      171
    ## CRUK0021        0        0        0        0        0        0        0
    ## CRUK0022        0        0        0        0        0        0        0
    ## CRUK0023        0        0        0        0        0        0        0
    ## CRUK0024        0        0        0        0        0        0        0
    ## CRUK0025        0        0        0        0        0        0        0
    ## CRUK0026        0        0        0        0        0        0        0
    ## CRUK0027        0        0        0        0        0        0        0
    ## CRUK0028        0        0        0        0        0        0        0
    ## CRUK0029        0        0        0        0        0        0        0
    ## CRUK0030        0        0        0        0        0        0        0
    ## CRUK0031        0        0        0        0        0        0        0
    ## CRUK0032        0        0        0        0        0        0        0
    ## CRUK0033        0        0        0        0        0        0        0
    ## CRUK0034        0        0        0        0        0        0        0
    ## CRUK0035        0        0        0        0        0        0        0
    ## CRUK0036        0        0        0        0        0        0        0
    ## CRUK0037        0        0        0        0        0        0        0
    ## CRUK0038        0        0        0        0        0        0        0
    ## CRUK0039        0        0        0        0        0        0        0
    ## CRUK0040        0        0        0        0        0        0        0
    ## CRUK0041        0        0        0        0        0        0        0
    ## CRUK0042        0        0        0        0        0        0        0
    ## CRUK0043        0        0        0        0        0        0        0
    ## CRUK0044        0        0        0        0        0        0        0
    ## CRUK0045        0        0        0        0        0        0        0
    ## CRUK0046        0        0        0        0        0        0        0
    ## CRUK0047        0        0        0        0        0        0        0
    ## CRUK0048        0        0        0        0        0        0        0
    ## CRUK0049        0        0        0        0        0        0        0
    ## CRUK0050        0        0        0        0        0        0        0
    ## CRUK0051        0        0        0        0        0        0        0
    ## CRUK0052        0        0        0        0        0        0        0
    ## CRUK0054        0        0        0        0        0        0        0
    ## CRUK0055        0        0        0        0        0        0        0
    ## CRUK0056        0        0        0        0        0        0        0
    ## CRUK0057        0        0        0        0        0        0        0
    ## CRUK0058        0        0        0        0        0        0        0
    ## CRUK0059        0        0        0        0        0        0        0
    ## CRUK0060        0        0        0        0        0        0        0
    ## CRUK0061        0        0        0        0        0        0        0
    ## CRUK0062        0        0        0        0        0        0        0
    ## CRUK0063        0        0        0        0        0        0        0
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0022 CRUK0023 CRUK0024 CRUK0025 CRUK0026 CRUK0027 CRUK0028
    ## CRUK0001       55      115       68      125       59      125       57
    ## CRUK0002       49       82       42       86       53       86       38
    ## CRUK0003       72      111       85      129       76      129       61
    ## CRUK0004       42      108       55      112       46      112       44
    ## CRUK0005       87      120       80       93       91       93       76
    ## CRUK0006       92      125       85       98       96       96       81
    ## CRUK0007       58      111       71      115       62      115       47
    ## CRUK0008       76      109       61      113       80      113       65
    ## CRUK0009       92      125       85       98       96       98       81
    ## CRUK0010       39       92       52       96       43       96       28
    ## CRUK0011       56       69       49       73       60       73       45
    ## CRUK0012       35       88       48       92       39       92       24
    ## CRUK0013       49       82       32       86       53       86       38
    ## CRUK0014      105      109       98       74      109       74       94
    ## CRUK0015       42      108       55      112       43      112       44
    ## CRUK0016       95      104       88      132       99      132       84
    ## CRUK0017       96      129       89      102      100      102       85
    ## CRUK0018       64       77       57       77       68       81       53
    ## CRUK0019       35       88       48       92       39       92       24
    ## CRUK0020      147      151      140      112      151      116      136
    ## CRUK0021       61      103       74      131       65      131       63
    ## CRUK0022        0      103       50      107       41      107       39
    ## CRUK0023        0        0       96      111      107      111       92
    ## CRUK0024        0        0        0      100       54      100       52
    ## CRUK0025        0        0        0        0      111       76       96
    ## CRUK0026        0        0        0        0        0      111       43
    ## CRUK0027        0        0        0        0        0        0       96
    ## CRUK0028        0        0        0        0        0        0        0
    ## CRUK0029        0        0        0        0        0        0        0
    ## CRUK0030        0        0        0        0        0        0        0
    ## CRUK0031        0        0        0        0        0        0        0
    ## CRUK0032        0        0        0        0        0        0        0
    ## CRUK0033        0        0        0        0        0        0        0
    ## CRUK0034        0        0        0        0        0        0        0
    ## CRUK0035        0        0        0        0        0        0        0
    ## CRUK0036        0        0        0        0        0        0        0
    ## CRUK0037        0        0        0        0        0        0        0
    ## CRUK0038        0        0        0        0        0        0        0
    ## CRUK0039        0        0        0        0        0        0        0
    ## CRUK0040        0        0        0        0        0        0        0
    ## CRUK0041        0        0        0        0        0        0        0
    ## CRUK0042        0        0        0        0        0        0        0
    ## CRUK0043        0        0        0        0        0        0        0
    ## CRUK0044        0        0        0        0        0        0        0
    ## CRUK0045        0        0        0        0        0        0        0
    ## CRUK0046        0        0        0        0        0        0        0
    ## CRUK0047        0        0        0        0        0        0        0
    ## CRUK0048        0        0        0        0        0        0        0
    ## CRUK0049        0        0        0        0        0        0        0
    ## CRUK0050        0        0        0        0        0        0        0
    ## CRUK0051        0        0        0        0        0        0        0
    ## CRUK0052        0        0        0        0        0        0        0
    ## CRUK0054        0        0        0        0        0        0        0
    ## CRUK0055        0        0        0        0        0        0        0
    ## CRUK0056        0        0        0        0        0        0        0
    ## CRUK0057        0        0        0        0        0        0        0
    ## CRUK0058        0        0        0        0        0        0        0
    ## CRUK0059        0        0        0        0        0        0        0
    ## CRUK0060        0        0        0        0        0        0        0
    ## CRUK0061        0        0        0        0        0        0        0
    ## CRUK0062        0        0        0        0        0        0        0
    ## CRUK0063        0        0        0        0        0        0        0
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0029 CRUK0030 CRUK0031 CRUK0032 CRUK0033 CRUK0034 CRUK0035
    ## CRUK0001       89      130       96       66       66       79       87
    ## CRUK0002       53       95       57       27       27       40       48
    ## CRUK0003       96      138       86       70       70       83       91
    ## CRUK0004       79      121       83       53       53       66       74
    ## CRUK0005       60      102       95       65       65       78       55
    ## CRUK0006       65      107       88       70       58       83       60
    ## CRUK0007       82      124       86       56       56       69       77
    ## CRUK0008       80      119       72       51       42       67       75
    ## CRUK0009       65      107      100       70       70       83       60
    ## CRUK0010       63      105       67       37       37       50       58
    ## CRUK0011       60       82       64       34       34       27       55
    ## CRUK0012       59      101       63       33       33       46       54
    ## CRUK0013       53       95       57       27       27       40       48
    ## CRUK0014       78       83      113       83       83       76       73
    ## CRUK0015       79      121       83       53       53       66       74
    ## CRUK0016       99      141       89       73       73       86       94
    ## CRUK0017       69      111       92       74       62       87       64
    ## CRUK0018       68       90       72       42       42       35       63
    ## CRUK0019       59      101       63       33       33       46       54
    ## CRUK0020      120      125      140      125      113      118      115
    ## CRUK0021       98      140       88       72       72       85       93
    ## CRUK0022       74      116       78       48       48       61       69
    ## CRUK0023      107      120       97       81       81       74      102
    ## CRUK0024       67      109       71       41       41       54       62
    ## CRUK0025       80       85      115       85       85       78       75
    ## CRUK0026       78      120       82       52       52       65       73
    ## CRUK0027       80       85      115       85       85       76       75
    ## CRUK0028       63      105       67       37       37       50       58
    ## CRUK0029        0       89       82       52       52       65       42
    ## CRUK0030        0        0      124       91       94       87       84
    ## CRUK0031        0        0        0       56       44       69       77
    ## CRUK0032        0        0        0        0       26       37       47
    ## CRUK0033        0        0        0        0        0       39       47
    ## CRUK0034        0        0        0        0        0        0       60
    ## CRUK0035        0        0        0        0        0        0        0
    ## CRUK0036        0        0        0        0        0        0        0
    ## CRUK0037        0        0        0        0        0        0        0
    ## CRUK0038        0        0        0        0        0        0        0
    ## CRUK0039        0        0        0        0        0        0        0
    ## CRUK0040        0        0        0        0        0        0        0
    ## CRUK0041        0        0        0        0        0        0        0
    ## CRUK0042        0        0        0        0        0        0        0
    ## CRUK0043        0        0        0        0        0        0        0
    ## CRUK0044        0        0        0        0        0        0        0
    ## CRUK0045        0        0        0        0        0        0        0
    ## CRUK0046        0        0        0        0        0        0        0
    ## CRUK0047        0        0        0        0        0        0        0
    ## CRUK0048        0        0        0        0        0        0        0
    ## CRUK0049        0        0        0        0        0        0        0
    ## CRUK0050        0        0        0        0        0        0        0
    ## CRUK0051        0        0        0        0        0        0        0
    ## CRUK0052        0        0        0        0        0        0        0
    ## CRUK0054        0        0        0        0        0        0        0
    ## CRUK0055        0        0        0        0        0        0        0
    ## CRUK0056        0        0        0        0        0        0        0
    ## CRUK0057        0        0        0        0        0        0        0
    ## CRUK0058        0        0        0        0        0        0        0
    ## CRUK0059        0        0        0        0        0        0        0
    ## CRUK0060        0        0        0        0        0        0        0
    ## CRUK0061        0        0        0        0        0        0        0
    ## CRUK0062        0        0        0        0        0        0        0
    ## CRUK0063        0        0        0        0        0        0        0
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0036 CRUK0037 CRUK0038 CRUK0039 CRUK0040 CRUK0041 CRUK0042
    ## CRUK0001       97       80       76       82       79       60       73
    ## CRUK0002       55       41       37       43       40       41       34
    ## CRUK0003       81       84       80       86       83       64       77
    ## CRUK0004       84       67       63       69       66       47       60
    ## CRUK0005       96       79       75       77       78       72       72
    ## CRUK0006       89       84       80       86       83       84       77
    ## CRUK0007       67       70       66       72       69       50       63
    ## CRUK0008       73       68       64       70       67       68       61
    ## CRUK0009       99       84       80       86       83       77       77
    ## CRUK0010       68       51       47       53       50       31       44
    ## CRUK0011       65       28       24       30       27       48       21
    ## CRUK0012       64       47       43       49       46       27       40
    ## CRUK0013       58       41       37       43       40       41       34
    ## CRUK0014      114       77       73       79       76       97       70
    ## CRUK0015       84       67       63       69       66       47       60
    ## CRUK0016      104       87       83       89       86       87       80
    ## CRUK0017       93       88       84       90       87       88       81
    ## CRUK0018       73       36       32       34       35       56       29
    ## CRUK0019       64       47       43       49       46       27       40
    ## CRUK0020      141      119      115      121      116      139      112
    ## CRUK0021      103       86       82       88       85       66       79
    ## CRUK0022       79       62       58       64       61       42       55
    ## CRUK0023      112       75       68       77       74       95       68
    ## CRUK0024       72       55       51       57       54       55       48
    ## CRUK0025      116       79       75       81       78       99       72
    ## CRUK0026       83       66       62       68       65       46       59
    ## CRUK0027      116       79       75       81       78       99       72
    ## CRUK0028       68       51       47       53       50       31       44
    ## CRUK0029       83       66       62       68       65       66       59
    ## CRUK0030      125       88       84       90       87      108       81
    ## CRUK0031       75       70       66       72       69       70       63
    ## CRUK0032       57       40       36       42       37       40       33
    ## CRUK0033       45       40       36       42       39       40       33
    ## CRUK0034       70       33       29       35       32       53       26
    ## CRUK0035       78       61       57       63       60       61       54
    ## CRUK0036        0       71       67       73       70       71       64
    ## CRUK0037        0        0       30       36       33       54       27
    ## CRUK0038        0        0        0       32       29       50       23
    ## CRUK0039        0        0        0        0       35       56       29
    ## CRUK0040        0        0        0        0        0       53       26
    ## CRUK0041        0        0        0        0        0        0       47
    ## CRUK0042        0        0        0        0        0        0        0
    ## CRUK0043        0        0        0        0        0        0        0
    ## CRUK0044        0        0        0        0        0        0        0
    ## CRUK0045        0        0        0        0        0        0        0
    ## CRUK0046        0        0        0        0        0        0        0
    ## CRUK0047        0        0        0        0        0        0        0
    ## CRUK0048        0        0        0        0        0        0        0
    ## CRUK0049        0        0        0        0        0        0        0
    ## CRUK0050        0        0        0        0        0        0        0
    ## CRUK0051        0        0        0        0        0        0        0
    ## CRUK0052        0        0        0        0        0        0        0
    ## CRUK0054        0        0        0        0        0        0        0
    ## CRUK0055        0        0        0        0        0        0        0
    ## CRUK0056        0        0        0        0        0        0        0
    ## CRUK0057        0        0        0        0        0        0        0
    ## CRUK0058        0        0        0        0        0        0        0
    ## CRUK0059        0        0        0        0        0        0        0
    ## CRUK0060        0        0        0        0        0        0        0
    ## CRUK0061        0        0        0        0        0        0        0
    ## CRUK0062        0        0        0        0        0        0        0
    ## CRUK0063        0        0        0        0        0        0        0
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0043 CRUK0044 CRUK0045 CRUK0046 CRUK0047 CRUK0048 CRUK0049
    ## CRUK0001       56       73       55       69       78       72      129
    ## CRUK0002       14       34       16       30       39       69      123
    ## CRUK0003       60       77       59       73       82       92      146
    ## CRUK0004       43       60       42       56       65       62      116
    ## CRUK0005       55       72       54       68       77      103      130
    ## CRUK0006       60       77       59       61       82      112      135
    ## CRUK0007       46       63       45       59       68       78      132
    ## CRUK0008       44       61       43       45       50       86      150
    ## CRUK0009       57       77       59       73       82      105      135
    ## CRUK0010       27       44       26       40       49       59      113
    ## CRUK0011       24       21       23       37       46       76      110
    ## CRUK0012       23       40       22       36       45       55      109
    ## CRUK0013       17       34       16       30       28       69      123
    ## CRUK0014       73       70       72       86       95      125      111
    ## CRUK0015       43       60       40       56       65       62      113
    ## CRUK0016       63       80       62       76       85      115      169
    ## CRUK0017       64       81       63       65       78      108      139
    ## CRUK0018       32       29       31       45       54       84      118
    ## CRUK0019       23       40       22       36       45       55      109
    ## CRUK0020      115      112      114      116      137      167      148
    ## CRUK0021       62       79       61       75       84       81      135
    ## CRUK0022       38       55       37       51       60       57      111
    ## CRUK0023       71       68       70       84       93      123      148
    ## CRUK0024       31       48       30       44       45       70      124
    ## CRUK0025       75       72       74       88       97      127      113
    ## CRUK0026       42       59       41       55       64       61      112
    ## CRUK0027       75       72       74       88       97      127      113
    ## CRUK0028       27       44       26       36       45       55      113
    ## CRUK0029       42       59       41       55       64       94      117
    ## CRUK0030       84       81       83       97      106      136      122
    ## CRUK0031       46       63       45       47       68       98      152
    ## CRUK0032       16       33       15       29       38       68      122
    ## CRUK0033       16       33       15       17       38       68      122
    ## CRUK0034       29       26       28       42       51       81      115
    ## CRUK0035       37       54       36       50       59       89      112
    ## CRUK0036       47       64       46       48       69       99      153
    ## CRUK0037       30       27       29       43       52       82      116
    ## CRUK0038       26       23       25       39       48       78      112
    ## CRUK0039       32       29       31       45       54       84      118
    ## CRUK0040       29       26       28       42       51       81      115
    ## CRUK0041       30       47       29       43       52       58      116
    ## CRUK0042       23       20       22       36       45       75      109
    ## CRUK0043        0       23        5       19       28       58      112
    ## CRUK0044        0        0       22       36       45       75      109
    ## CRUK0045        0        0        0       18       27       57      111
    ## CRUK0046        0        0        0        0       37       67      125
    ## CRUK0047        0        0        0        0        0       68      134
    ## CRUK0048        0        0        0        0        0        0      131
    ## CRUK0049        0        0        0        0        0        0        0
    ## CRUK0050        0        0        0        0        0        0        0
    ## CRUK0051        0        0        0        0        0        0        0
    ## CRUK0052        0        0        0        0        0        0        0
    ## CRUK0054        0        0        0        0        0        0        0
    ## CRUK0055        0        0        0        0        0        0        0
    ## CRUK0056        0        0        0        0        0        0        0
    ## CRUK0057        0        0        0        0        0        0        0
    ## CRUK0058        0        0        0        0        0        0        0
    ## CRUK0059        0        0        0        0        0        0        0
    ## CRUK0060        0        0        0        0        0        0        0
    ## CRUK0061        0        0        0        0        0        0        0
    ## CRUK0062        0        0        0        0        0        0        0
    ## CRUK0063        0        0        0        0        0        0        0
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0050 CRUK0051 CRUK0052 CRUK0054 CRUK0055 CRUK0056 CRUK0057
    ## CRUK0001       74      129      159       53       58       69       66
    ## CRUK0002       35      123      126       34       19       30       24
    ## CRUK0003       78      146      169       57       62       73       70
    ## CRUK0004       61      116      152       40       45       56       53
    ## CRUK0005       73      130      133       72       57       68       65
    ## CRUK0006       78      135      126       77       62       73       70
    ## CRUK0007       64      132      152       43       48       59       56
    ## CRUK0008       46      150      141       61       46       57       54
    ## CRUK0009       78      135      138       77       62       73       70
    ## CRUK0010       45      113      136       24       29       40       34
    ## CRUK0011       42      110      113       41       26       37       34
    ## CRUK0012       41      109      132       20       25       36       33
    ## CRUK0013       24      123      126       34       19       30       27
    ## CRUK0014       91      111      114       90       75       86       83
    ## CRUK0015       61      116      152       40       45       56       53
    ## CRUK0016       81      169      172       80       65       76       71
    ## CRUK0017       74      139      130       81       66       77       74
    ## CRUK0018       50      118      117       49       34       45       42
    ## CRUK0019       41      109      132       20       25       36       33
    ## CRUK0020      133      153      137      132      117      128      125
    ## CRUK0021       80      135      171       59       64       75       72
    ## CRUK0022       56      111      147       35       40       51       48
    ## CRUK0023       89      148      148       88       73       84       81
    ## CRUK0024       41      124      140       48       33       44       41
    ## CRUK0025       93      113      112       92       77       88       85
    ## CRUK0026       60      115      151       39       44       55       52
    ## CRUK0027       93      113      116       92       77       88       85
    ## CRUK0028       45      113      136       24       29       40       37
    ## CRUK0029       60      117      120       59       44       55       52
    ## CRUK0030      102      118      121      101       86       97       92
    ## CRUK0031       64      152      141       63       48       59       56
    ## CRUK0032       34      122      125       33       18       29       26
    ## CRUK0033       34      122      113       33       18       29       26
    ## CRUK0034       47      115      118       46       31       42       39
    ## CRUK0035       55      112      115       54       39       50       47
    ## CRUK0036       65      153      141       64       49       60       54
    ## CRUK0037       48      116      119       47       32       39       40
    ## CRUK0038       44      112      112       43       28       39       36
    ## CRUK0039       50      118      121       49       34       45       42
    ## CRUK0040       47      115      118       46       31       42       39
    ## CRUK0041       48      116      139       27       32       43       40
    ## CRUK0042       41      109      112       40       25       36       33
    ## CRUK0043       24      112      115       23        8       19       16
    ## CRUK0044       41      109      112       40       25       36       33
    ## CRUK0045       23      111      114       22        7       18       15
    ## CRUK0046       37      125      116       36       21       32       29
    ## CRUK0047       25      134      137       45       30       41       38
    ## CRUK0048       68      131      167       55       60       71       68
    ## CRUK0049      130      117      153      109      114      125      122
    ## CRUK0050        0      130      133       41       26       37       34
    ## CRUK0051        0        0      153      109      114      125      122
    ## CRUK0052        0        0        0      132      117      128      125
    ## CRUK0054        0        0        0        0       25       36       33
    ## CRUK0055        0        0        0        0        0       21       18
    ## CRUK0056        0        0        0        0        0        0       29
    ## CRUK0057        0        0        0        0        0        0        0
    ## CRUK0058        0        0        0        0        0        0        0
    ## CRUK0059        0        0        0        0        0        0        0
    ## CRUK0060        0        0        0        0        0        0        0
    ## CRUK0061        0        0        0        0        0        0        0
    ## CRUK0062        0        0        0        0        0        0        0
    ## CRUK0063        0        0        0        0        0        0        0
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0058 CRUK0059 CRUK0060 CRUK0061 CRUK0062 CRUK0063 CRUK0064
    ## CRUK0001       53       73       88       61      137      140       92
    ## CRUK0002       47       34       49       22       98       97       53
    ## CRUK0003       70       77       92       65      121      110       96
    ## CRUK0004       40       60       75       48      124      127       79
    ## CRUK0005       85       72       87       60      105      133       60
    ## CRUK0006       90       77       92       65      110      138       65
    ## CRUK0007       56       63       78       51      107      110       82
    ## CRUK0008       74       61       76       41      125      128       80
    ## CRUK0009       90       77       90       65      110      144       65
    ## CRUK0010       37       44       59       32      108      111       63
    ## CRUK0011       54       21       56       29      105      108       60
    ## CRUK0012       33       40       55       28      104      107       59
    ## CRUK0013       47       34       49       14       98      101       53
    ## CRUK0014      103       70      105       78      123      157       78
    ## CRUK0015       40       60       75       48      124      127       79
    ## CRUK0016       93       80       95       68      144      117       92
    ## CRUK0017       94       81       96       69      114      148       69
    ## CRUK0018       62       29       64       37      113      116       68
    ## CRUK0019       33       40       55       28      104      107       59
    ## CRUK0020      145      112      142      120      165      196      120
    ## CRUK0021       59       79       94       67      143      122       98
    ## CRUK0022       35       55       70       43      119      122       74
    ## CRUK0023      101       68      103       76      152      131      107
    ## CRUK0024       48       48       63       28      112      115       67
    ## CRUK0025      105       72      107       80      125      159       80
    ## CRUK0026       39       59       71       47      123      126       78
    ## CRUK0027      105       72      107       80      125      159       80
    ## CRUK0028       37       44       59       32      108      111       63
    ## CRUK0029       72       59       74       47       88      126       47
    ## CRUK0030      114       81      116       89      134      164       89
    ## CRUK0031       76       63       78       51      127      113       82
    ## CRUK0032       46       33       48       21       97      100       52
    ## CRUK0033       46       33       48       21       97      100       52
    ## CRUK0034       59       26       61       34      110      113       65
    ## CRUK0035       67       54       69       42       85      121       42
    ## CRUK0036       77       64       79       52      108      108       83
    ## CRUK0037       60       27       59       35      111      114       66
    ## CRUK0038       56       23       58       31      107      110       62
    ## CRUK0039       62       29       59       37      113      116       68
    ## CRUK0040       59       26       61       34      110      113       65
    ## CRUK0041       40       47       62       35      111      114       66
    ## CRUK0042       53       20       55       28      104      107       59
    ## CRUK0043       36       23       38       11       87       90       42
    ## CRUK0044       53       20       55       28      104      107       59
    ## CRUK0045       35       22       37       10       86       89       41
    ## CRUK0046       49       36       51       24      100      103       55
    ## CRUK0047       58       45       60       25      109      112       64
    ## CRUK0048       55       75       90       63      139      142       94
    ## CRUK0049      109      109      139      117      162      196      117
    ## CRUK0050       54       41       56       21      105      108       60
    ## CRUK0051      109      109      144      117      162      190      117
    ## CRUK0052      145      112      144      120      162      199      120
    ## CRUK0054       33       40       55       28      104      107       59
    ## CRUK0055       38       25       40       13       89       92       44
    ## CRUK0056       49       36       45       24      100      103       55
    ## CRUK0057       46       33       48       21       97      100       52
    ## CRUK0058        0       53       68       41      117      120       72
    ## CRUK0059        0        0       55       28      104      107       59
    ## CRUK0060        0        0        0       43      119      120       74
    ## CRUK0061        0        0        0        0       92       95       47
    ## CRUK0062        0        0        0        0        0      137       92
    ## CRUK0063        0        0        0        0        0        0      126
    ## CRUK0064        0        0        0        0        0        0        0
    ## CRUK0065        0        0        0        0        0        0        0
    ## CRUK0066        0        0        0        0        0        0        0
    ## CRUK0067        0        0        0        0        0        0        0
    ## CRUK0068        0        0        0        0        0        0        0
    ## CRUK0069        0        0        0        0        0        0        0
    ## CRUK0070        0        0        0        0        0        0        0
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0065 CRUK0066 CRUK0067 CRUK0068 CRUK0069 CRUK0070 CRUK0071
    ## CRUK0001      136       96      121      144      105      110       96
    ## CRUK0002       97       63       82      105       66       71       57
    ## CRUK0003      120       92       91      128      109      114       80
    ## CRUK0004      123       84      103      131       92       97       83
    ## CRUK0005      104       95      120      106       73       78       91
    ## CRUK0006      109      100      125      111       78       83      100
    ## CRUK0007      106       92       91      114       95      100       66
    ## CRUK0008      124       90      109      132       93       98       84
    ## CRUK0009      104      106      125      117       78       83      100
    ## CRUK0010      107       73       92      115       76       81       67
    ## CRUK0011      104       70       89      112       73       78       64
    ## CRUK0012      103       69       88      111       72       77       63
    ## CRUK0013       97       63       82      105       66       71       57
    ## CRUK0014      122      119      138      130       91       96      113
    ## CRUK0015      123       89      108      131       92       97       83
    ## CRUK0016      143       79      104      145      105      117      103
    ## CRUK0017      113      110      129      121       82       87      104
    ## CRUK0018      112       78       97      120       81       86       68
    ## CRUK0019      103       69       88      111       72       77       63
    ## CRUK0020      164      161      180      172      133      138      155
    ## CRUK0021      142       84      103      150      111      116      102
    ## CRUK0022      118       84      103      126       87       92       78
    ## CRUK0023      151       87      112      159      120      125      111
    ## CRUK0024      111       77       96      119       80       85       71
    ## CRUK0025      124      121      140      132       93       98      115
    ## CRUK0026      122       88      107      130       91       96       82
    ## CRUK0027      124      121      140      132       93       98      115
    ## CRUK0028      107       73       92      115       76       81       67
    ## CRUK0029       91       88      107       99       60       65       82
    ## CRUK0030      133      130      149      141      102      107      124
    ## CRUK0031      126       78       97      134       86      100       86
    ## CRUK0032       96       62       81      104       65       70       56
    ## CRUK0033       96       62       81      104       65       70       56
    ## CRUK0034      109       75       94      117       78       83       69
    ## CRUK0035       86       83      102       94       55       60       77
    ## CRUK0036      107       93       92      112       96      101       67
    ## CRUK0037      110       76       95      118       79       84       70
    ## CRUK0038      106       72       91      114       75       80       66
    ## CRUK0039      112       78       97      120       81       86       68
    ## CRUK0040      109       75       94      117       78       83       69
    ## CRUK0041      110       76       95      118       79       84       70
    ## CRUK0042      103       69       88      111       72       77       63
    ## CRUK0043       86       52       71       94       55       60       46
    ## CRUK0044      103       69       88      111       72       77       63
    ## CRUK0045       85       51       70       93       54       59       45
    ## CRUK0046       99       65       84      107       68       73       59
    ## CRUK0047      108       74       93      116       77       82       68
    ## CRUK0048      138      104      123      146      107      112       98
    ## CRUK0049      161      158      177      169      130      135      152
    ## CRUK0050      104       70       89      112       73       78       64
    ## CRUK0051      161      158      177      169      130      135      152
    ## CRUK0052      164      161      180      172      133      138      155
    ## CRUK0054      103       69       88      111       72       77       63
    ## CRUK0055       88       54       73       96       57       62       48
    ## CRUK0056       99       65       84      107       68       73       59
    ## CRUK0057       96       62       81      104       65       70       56
    ## CRUK0058      116       82      101      124       85       90       76
    ## CRUK0059      103       69       88      111       72       77       63
    ## CRUK0060      118       82      103      126       87       92       78
    ## CRUK0061       91       57       76       99       60       65       51
    ## CRUK0062      102      133      118      110      105       96       89
    ## CRUK0063      136      106       97      133      139      130       96
    ## CRUK0064       91       88      107       99       53       65       82
    ## CRUK0065        0      132      117      109      104       95       92
    ## CRUK0066        0        0       88      134       99      106       92
    ## CRUK0067        0        0        0      125      120      111       77
    ## CRUK0068        0        0        0        0      112      103      100
    ## CRUK0069        0        0        0        0        0       78       95
    ## CRUK0070        0        0        0        0        0        0       86
    ## CRUK0071        0        0        0        0        0        0        0
    ## CRUK0072        0        0        0        0        0        0        0
    ## CRUK0073        0        0        0        0        0        0        0
    ## CRUK0074        0        0        0        0        0        0        0
    ## CRUK0075        0        0        0        0        0        0        0
    ## CRUK0076        0        0        0        0        0        0        0
    ## CRUK0077        0        0        0        0        0        0        0
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0072 CRUK0073 CRUK0074 CRUK0075 CRUK0076 CRUK0077 CRUK0078
    ## CRUK0001      107      102      138      114      143       97      102
    ## CRUK0002      101       63       99       78      104       58       63
    ## CRUK0003      104       92      122      101      127      101       86
    ## CRUK0004       94       89      125       99      130       84       89
    ## CRUK0005      139      101      106      116      111       65      101
    ## CRUK0006      144      106      111      121      116       58      106
    ## CRUK0007       90       92      108       87      113       87       72
    ## CRUK0008      120       82      126      105      131       73       90
    ## CRUK0009      139      106      106      121      116       70      106
    ## CRUK0010       91       73      109       88      114       68       73
    ## CRUK0011      108       70      106       85      111       65       70
    ## CRUK0012       87       69      105       84      110       64       69
    ## CRUK0013      101       63       99       78      104       58       63
    ## CRUK0014      157      119      124      134      129       83      119
    ## CRUK0015       94       89      125      104      130       84       89
    ## CRUK0016      147       95      145      117      150      104      109
    ## CRUK0017      140      102      115      125      118       62      110
    ## CRUK0018      116       78      114       93      119       73       78
    ## CRUK0019       87       69      105       84      110       64       69
    ## CRUK0020      199      161      166      176      171      113      161
    ## CRUK0021      113       94      144      123      149      103      108
    ## CRUK0022       89       84      120       99      125       79       84
    ## CRUK0023      155      101      153      132      158      112      117
    ## CRUK0024      102       77      113       92      118       72       77
    ## CRUK0025      159      121      126      136      131       85      121
    ## CRUK0026       93       88      124      103      126       83       88
    ## CRUK0027      159      121      126      136      131       85      121
    ## CRUK0028       91       73      109       88      114       68       73
    ## CRUK0029      126       88       89      100       98       52       88
    ## CRUK0030      168      130      135      145      140       94      130
    ## CRUK0031      130       69      128       98      124       75       83
    ## CRUK0032      100       62       98       77      103       57       62
    ## CRUK0033      100       62       98       77      103       45       62
    ## CRUK0034      113       75      111       90      116       70       75
    ## CRUK0035      121       83       88       98       93       47       83
    ## CRUK0036      111       93      109       88      114       76       73
    ## CRUK0037      114       76      112       91      117       71       76
    ## CRUK0038      110       72      108       87      113       67       72
    ## CRUK0039      116       78      114       93      119       73       78
    ## CRUK0040      113       75      111       90      116       70       75
    ## CRUK0041       94       76      112       91      117       71       76
    ## CRUK0042      107       69      105       84      110       64       69
    ## CRUK0043       90       52       88       67       93       47       52
    ## CRUK0044      107       69      105       84      110       64       69
    ## CRUK0045       89       51       87       66       92       46       51
    ## CRUK0046      103       65      101       80      106       48       65
    ## CRUK0047      104       66      110       89      115       69       74
    ## CRUK0048      101       96      140      119      145       99      104
    ## CRUK0049      163      158      163      173      168      122      158
    ## CRUK0050      100       62      106       85      111       65       70
    ## CRUK0051      163      158      163      173      168      122      158
    ## CRUK0052      199      158      166      176      171      113      161
    ## CRUK0054       87       69      105       84      110       64       69
    ## CRUK0055       92       54       90       69       95       49       54
    ## CRUK0056      103       65      101       69      106       60       65
    ## CRUK0057      100       62       98       77      103       57       62
    ## CRUK0058       87       82      118       97      123       77       82
    ## CRUK0059      107       69      105       84      110       64       69
    ## CRUK0060      122       81      120       93      120       79       84
    ## CRUK0061       95       57       93       72       98       52       57
    ## CRUK0062      137      133       98      128      109       97       99
    ## CRUK0063      140      122      138      131      143      131      102
    ## CRUK0064      126       88       93       96       98       52       88
    ## CRUK0065      124      132       89      127      108       96       98
    ## CRUK0066      136       84      134      108      139       93       98
    ## CRUK0067      121      103      119      103      124      112       83
    ## CRUK0068      144      140      111      135      116      104      101
    ## CRUK0069      139       92      106      100      102       65       92
    ## CRUK0070      130      106       97      121       99       70       92
    ## CRUK0071       96       92       94       87       99       87       58
    ## CRUK0072        0      128      126      131      143      131      102
    ## CRUK0073        0        0      134      100      130       93       89
    ## CRUK0074        0        0        0      129      110       98      100
    ## CRUK0075        0        0        0        0      125      108       84
    ## CRUK0076        0        0        0        0        0      103       96
    ## CRUK0077        0        0        0        0        0        0       93
    ## CRUK0078        0        0        0        0        0        0        0
    ## CRUK0079        0        0        0        0        0        0        0
    ## CRUK0080        0        0        0        0        0        0        0
    ## CRUK0081        0        0        0        0        0        0        0
    ## CRUK0082        0        0        0        0        0        0        0
    ## CRUK0083        0        0        0        0        0        0        0
    ## CRUK0084        0        0        0        0        0        0        0
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0079 CRUK0080 CRUK0081 CRUK0082 CRUK0083 CRUK0084 CRUK0085
    ## CRUK0001      136       62       93      147      119       57       62
    ## CRUK0002       97       56       54      108       80       18       23
    ## CRUK0003      120       79       83      131      103       61       66
    ## CRUK0004      123       49       75      134      106       44       49
    ## CRUK0005      104       94       92      115      118       56       61
    ## CRUK0006      109       99       97      120      123       61       66
    ## CRUK0007      106       65       83      117       89       47       52
    ## CRUK0008      124       83       81      135       99       45       50
    ## CRUK0009      109       99       97      120      123       61       66
    ## CRUK0010      107       46       64      118       90       28       33
    ## CRUK0011      104       63       61      115       87       25       30
    ## CRUK0012      103       42       60      114       86       24       29
    ## CRUK0013       97       56       54      108       80       18       23
    ## CRUK0014      122      112      110      133      136       74       79
    ## CRUK0015      123       49       80      134      106       44       49
    ## CRUK0016      136      102       69      154      126       64       69
    ## CRUK0017      113      103      101      124      119       65       70
    ## CRUK0018      112       71       69      123       95       33       38
    ## CRUK0019      103       42       60      114       86       24       29
    ## CRUK0020      164      154      152      175      178      116      121
    ## CRUK0021      142       68       75      153      125       63       66
    ## CRUK0022      118       44       75      129      101       39       44
    ## CRUK0023      151      110       84      162      134       72       77
    ## CRUK0024      109       57       68      122       94       32       37
    ## CRUK0025      124      114      112      135      138       76       81
    ## CRUK0026      122       48       79      133      105       43       48
    ## CRUK0027      124      114      112      135      138       76       81
    ## CRUK0028      107       46       64      118       90       28       33
    ## CRUK0029       91       77       79      102      105       43       48
    ## CRUK0030      133      123      121      144      143       85       90
    ## CRUK0031      117       85       69      128      100       47       52
    ## CRUK0032       96       55       53      107       79       17       22
    ## CRUK0033       96       55       53      107       79       17       22
    ## CRUK0034      109       68       66      120       92       30       35
    ## CRUK0035       86       76       74       97      100       38       43
    ## CRUK0036      107       86       84      118       90       48       53
    ## CRUK0037      110       69       67      121       93       27       32
    ## CRUK0038      106       65       63      117       89       27       32
    ## CRUK0039      112       71       69      123       95       33       38
    ## CRUK0040      109       68       66      120       92       30       35
    ## CRUK0041      110       49       67      121       93       31       36
    ## CRUK0042      103       62       60      114       86       24       29
    ## CRUK0043       86       45       43       97       69        7       12
    ## CRUK0044      103       62       60      114       86       24       29
    ## CRUK0045       85       44       42       96       68        6       11
    ## CRUK0046       99       58       56      110       82       20       25
    ## CRUK0047      108       67       65      119       83       29       34
    ## CRUK0048      138       64       95      149      113       59       64
    ## CRUK0049      161      118      149      172      175      113      118
    ## CRUK0050      104       63       61      115       79       25       30
    ## CRUK0051      161      118      149      172      171      113      118
    ## CRUK0052      164      154      152      175      178      116      121
    ## CRUK0054      103       42       60      114       86       24       29
    ## CRUK0055       88       47       45       99       71        9       12
    ## CRUK0056       99       58       56      110       71       16       21
    ## CRUK0057       96       55       53      107       79       17       22
    ## CRUK0058      116       42       73      127       99       37       42
    ## CRUK0059      103       62       60      114       86       24       29
    ## CRUK0060      118       77       75      129       95       39       44
    ## CRUK0061       91       50       48      102       74       12       17
    ## CRUK0062      102      122      124      113      116       88       93
    ## CRUK0063      136      129      103      147      115       91       96
    ## CRUK0064       84       81       72      102      105       43       48
    ## CRUK0065      101      125      123      112      115       87       92
    ## CRUK0066      132       91       60      143      115       53       58
    ## CRUK0067      117      110       79      128      100       72       77
    ## CRUK0068      109      133      131      113      123       95      100
    ## CRUK0069       88       94       85      106      109       56       61
    ## CRUK0070       95       99       97       99      109       61       66
    ## CRUK0071       92       85       83      103       75       47       52
    ## CRUK0072      136       96      127      147      111       91       96
    ## CRUK0073      123       91       75      134       98       53       58
    ## CRUK0074      103      123      125      114      117       89       94
    ## CRUK0075      111      106       92      129       90       68       73
    ## CRUK0076       99      132      130      103      113       94       99
    ## CRUK0077       96       86       84      107      110       48       53
    ## CRUK0078       89       91       89       95       72       53       58
    ## CRUK0079        0      125      116      103      106       87       92
    ## CRUK0080        0        0       82      134      108       46       51
    ## CRUK0081        0        0        0      134      106       44       49
    ## CRUK0082        0        0        0        0      117       98      103
    ## CRUK0083        0        0        0        0        0       70       75
    ## CRUK0084        0        0        0        0        0        0        9
    ## CRUK0085        0        0        0        0        0        0        0
    ## CRUK0086        0        0        0        0        0        0        0
    ## CRUK0087        0        0        0        0        0        0        0
    ## CRUK0088        0        0        0        0        0        0        0
    ## CRUK0089        0        0        0        0        0        0        0
    ## CRUK0090        0        0        0        0        0        0        0
    ## CRUK0091        0        0        0        0        0        0        0
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0086 CRUK0087 CRUK0088 CRUK0089 CRUK0090 CRUK0091 CRUK0092
    ## CRUK0001       93      114       86       86       78       80       88
    ## CRUK0002       54       75       47       47       39       41       49
    ## CRUK0003       97       98       90       70       68       70       72
    ## CRUK0004       80      101       73       73       65       67       73
    ## CRUK0005       61       82       54       85       77       79       87
    ## CRUK0006       66       87       59       78       82       84       92
    ## CRUK0007       83       84       76       56       68       70       58
    ## CRUK0008       81      102       74       62       66       68       76
    ## CRUK0009       66       82       59       90       82       84       92
    ## CRUK0010       64       85       57       57       49       51       59
    ## CRUK0011       61       82       54       54       46       48       56
    ## CRUK0012       60       81       53       53       45       47       55
    ## CRUK0013       54       75       47       47       39       41       49
    ## CRUK0014       79      100       72      103       95       97      105
    ## CRUK0015       80      101       73       73       65       67       75
    ## CRUK0016       93      121       93       93       71       63       93
    ## CRUK0017       70       91       63       82       86       88       96
    ## CRUK0018       69       90       62       62       54       56       64
    ## CRUK0019       60       81       53       53       45       47       55
    ## CRUK0020      121      142      114      133      132      139      147
    ## CRUK0021       99      120       92       92       70       62       94
    ## CRUK0022       75       96       68       68       60       62       70
    ## CRUK0023      108      129      101      101       79       71      103
    ## CRUK0024       68       89       61       61       53       55       63
    ## CRUK0025       81      102       74      105       97       99      107
    ## CRUK0026       79      100       72       72       64       66       74
    ## CRUK0027       81      102       74      105       97       99      107
    ## CRUK0028       64       85       57       57       49       51       59
    ## CRUK0029       48       69       41       72       64       66       74
    ## CRUK0030       90      111       83      114      106      108      116
    ## CRUK0031       83      104       76       64       54       56       78
    ## CRUK0032       53       74       46       46       38       40       48
    ## CRUK0033       53       74       46       34       38       40       48
    ## CRUK0034       66       87       59       59       51       53       61
    ## CRUK0035       43       64       36       67       59       61       69
    ## CRUK0036       84       85       77       45       69       71       59
    ## CRUK0037       67       88       60       60       49       54       62
    ## CRUK0038       63       84       56       56       48       50       58
    ## CRUK0039       69       90       62       62       54       56       64
    ## CRUK0040       66       87       59       59       51       53       61
    ## CRUK0041       67       88       60       60       52       54       62
    ## CRUK0042       60       81       53       53       45       47       55
    ## CRUK0043       43       64       36       36       28       30       38
    ## CRUK0044       60       81       53       53       45       47       55
    ## CRUK0045       42       63       35       35       27       29       37
    ## CRUK0046       56       77       49       37       41       43       51
    ## CRUK0047       65       86       58       58       50       52       60
    ## CRUK0048       95      116       88       88       80       82       90
    ## CRUK0049      118      139      111      142      129      136      144
    ## CRUK0050       61       82       54       54       46       48       56
    ## CRUK0051      118      139      111      142      134      136      144
    ## CRUK0052      121      142      114      133      137      139      147
    ## CRUK0054       60       81       53       53       45       47       55
    ## CRUK0055       45       66       38       38       30       32       40
    ## CRUK0056       56       77       49       49       41       43       40
    ## CRUK0057       53       74       46       46       38       37       48
    ## CRUK0058       73       94       66       66       58       60       68
    ## CRUK0059       60       81       53       53       45       47       55
    ## CRUK0060       73       96       68       68       52       62       64
    ## CRUK0061       48       69       41       41       33       35       43
    ## CRUK0062       93       94       86       97      109      111       99
    ## CRUK0063      127      128      120      100       98       90      102
    ## CRUK0064       41       69       41       72       64       66       74
    ## CRUK0065       92       84       85       96      108      110       98
    ## CRUK0066       89      110       82       82       60       52       84
    ## CRUK0067      108      109      101       81       79       71       83
    ## CRUK0068      100      101       93      104      116      118      106
    ## CRUK0069       54       82       54       85       77       79       87
    ## CRUK0070       66       87       59       90       82       84       92
    ## CRUK0071       83       84       76       56       68       70       58
    ## CRUK0072      127      119      120      100      112      114      102
    ## CRUK0073       89      110       82       82       60       62       84
    ## CRUK0074       94       86       87       98      110      112      100
    ## CRUK0075       97      105       97       77       89       91       68
    ## CRUK0076       99      100       92      103      115      117      105
    ## CRUK0077       53       74       46       65       69       71       79
    ## CRUK0078       89       90       82       62       74       76       64
    ## CRUK0079       85       93       85       96      108      110       98
    ## CRUK0080       82      103       75       75       67       69       77
    ## CRUK0081       73      101       73       73       51       43       75
    ## CRUK0082      103      104       96      107      119      121      109
    ## CRUK0083      106      107       99       79       91       93       70
    ## CRUK0084       44       65       37       37       29       31       39
    ## CRUK0085       49       70       42       42       34       36       44
    ## CRUK0086        0       70       42       73       65       67       75
    ## CRUK0087        0        0       63       74       86       88       76
    ## CRUK0088        0        0        0       66       56       60       68
    ## CRUK0089        0        0        0        0       58       60       48
    ## CRUK0090        0        0        0        0        0       38       60
    ## CRUK0091        0        0        0        0        0        0       62
    ## CRUK0092        0        0        0        0        0        0        0
    ## CRUK0093        0        0        0        0        0        0        0
    ## CRUK0094        0        0        0        0        0        0        0
    ## CRUK0095        0        0        0        0        0        0        0
    ## CRUK0096        0        0        0        0        0        0        0
    ## CRUK0097        0        0        0        0        0        0        0
    ## CRUK0098        0        0        0        0        0        0        0
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0093 CRUK0094 CRUK0095 CRUK0096 CRUK0097 CRUK0098 CRUK0099
    ## CRUK0001       94       59       64       77       89       93      104
    ## CRUK0002       55       20       29       38       50       54       65
    ## CRUK0003       84       63       72       81       93       97      108
    ## CRUK0004       81       46       55       64       76       80       91
    ## CRUK0005       93       58       67       76       57       61       72
    ## CRUK0006       98       63       72       81       62       66       65
    ## CRUK0007       84       49       58       64       79       83       94
    ## CRUK0008       82       47       56       65       77       81       72
    ## CRUK0009       98       63       72       81       62       66       77
    ## CRUK0010       65       27       39       48       60       64       75
    ## CRUK0011       62       27       36       25       57       61       72
    ## CRUK0012       61       26       35       44       56       60       71
    ## CRUK0013       55       20       29       38       50       54       57
    ## CRUK0014      111       76       85       74       75       79       90
    ## CRUK0015       81       46       55       64       76       80       91
    ## CRUK0016       77       66       75       84       96      100      111
    ## CRUK0017      102       67       76       85       66       70       69
    ## CRUK0018       70       35       44       33       65       69       80
    ## CRUK0019       61       26       35       44       56       60       71
    ## CRUK0020      148      118      127      116      117      121      120
    ## CRUK0021       76       65       74       83       95       99      110
    ## CRUK0022       74       41       50       59       71       75       86
    ## CRUK0023       85       74       83       72      104      108      119
    ## CRUK0024       69       34       43       52       64       68       71
    ## CRUK0025      113       78       87       76       77       81       92
    ## CRUK0026       80       45       54       63       75       79       90
    ## CRUK0027      113       78       87       76       77       81       92
    ## CRUK0028       65       30       39       48       60       64       75
    ## CRUK0029       80       45       54       63       44       48       59
    ## CRUK0030      122       87       92       85       86       90      101
    ## CRUK0031       70       49       58       67       79       83       82
    ## CRUK0032       54       19       28       37       49       53       64
    ## CRUK0033       54       19       28       37       49       53       52
    ## CRUK0034       67       32       41       30       62       66       77
    ## CRUK0035       75       40       49       58       39       43       54
    ## CRUK0036       85       50       59       68       80       84       83
    ## CRUK0037       68       33       42       31       63       67       78
    ## CRUK0038       64       29       38       27       59       63       74
    ## CRUK0039       70       35       44       33       65       69       80
    ## CRUK0040       65       32       41       30       62       66       77
    ## CRUK0041       68       33       42       51       63       67       78
    ## CRUK0042       61       26       35       24       56       60       71
    ## CRUK0043       44        9       18       27       39       43       54
    ## CRUK0044       61       26       35       24       56       60       71
    ## CRUK0045       43        8       17       26       38       42       53
    ## CRUK0046       57       22       31       40       52       56       55
    ## CRUK0047       66       31       40       49       61       65       68
    ## CRUK0048       96       61       70       79       91       95      106
    ## CRUK0049      145      115      124      113      114      118      129
    ## CRUK0050       62       27       36       45       57       61       64
    ## CRUK0051      150      115      124      113      114      118      129
    ## CRUK0052      153      118      123      113      117      118      120
    ## CRUK0054       61       26       35       44       56       60       71
    ## CRUK0055       46       11       20       29       41       45       56
    ## CRUK0056       57       22       20       40       52       56       67
    ## CRUK0057       54       13       28       37       49       53       64
    ## CRUK0058       74       39       48       57       69       73       84
    ## CRUK0059       61       26       35       24       56       60       71
    ## CRUK0060       71       41       44       59       71       75       86
    ## CRUK0061       49       14       23       32       44       48       51
    ## CRUK0062      125       90       99      108       89       90      104
    ## CRUK0063      104       93      102      111      123      127      138
    ## CRUK0064       80       45       54       63       44       48       59
    ## CRUK0065      124       89       98      107       88       92      103
    ## CRUK0066       66       55       64       73       85       89      100
    ## CRUK0067       85       74       83       92      104      108      119
    ## CRUK0068      132       97      106      115       91       95      111
    ## CRUK0069       93       58       67       76       57       61       72
    ## CRUK0070       94       63       72       81       62       66       77
    ## CRUK0071       84       49       58       67       79       83       94
    ## CRUK0072      128       93      102      111      123      127      138
    ## CRUK0073       74       55       64       73       85       89      100
    ## CRUK0074      126       91      100      109       90       94      105
    ## CRUK0075      105       70       68       88      100      104      115
    ## CRUK0076      131       96      105      114       95       99      110
    ## CRUK0077       85       50       59       68       49       53       52
    ## CRUK0078       90       55       64       73       80       84      100
    ## CRUK0079      124       89       98      107       88       92      103
    ## CRUK0080       83       48       57       66       78       82       93
    ## CRUK0081       57       46       55       64       76       80       91
    ## CRUK0082      131      100      109      118       94       98      114
    ## CRUK0083      107       72       70       90      102      106      117
    ## CRUK0084       45       10       19       28       40       44       55
    ## CRUK0085       50       15       24       33       45       49       60
    ## CRUK0086       81       46       55       64       45       49       60
    ## CRUK0087      102       67       76       85       66       70       81
    ## CRUK0088       74       39       48       57       38       42       53
    ## CRUK0089       74       39       48       57       69       73       72
    ## CRUK0090       47       31       40       49       61       65       76
    ## CRUK0091       44       30       42       51       63       67       78
    ## CRUK0092       76       41       39       59       71       75       86
    ## CRUK0093        0       47       56       65       77       81       92
    ## CRUK0094        0        0       21       30       42       46       57
    ## CRUK0095        0        0        0       39       51       55       66
    ## CRUK0096        0        0        0        0       60       64       75
    ## CRUK0097        0        0        0        0        0       40       56
    ## CRUK0098        0        0        0        0        0        0       60
    ## CRUK0099        0        0        0        0        0        0        0
    ## CRUK0100        0        0        0        0        0        0        0
    ##          CRUK0100
    ## CRUK0001       96
    ## CRUK0002       57
    ## CRUK0003       86
    ## CRUK0004       83
    ## CRUK0005       95
    ## CRUK0006      100
    ## CRUK0007       86
    ## CRUK0008       76
    ## CRUK0009      100
    ## CRUK0010       67
    ## CRUK0011       64
    ## CRUK0012       63
    ## CRUK0013       49
    ## CRUK0014      113
    ## CRUK0015       83
    ## CRUK0016       77
    ## CRUK0017      104
    ## CRUK0018       72
    ## CRUK0019       63
    ## CRUK0020      155
    ## CRUK0021       78
    ## CRUK0022       78
    ## CRUK0023       87
    ## CRUK0024       63
    ## CRUK0025      115
    ## CRUK0026       82
    ## CRUK0027      115
    ## CRUK0028       67
    ## CRUK0029       82
    ## CRUK0030      124
    ## CRUK0031       72
    ## CRUK0032       56
    ## CRUK0033       56
    ## CRUK0034       69
    ## CRUK0035       77
    ## CRUK0036       87
    ## CRUK0037       70
    ## CRUK0038       66
    ## CRUK0039       69
    ## CRUK0040       69
    ## CRUK0041       70
    ## CRUK0042       63
    ## CRUK0043       46
    ## CRUK0044       63
    ## CRUK0045       45
    ## CRUK0046       59
    ## CRUK0047       60
    ## CRUK0048       98
    ## CRUK0049      152
    ## CRUK0050       56
    ## CRUK0051      152
    ## CRUK0052      155
    ## CRUK0054       63
    ## CRUK0055       48
    ## CRUK0056       59
    ## CRUK0057       56
    ## CRUK0058       76
    ## CRUK0059       63
    ## CRUK0060       75
    ## CRUK0061       43
    ## CRUK0062      127
    ## CRUK0063      106
    ## CRUK0064       82
    ## CRUK0065      126
    ## CRUK0066       68
    ## CRUK0067       87
    ## CRUK0068      134
    ## CRUK0069       95
    ## CRUK0070       96
    ## CRUK0071       86
    ## CRUK0072      130
    ## CRUK0073       78
    ## CRUK0074      128
    ## CRUK0075      107
    ## CRUK0076      133
    ## CRUK0077       87
    ## CRUK0078       92
    ## CRUK0079      126
    ## CRUK0080       85
    ## CRUK0081       59
    ## CRUK0082      133
    ## CRUK0083      109
    ## CRUK0084       47
    ## CRUK0085       52
    ## CRUK0086       83
    ## CRUK0087      104
    ## CRUK0088       76
    ## CRUK0089       76
    ## CRUK0090       54
    ## CRUK0091       46
    ## CRUK0092       78
    ## CRUK0093       54
    ## CRUK0094       49
    ## CRUK0095       58
    ## CRUK0096       67
    ## CRUK0097       79
    ## CRUK0098       83
    ## CRUK0099       86
    ## CRUK0100        0
    ## 
    ## $cluster$distances$dist_obj
    ##          CRUK0001 CRUK0002 CRUK0003 CRUK0004 CRUK0005 CRUK0006 CRUK0007
    ## CRUK0001                67       90       60      105      110       76
    ## CRUK0002       67                71       54       66       71       57
    ## CRUK0003       90       71                77      109      114       60
    ## CRUK0004       60       54       77                92       97       63
    ## CRUK0005      105       66      109       92                72       95
    ## CRUK0006      110       71      114       97       72               100
    ## CRUK0007       76       57       60       63       95      100         
    ## CRUK0008       94       55       98       81       93       86       84
    ## CRUK0009      107       66      114       97       71       83      100
    ## CRUK0010       57       38       61       44       76       81       47
    ## CRUK0011       74       35       78       61       73       78       64
    ## CRUK0012       53       34       57       40       72       77       43
    ## CRUK0013       67       28       71       54       66       71       57
    ## CRUK0014      123       84      127      110       91       96      113
    ## CRUK0015       60       54       77       47       92       97       63
    ## CRUK0016      113       74      103      100      106      111      103
    ## CRUK0017      114       75      118      101       82       75      104
    ## CRUK0018       82       43       86       69       77       86       72
    ## CRUK0019       53       34       57       40       72       77       43
    ## CRUK0020      165      126      169      152      133      126      155
    ## CRUK0021       79       73       82       66      111      116       82
    ## CRUK0022       55       49       72       42       87       92       58
    ## CRUK0023      115       82      111      108      120      125      111
    ## CRUK0024       68       42       85       55       80       85       71
    ## CRUK0025      125       86      129      112       93       98      115
    ## CRUK0026       59       53       76       46       91       96       62
    ## CRUK0027      125       86      129      112       93       96      115
    ## CRUK0028       57       38       61       44       76       81       47
    ## CRUK0029       89       53       96       79       60       65       82
    ## CRUK0030      130       95      138      121      102      107      124
    ## CRUK0031       96       57       86       83       95       88       86
    ## CRUK0032       66       27       70       53       65       70       56
    ## CRUK0033       66       27       70       53       65       58       56
    ## CRUK0034       79       40       83       66       78       83       69
    ## CRUK0035       87       48       91       74       55       60       77
    ## CRUK0036       97       55       81       84       96       89       67
    ## CRUK0037       80       41       84       67       79       84       70
    ## CRUK0038       76       37       80       63       75       80       66
    ## CRUK0039       82       43       86       69       77       86       72
    ## CRUK0040       79       40       83       66       78       83       69
    ## CRUK0041       60       41       64       47       72       84       50
    ## CRUK0042       73       34       77       60       72       77       63
    ## CRUK0043       56       14       60       43       55       60       46
    ## CRUK0044       73       34       77       60       72       77       63
    ## CRUK0045       55       16       59       42       54       59       45
    ## CRUK0046       69       30       73       56       68       61       59
    ## CRUK0047       78       39       82       65       77       82       68
    ## CRUK0048       72       69       92       62      103      112       78
    ## CRUK0049      129      123      146      116      130      135      132
    ## CRUK0050       74       35       78       61       73       78       64
    ## CRUK0051      129      123      146      116      130      135      132
    ## CRUK0052      159      126      169      152      133      126      152
    ## CRUK0054       53       34       57       40       72       77       43
    ## CRUK0055       58       19       62       45       57       62       48
    ## CRUK0056       69       30       73       56       68       73       59
    ## CRUK0057       66       24       70       53       65       70       56
    ## CRUK0058       53       47       70       40       85       90       56
    ## CRUK0059       73       34       77       60       72       77       63
    ## CRUK0060       88       49       92       75       87       92       78
    ## CRUK0061       61       22       65       48       60       65       51
    ## CRUK0062      137       98      121      124      105      110      107
    ## CRUK0063      140       97      110      127      133      138      110
    ## CRUK0064       92       53       96       79       60       65       82
    ## CRUK0065      136       97      120      123      104      109      106
    ## CRUK0066       96       63       92       84       95      100       92
    ## CRUK0067      121       82       91      103      120      125       91
    ## CRUK0068      144      105      128      131      106      111      114
    ## CRUK0069      105       66      109       92       73       78       95
    ## CRUK0070      110       71      114       97       78       83      100
    ## CRUK0071       96       57       80       83       91      100       66
    ## CRUK0072      107      101      104       94      139      144       90
    ## CRUK0073      102       63       92       89      101      106       92
    ## CRUK0074      138       99      122      125      106      111      108
    ## CRUK0075      114       78      101       99      116      121       87
    ## CRUK0076      143      104      127      130      111      116      113
    ## CRUK0077       97       58      101       84       65       58       87
    ## CRUK0078      102       63       86       89      101      106       72
    ## CRUK0079      136       97      120      123      104      109      106
    ## CRUK0080       62       56       79       49       94       99       65
    ## CRUK0081       93       54       83       75       92       97       83
    ## CRUK0082      147      108      131      134      115      120      117
    ## CRUK0083      119       80      103      106      118      123       89
    ## CRUK0084       57       18       61       44       56       61       47
    ## CRUK0085       62       23       66       49       61       66       52
    ## CRUK0086       93       54       97       80       61       66       83
    ## CRUK0087      114       75       98      101       82       87       84
    ## CRUK0088       86       47       90       73       54       59       76
    ## CRUK0089       86       47       70       73       85       78       56
    ## CRUK0090       78       39       68       65       77       82       68
    ## CRUK0091       80       41       70       67       79       84       70
    ## CRUK0092       88       49       72       73       87       92       58
    ## CRUK0093       94       55       84       81       93       98       84
    ## CRUK0094       59       20       63       46       58       63       49
    ## CRUK0095       64       29       72       55       67       72       58
    ## CRUK0096       77       38       81       64       76       81       64
    ## CRUK0097       89       50       93       76       57       62       79
    ## CRUK0098       93       54       97       80       61       66       83
    ## CRUK0099      104       65      108       91       72       65       94
    ## CRUK0100       96       57       86       83       95      100       86
    ##          CRUK0008 CRUK0009 CRUK0010 CRUK0011 CRUK0012 CRUK0013 CRUK0014
    ## CRUK0001       94      107       57       74       53       67      123
    ## CRUK0002       55       66       38       35       34       28       84
    ## CRUK0003       98      114       61       78       57       71      127
    ## CRUK0004       81       97       44       61       40       54      110
    ## CRUK0005       93       71       76       73       72       66       91
    ## CRUK0006       86       83       81       78       77       71       96
    ## CRUK0007       84      100       47       64       43       57      113
    ## CRUK0008                98       65       62       61       47      111
    ## CRUK0009       98                81       78       77       71       96
    ## CRUK0010       65       81                45       24       38       94
    ## CRUK0011       62       78       45                41       35       71
    ## CRUK0012       61       77       24       41                34       90
    ## CRUK0013       47       71       38       35       34                84
    ## CRUK0014      111       96       94       71       90       84         
    ## CRUK0015       81       97       44       61       40       54      110
    ## CRUK0016      101      117       84       81       80       74      130
    ## CRUK0017       77       87       85       82       81       75      100
    ## CRUK0018       70       86       53       30       49       43       79
    ## CRUK0019       61       77       24       41       20       34       90
    ## CRUK0020      138      138      136      113      132      126      114
    ## CRUK0021      100      116       63       80       59       73      129
    ## CRUK0022       76       92       39       56       35       49      105
    ## CRUK0023      109      125       92       69       88       82      109
    ## CRUK0024       61       85       52       49       48       32       98
    ## CRUK0025      113       98       96       73       92       86       74
    ## CRUK0026       80       96       43       60       39       53      109
    ## CRUK0027      113       98       96       73       92       86       74
    ## CRUK0028       65       81       28       45       24       38       94
    ## CRUK0029       80       65       63       60       59       53       78
    ## CRUK0030      119      107      105       82      101       95       83
    ## CRUK0031       72      100       67       64       63       57      113
    ## CRUK0032       51       70       37       34       33       27       83
    ## CRUK0033       42       70       37       34       33       27       83
    ## CRUK0034       67       83       50       27       46       40       76
    ## CRUK0035       75       60       58       55       54       48       73
    ## CRUK0036       73       99       68       65       64       58      114
    ## CRUK0037       68       84       51       28       47       41       77
    ## CRUK0038       64       80       47       24       43       37       73
    ## CRUK0039       70       86       53       30       49       43       79
    ## CRUK0040       67       83       50       27       46       40       76
    ## CRUK0041       68       77       31       48       27       41       97
    ## CRUK0042       61       77       44       21       40       34       70
    ## CRUK0043       44       57       27       24       23       17       73
    ## CRUK0044       61       77       44       21       40       34       70
    ## CRUK0045       43       59       26       23       22       16       72
    ## CRUK0046       45       73       40       37       36       30       86
    ## CRUK0047       50       82       49       46       45       28       95
    ## CRUK0048       86      105       59       76       55       69      125
    ## CRUK0049      150      135      113      110      109      123      111
    ## CRUK0050       46       78       45       42       41       24       91
    ## CRUK0051      150      135      113      110      109      123      111
    ## CRUK0052      141      138      136      113      132      126      114
    ## CRUK0054       61       77       24       41       20       34       90
    ## CRUK0055       46       62       29       26       25       19       75
    ## CRUK0056       57       73       40       37       36       30       86
    ## CRUK0057       54       70       34       34       33       27       83
    ## CRUK0058       74       90       37       54       33       47      103
    ## CRUK0059       61       77       44       21       40       34       70
    ## CRUK0060       76       90       59       56       55       49      105
    ## CRUK0061       41       65       32       29       28       14       78
    ## CRUK0062      125      110      108      105      104       98      123
    ## CRUK0063      128      144      111      108      107      101      157
    ## CRUK0064       80       65       63       60       59       53       78
    ## CRUK0065      124      104      107      104      103       97      122
    ## CRUK0066       90      106       73       70       69       63      119
    ## CRUK0067      109      125       92       89       88       82      138
    ## CRUK0068      132      117      115      112      111      105      130
    ## CRUK0069       93       78       76       73       72       66       91
    ## CRUK0070       98       83       81       78       77       71       96
    ## CRUK0071       84      100       67       64       63       57      113
    ## CRUK0072      120      139       91      108       87      101      157
    ## CRUK0073       82      106       73       70       69       63      119
    ## CRUK0074      126      106      109      106      105       99      124
    ## CRUK0075      105      121       88       85       84       78      134
    ## CRUK0076      131      116      114      111      110      104      129
    ## CRUK0077       73       70       68       65       64       58       83
    ## CRUK0078       90      106       73       70       69       63      119
    ## CRUK0079      124      109      107      104      103       97      122
    ## CRUK0080       83       99       46       63       42       56      112
    ## CRUK0081       81       97       64       61       60       54      110
    ## CRUK0082      135      120      118      115      114      108      133
    ## CRUK0083       99      123       90       87       86       80      136
    ## CRUK0084       45       61       28       25       24       18       74
    ## CRUK0085       50       66       33       30       29       23       79
    ## CRUK0086       81       66       64       61       60       54       79
    ## CRUK0087      102       82       85       82       81       75      100
    ## CRUK0088       74       59       57       54       53       47       72
    ## CRUK0089       62       90       57       54       53       47      103
    ## CRUK0090       66       82       49       46       45       39       95
    ## CRUK0091       68       84       51       48       47       41       97
    ## CRUK0092       76       92       59       56       55       49      105
    ## CRUK0093       82       98       65       62       61       55      111
    ## CRUK0094       47       63       27       27       26       20       76
    ## CRUK0095       56       72       39       36       35       29       85
    ## CRUK0096       65       81       48       25       44       38       74
    ## CRUK0097       77       62       60       57       56       50       75
    ## CRUK0098       81       66       64       61       60       54       79
    ## CRUK0099       72       77       75       72       71       57       90
    ## CRUK0100       76      100       67       64       63       49      113
    ##          CRUK0015 CRUK0016 CRUK0017 CRUK0018 CRUK0019 CRUK0020 CRUK0021
    ## CRUK0001       60      113      114       82       53      165       79
    ## CRUK0002       54       74       75       43       34      126       73
    ## CRUK0003       77      103      118       86       57      169       82
    ## CRUK0004       47      100      101       69       40      152       66
    ## CRUK0005       92      106       82       77       72      133      111
    ## CRUK0006       97      111       75       86       77      126      116
    ## CRUK0007       63      103      104       72       43      155       82
    ## CRUK0008       81      101       77       70       61      138      100
    ## CRUK0009       97      117       87       86       77      138      116
    ## CRUK0010       44       84       85       53       24      136       63
    ## CRUK0011       61       81       82       30       41      113       80
    ## CRUK0012       40       80       81       49       20      132       59
    ## CRUK0013       54       74       75       43       34      126       73
    ## CRUK0014      110      130      100       79       90      114      129
    ## CRUK0015               100      101       69       40      152       66
    ## CRUK0016      100               121       89       80      172       95
    ## CRUK0017      101      121                90       81      125      120
    ## CRUK0018       69       89       90                49      117       88
    ## CRUK0019       40       80       81       49               132       59
    ## CRUK0020      152      172      125      117      132               171
    ## CRUK0021       66       95      120       88       59      171         
    ## CRUK0022       42       95       96       64       35      147       61
    ## CRUK0023      108      104      129       77       88      151      103
    ## CRUK0024       55       88       89       57       48      140       74
    ## CRUK0025      112      132      102       77       92      112      131
    ## CRUK0026       43       99      100       68       39      151       65
    ## CRUK0027      112      132      102       81       92      116      131
    ## CRUK0028       44       84       85       53       24      136       63
    ## CRUK0029       79       99       69       68       59      120       98
    ## CRUK0030      121      141      111       90      101      125      140
    ## CRUK0031       83       89       92       72       63      140       88
    ## CRUK0032       53       73       74       42       33      125       72
    ## CRUK0033       53       73       62       42       33      113       72
    ## CRUK0034       66       86       87       35       46      118       85
    ## CRUK0035       74       94       64       63       54      115       93
    ## CRUK0036       84      104       93       73       64      141      103
    ## CRUK0037       67       87       88       36       47      119       86
    ## CRUK0038       63       83       84       32       43      115       82
    ## CRUK0039       69       89       90       34       49      121       88
    ## CRUK0040       66       86       87       35       46      116       85
    ## CRUK0041       47       87       88       56       27      139       66
    ## CRUK0042       60       80       81       29       40      112       79
    ## CRUK0043       43       63       64       32       23      115       62
    ## CRUK0044       60       80       81       29       40      112       79
    ## CRUK0045       40       62       63       31       22      114       61
    ## CRUK0046       56       76       65       45       36      116       75
    ## CRUK0047       65       85       78       54       45      137       84
    ## CRUK0048       62      115      108       84       55      167       81
    ## CRUK0049      113      169      139      118      109      148      135
    ## CRUK0050       61       81       74       50       41      133       80
    ## CRUK0051      116      169      139      118      109      153      135
    ## CRUK0052      152      172      130      117      132      137      171
    ## CRUK0054       40       80       81       49       20      132       59
    ## CRUK0055       45       65       66       34       25      117       64
    ## CRUK0056       56       76       77       45       36      128       75
    ## CRUK0057       53       71       74       42       33      125       72
    ## CRUK0058       40       93       94       62       33      145       59
    ## CRUK0059       60       80       81       29       40      112       79
    ## CRUK0060       75       95       96       64       55      142       94
    ## CRUK0061       48       68       69       37       28      120       67
    ## CRUK0062      124      144      114      113      104      165      143
    ## CRUK0063      127      117      148      116      107      196      122
    ## CRUK0064       79       92       69       68       59      120       98
    ## CRUK0065      123      143      113      112      103      164      142
    ## CRUK0066       89       79      110       78       69      161       84
    ## CRUK0067      108      104      129       97       88      180      103
    ## CRUK0068      131      145      121      120      111      172      150
    ## CRUK0069       92      105       82       81       72      133      111
    ## CRUK0070       97      117       87       86       77      138      116
    ## CRUK0071       83      103      104       68       63      155      102
    ## CRUK0072       94      147      140      116       87      199      113
    ## CRUK0073       89       95      102       78       69      161       94
    ## CRUK0074      125      145      115      114      105      166      144
    ## CRUK0075      104      117      125       93       84      176      123
    ## CRUK0076      130      150      118      119      110      171      149
    ## CRUK0077       84      104       62       73       64      113      103
    ## CRUK0078       89      109      110       78       69      161      108
    ## CRUK0079      123      136      113      112      103      164      142
    ## CRUK0080       49      102      103       71       42      154       68
    ## CRUK0081       80       69      101       69       60      152       75
    ## CRUK0082      134      154      124      123      114      175      153
    ## CRUK0083      106      126      119       95       86      178      125
    ## CRUK0084       44       64       65       33       24      116       63
    ## CRUK0085       49       69       70       38       29      121       66
    ## CRUK0086       80       93       70       69       60      121       99
    ## CRUK0087      101      121       91       90       81      142      120
    ## CRUK0088       73       93       63       62       53      114       92
    ## CRUK0089       73       93       82       62       53      133       92
    ## CRUK0090       65       71       86       54       45      132       70
    ## CRUK0091       67       63       88       56       47      139       62
    ## CRUK0092       75       93       96       64       55      147       94
    ## CRUK0093       81       77      102       70       61      148       76
    ## CRUK0094       46       66       67       35       26      118       65
    ## CRUK0095       55       75       76       44       35      127       74
    ## CRUK0096       64       84       85       33       44      116       83
    ## CRUK0097       76       96       66       65       56      117       95
    ## CRUK0098       80      100       70       69       60      121       99
    ## CRUK0099       91      111       69       80       71      120      110
    ## CRUK0100       83       77      104       72       63      155       78
    ##          CRUK0022 CRUK0023 CRUK0024 CRUK0025 CRUK0026 CRUK0027 CRUK0028
    ## CRUK0001       55      115       68      125       59      125       57
    ## CRUK0002       49       82       42       86       53       86       38
    ## CRUK0003       72      111       85      129       76      129       61
    ## CRUK0004       42      108       55      112       46      112       44
    ## CRUK0005       87      120       80       93       91       93       76
    ## CRUK0006       92      125       85       98       96       96       81
    ## CRUK0007       58      111       71      115       62      115       47
    ## CRUK0008       76      109       61      113       80      113       65
    ## CRUK0009       92      125       85       98       96       98       81
    ## CRUK0010       39       92       52       96       43       96       28
    ## CRUK0011       56       69       49       73       60       73       45
    ## CRUK0012       35       88       48       92       39       92       24
    ## CRUK0013       49       82       32       86       53       86       38
    ## CRUK0014      105      109       98       74      109       74       94
    ## CRUK0015       42      108       55      112       43      112       44
    ## CRUK0016       95      104       88      132       99      132       84
    ## CRUK0017       96      129       89      102      100      102       85
    ## CRUK0018       64       77       57       77       68       81       53
    ## CRUK0019       35       88       48       92       39       92       24
    ## CRUK0020      147      151      140      112      151      116      136
    ## CRUK0021       61      103       74      131       65      131       63
    ## CRUK0022               103       50      107       41      107       39
    ## CRUK0023      103                96      111      107      111       92
    ## CRUK0024       50       96               100       54      100       52
    ## CRUK0025      107      111      100               111       76       96
    ## CRUK0026       41      107       54      111               111       43
    ## CRUK0027      107      111      100       76      111                96
    ## CRUK0028       39       92       52       96       43       96         
    ## CRUK0029       74      107       67       80       78       80       63
    ## CRUK0030      116      120      109       85      120       85      105
    ## CRUK0031       78       97       71      115       82      115       67
    ## CRUK0032       48       81       41       85       52       85       37
    ## CRUK0033       48       81       41       85       52       85       37
    ## CRUK0034       61       74       54       78       65       76       50
    ## CRUK0035       69      102       62       75       73       75       58
    ## CRUK0036       79      112       72      116       83      116       68
    ## CRUK0037       62       75       55       79       66       79       51
    ## CRUK0038       58       68       51       75       62       75       47
    ## CRUK0039       64       77       57       81       68       81       53
    ## CRUK0040       61       74       54       78       65       78       50
    ## CRUK0041       42       95       55       99       46       99       31
    ## CRUK0042       55       68       48       72       59       72       44
    ## CRUK0043       38       71       31       75       42       75       27
    ## CRUK0044       55       68       48       72       59       72       44
    ## CRUK0045       37       70       30       74       41       74       26
    ## CRUK0046       51       84       44       88       55       88       36
    ## CRUK0047       60       93       45       97       64       97       45
    ## CRUK0048       57      123       70      127       61      127       55
    ## CRUK0049      111      148      124      113      112      113      113
    ## CRUK0050       56       89       41       93       60       93       45
    ## CRUK0051      111      148      124      113      115      113      113
    ## CRUK0052      147      148      140      112      151      116      136
    ## CRUK0054       35       88       48       92       39       92       24
    ## CRUK0055       40       73       33       77       44       77       29
    ## CRUK0056       51       84       44       88       55       88       40
    ## CRUK0057       48       81       41       85       52       85       37
    ## CRUK0058       35      101       48      105       39      105       37
    ## CRUK0059       55       68       48       72       59       72       44
    ## CRUK0060       70      103       63      107       71      107       59
    ## CRUK0061       43       76       28       80       47       80       32
    ## CRUK0062      119      152      112      125      123      125      108
    ## CRUK0063      122      131      115      159      126      159      111
    ## CRUK0064       74      107       67       80       78       80       63
    ## CRUK0065      118      151      111      124      122      124      107
    ## CRUK0066       84       87       77      121       88      121       73
    ## CRUK0067      103      112       96      140      107      140       92
    ## CRUK0068      126      159      119      132      130      132      115
    ## CRUK0069       87      120       80       93       91       93       76
    ## CRUK0070       92      125       85       98       96       98       81
    ## CRUK0071       78      111       71      115       82      115       67
    ## CRUK0072       89      155      102      159       93      159       91
    ## CRUK0073       84      101       77      121       88      121       73
    ## CRUK0074      120      153      113      126      124      126      109
    ## CRUK0075       99      132       92      136      103      136       88
    ## CRUK0076      125      158      118      131      126      131      114
    ## CRUK0077       79      112       72       85       83       85       68
    ## CRUK0078       84      117       77      121       88      121       73
    ## CRUK0079      118      151      109      124      122      124      107
    ## CRUK0080       44      110       57      114       48      114       46
    ## CRUK0081       75       84       68      112       79      112       64
    ## CRUK0082      129      162      122      135      133      135      118
    ## CRUK0083      101      134       94      138      105      138       90
    ## CRUK0084       39       72       32       76       43       76       28
    ## CRUK0085       44       77       37       81       48       81       33
    ## CRUK0086       75      108       68       81       79       81       64
    ## CRUK0087       96      129       89      102      100      102       85
    ## CRUK0088       68      101       61       74       72       74       57
    ## CRUK0089       68      101       61      105       72      105       57
    ## CRUK0090       60       79       53       97       64       97       49
    ## CRUK0091       62       71       55       99       66       99       51
    ## CRUK0092       70      103       63      107       74      107       59
    ## CRUK0093       74       85       69      113       80      113       65
    ## CRUK0094       41       74       34       78       45       78       30
    ## CRUK0095       50       83       43       87       54       87       39
    ## CRUK0096       59       72       52       76       63       76       48
    ## CRUK0097       71      104       64       77       75       77       60
    ## CRUK0098       75      108       68       81       79       81       64
    ## CRUK0099       86      119       71       92       90       92       75
    ## CRUK0100       78       87       63      115       82      115       67
    ##          CRUK0029 CRUK0030 CRUK0031 CRUK0032 CRUK0033 CRUK0034 CRUK0035
    ## CRUK0001       89      130       96       66       66       79       87
    ## CRUK0002       53       95       57       27       27       40       48
    ## CRUK0003       96      138       86       70       70       83       91
    ## CRUK0004       79      121       83       53       53       66       74
    ## CRUK0005       60      102       95       65       65       78       55
    ## CRUK0006       65      107       88       70       58       83       60
    ## CRUK0007       82      124       86       56       56       69       77
    ## CRUK0008       80      119       72       51       42       67       75
    ## CRUK0009       65      107      100       70       70       83       60
    ## CRUK0010       63      105       67       37       37       50       58
    ## CRUK0011       60       82       64       34       34       27       55
    ## CRUK0012       59      101       63       33       33       46       54
    ## CRUK0013       53       95       57       27       27       40       48
    ## CRUK0014       78       83      113       83       83       76       73
    ## CRUK0015       79      121       83       53       53       66       74
    ## CRUK0016       99      141       89       73       73       86       94
    ## CRUK0017       69      111       92       74       62       87       64
    ## CRUK0018       68       90       72       42       42       35       63
    ## CRUK0019       59      101       63       33       33       46       54
    ## CRUK0020      120      125      140      125      113      118      115
    ## CRUK0021       98      140       88       72       72       85       93
    ## CRUK0022       74      116       78       48       48       61       69
    ## CRUK0023      107      120       97       81       81       74      102
    ## CRUK0024       67      109       71       41       41       54       62
    ## CRUK0025       80       85      115       85       85       78       75
    ## CRUK0026       78      120       82       52       52       65       73
    ## CRUK0027       80       85      115       85       85       76       75
    ## CRUK0028       63      105       67       37       37       50       58
    ## CRUK0029                89       82       52       52       65       42
    ## CRUK0030       89               124       91       94       87       84
    ## CRUK0031       82      124                56       44       69       77
    ## CRUK0032       52       91       56                26       37       47
    ## CRUK0033       52       94       44       26                39       47
    ## CRUK0034       65       87       69       37       39                60
    ## CRUK0035       42       84       77       47       47       60         
    ## CRUK0036       83      125       75       57       45       70       78
    ## CRUK0037       66       88       70       40       40       33       61
    ## CRUK0038       62       84       66       36       36       29       57
    ## CRUK0039       68       90       72       42       42       35       63
    ## CRUK0040       65       87       69       37       39       32       60
    ## CRUK0041       66      108       70       40       40       53       61
    ## CRUK0042       59       81       63       33       33       26       54
    ## CRUK0043       42       84       46       16       16       29       37
    ## CRUK0044       59       81       63       33       33       26       54
    ## CRUK0045       41       83       45       15       15       28       36
    ## CRUK0046       55       97       47       29       17       42       50
    ## CRUK0047       64      106       68       38       38       51       59
    ## CRUK0048       94      136       98       68       68       81       89
    ## CRUK0049      117      122      152      122      122      115      112
    ## CRUK0050       60      102       64       34       34       47       55
    ## CRUK0051      117      118      152      122      122      115      112
    ## CRUK0052      120      121      141      125      113      118      115
    ## CRUK0054       59      101       63       33       33       46       54
    ## CRUK0055       44       86       48       18       18       31       39
    ## CRUK0056       55       97       59       29       29       42       50
    ## CRUK0057       52       92       56       26       26       39       47
    ## CRUK0058       72      114       76       46       46       59       67
    ## CRUK0059       59       81       63       33       33       26       54
    ## CRUK0060       74      116       78       48       48       61       69
    ## CRUK0061       47       89       51       21       21       34       42
    ## CRUK0062       88      134      127       97       97      110       85
    ## CRUK0063      126      164      113      100      100      113      121
    ## CRUK0064       47       89       82       52       52       65       42
    ## CRUK0065       91      133      126       96       96      109       86
    ## CRUK0066       88      130       78       62       62       75       83
    ## CRUK0067      107      149       97       81       81       94      102
    ## CRUK0068       99      141      134      104      104      117       94
    ## CRUK0069       60      102       86       65       65       78       55
    ## CRUK0070       65      107      100       70       70       83       60
    ## CRUK0071       82      124       86       56       56       69       77
    ## CRUK0072      126      168      130      100      100      113      121
    ## CRUK0073       88      130       69       62       62       75       83
    ## CRUK0074       89      135      128       98       98      111       88
    ## CRUK0075      100      145       98       77       77       90       98
    ## CRUK0076       98      140      124      103      103      116       93
    ## CRUK0077       52       94       75       57       45       70       47
    ## CRUK0078       88      130       83       62       62       75       83
    ## CRUK0079       91      133      117       96       96      109       86
    ## CRUK0080       77      123       85       55       55       68       76
    ## CRUK0081       79      121       69       53       53       66       74
    ## CRUK0082      102      144      128      107      107      120       97
    ## CRUK0083      105      143      100       79       79       92      100
    ## CRUK0084       43       85       47       17       17       30       38
    ## CRUK0085       48       90       52       22       22       35       43
    ## CRUK0086       48       90       83       53       53       66       43
    ## CRUK0087       69      111      104       74       74       87       64
    ## CRUK0088       41       83       76       46       46       59       36
    ## CRUK0089       72      114       64       46       34       59       67
    ## CRUK0090       64      106       54       38       38       51       59
    ## CRUK0091       66      108       56       40       40       53       61
    ## CRUK0092       74      116       78       48       48       61       69
    ## CRUK0093       80      122       70       54       54       67       75
    ## CRUK0094       45       87       49       19       19       32       40
    ## CRUK0095       54       92       58       28       28       41       49
    ## CRUK0096       63       85       67       37       37       30       58
    ## CRUK0097       44       86       79       49       49       62       39
    ## CRUK0098       48       90       83       53       53       66       43
    ## CRUK0099       59      101       82       64       52       77       54
    ## CRUK0100       82      124       72       56       56       69       77
    ##          CRUK0036 CRUK0037 CRUK0038 CRUK0039 CRUK0040 CRUK0041 CRUK0042
    ## CRUK0001       97       80       76       82       79       60       73
    ## CRUK0002       55       41       37       43       40       41       34
    ## CRUK0003       81       84       80       86       83       64       77
    ## CRUK0004       84       67       63       69       66       47       60
    ## CRUK0005       96       79       75       77       78       72       72
    ## CRUK0006       89       84       80       86       83       84       77
    ## CRUK0007       67       70       66       72       69       50       63
    ## CRUK0008       73       68       64       70       67       68       61
    ## CRUK0009       99       84       80       86       83       77       77
    ## CRUK0010       68       51       47       53       50       31       44
    ## CRUK0011       65       28       24       30       27       48       21
    ## CRUK0012       64       47       43       49       46       27       40
    ## CRUK0013       58       41       37       43       40       41       34
    ## CRUK0014      114       77       73       79       76       97       70
    ## CRUK0015       84       67       63       69       66       47       60
    ## CRUK0016      104       87       83       89       86       87       80
    ## CRUK0017       93       88       84       90       87       88       81
    ## CRUK0018       73       36       32       34       35       56       29
    ## CRUK0019       64       47       43       49       46       27       40
    ## CRUK0020      141      119      115      121      116      139      112
    ## CRUK0021      103       86       82       88       85       66       79
    ## CRUK0022       79       62       58       64       61       42       55
    ## CRUK0023      112       75       68       77       74       95       68
    ## CRUK0024       72       55       51       57       54       55       48
    ## CRUK0025      116       79       75       81       78       99       72
    ## CRUK0026       83       66       62       68       65       46       59
    ## CRUK0027      116       79       75       81       78       99       72
    ## CRUK0028       68       51       47       53       50       31       44
    ## CRUK0029       83       66       62       68       65       66       59
    ## CRUK0030      125       88       84       90       87      108       81
    ## CRUK0031       75       70       66       72       69       70       63
    ## CRUK0032       57       40       36       42       37       40       33
    ## CRUK0033       45       40       36       42       39       40       33
    ## CRUK0034       70       33       29       35       32       53       26
    ## CRUK0035       78       61       57       63       60       61       54
    ## CRUK0036                71       67       73       70       71       64
    ## CRUK0037       71                30       36       33       54       27
    ## CRUK0038       67       30                32       29       50       23
    ## CRUK0039       73       36       32                35       56       29
    ## CRUK0040       70       33       29       35                53       26
    ## CRUK0041       71       54       50       56       53                47
    ## CRUK0042       64       27       23       29       26       47         
    ## CRUK0043       47       30       26       32       29       30       23
    ## CRUK0044       64       27       23       29       26       47       20
    ## CRUK0045       46       29       25       31       28       29       22
    ## CRUK0046       48       43       39       45       42       43       36
    ## CRUK0047       69       52       48       54       51       52       45
    ## CRUK0048       99       82       78       84       81       58       75
    ## CRUK0049      153      116      112      118      115      116      109
    ## CRUK0050       65       48       44       50       47       48       41
    ## CRUK0051      153      116      112      118      115      116      109
    ## CRUK0052      141      119      112      121      118      139      112
    ## CRUK0054       64       47       43       49       46       27       40
    ## CRUK0055       49       32       28       34       31       32       25
    ## CRUK0056       60       39       39       45       42       43       36
    ## CRUK0057       54       40       36       42       39       40       33
    ## CRUK0058       77       60       56       62       59       40       53
    ## CRUK0059       64       27       23       29       26       47       20
    ## CRUK0060       79       59       58       59       61       62       55
    ## CRUK0061       52       35       31       37       34       35       28
    ## CRUK0062      108      111      107      113      110      111      104
    ## CRUK0063      108      114      110      116      113      114      107
    ## CRUK0064       83       66       62       68       65       66       59
    ## CRUK0065      107      110      106      112      109      110      103
    ## CRUK0066       93       76       72       78       75       76       69
    ## CRUK0067       92       95       91       97       94       95       88
    ## CRUK0068      112      118      114      120      117      118      111
    ## CRUK0069       96       79       75       81       78       79       72
    ## CRUK0070      101       84       80       86       83       84       77
    ## CRUK0071       67       70       66       68       69       70       63
    ## CRUK0072      111      114      110      116      113       94      107
    ## CRUK0073       93       76       72       78       75       76       69
    ## CRUK0074      109      112      108      114      111      112      105
    ## CRUK0075       88       91       87       93       90       91       84
    ## CRUK0076      114      117      113      119      116      117      110
    ## CRUK0077       76       71       67       73       70       71       64
    ## CRUK0078       73       76       72       78       75       76       69
    ## CRUK0079      107      110      106      112      109      110      103
    ## CRUK0080       86       69       65       71       68       49       62
    ## CRUK0081       84       67       63       69       66       67       60
    ## CRUK0082      118      121      117      123      120      121      114
    ## CRUK0083       90       93       89       95       92       93       86
    ## CRUK0084       48       27       27       33       30       31       24
    ## CRUK0085       53       32       32       38       35       36       29
    ## CRUK0086       84       67       63       69       66       67       60
    ## CRUK0087       85       88       84       90       87       88       81
    ## CRUK0088       77       60       56       62       59       60       53
    ## CRUK0089       45       60       56       62       59       60       53
    ## CRUK0090       69       49       48       54       51       52       45
    ## CRUK0091       71       54       50       56       53       54       47
    ## CRUK0092       59       62       58       64       61       62       55
    ## CRUK0093       85       68       64       70       65       68       61
    ## CRUK0094       50       33       29       35       32       33       26
    ## CRUK0095       59       42       38       44       41       42       35
    ## CRUK0096       68       31       27       33       30       51       24
    ## CRUK0097       80       63       59       65       62       63       56
    ## CRUK0098       84       67       63       69       66       67       60
    ## CRUK0099       83       78       74       80       77       78       71
    ## CRUK0100       87       70       66       69       69       70       63
    ##          CRUK0043 CRUK0044 CRUK0045 CRUK0046 CRUK0047 CRUK0048 CRUK0049
    ## CRUK0001       56       73       55       69       78       72      129
    ## CRUK0002       14       34       16       30       39       69      123
    ## CRUK0003       60       77       59       73       82       92      146
    ## CRUK0004       43       60       42       56       65       62      116
    ## CRUK0005       55       72       54       68       77      103      130
    ## CRUK0006       60       77       59       61       82      112      135
    ## CRUK0007       46       63       45       59       68       78      132
    ## CRUK0008       44       61       43       45       50       86      150
    ## CRUK0009       57       77       59       73       82      105      135
    ## CRUK0010       27       44       26       40       49       59      113
    ## CRUK0011       24       21       23       37       46       76      110
    ## CRUK0012       23       40       22       36       45       55      109
    ## CRUK0013       17       34       16       30       28       69      123
    ## CRUK0014       73       70       72       86       95      125      111
    ## CRUK0015       43       60       40       56       65       62      113
    ## CRUK0016       63       80       62       76       85      115      169
    ## CRUK0017       64       81       63       65       78      108      139
    ## CRUK0018       32       29       31       45       54       84      118
    ## CRUK0019       23       40       22       36       45       55      109
    ## CRUK0020      115      112      114      116      137      167      148
    ## CRUK0021       62       79       61       75       84       81      135
    ## CRUK0022       38       55       37       51       60       57      111
    ## CRUK0023       71       68       70       84       93      123      148
    ## CRUK0024       31       48       30       44       45       70      124
    ## CRUK0025       75       72       74       88       97      127      113
    ## CRUK0026       42       59       41       55       64       61      112
    ## CRUK0027       75       72       74       88       97      127      113
    ## CRUK0028       27       44       26       36       45       55      113
    ## CRUK0029       42       59       41       55       64       94      117
    ## CRUK0030       84       81       83       97      106      136      122
    ## CRUK0031       46       63       45       47       68       98      152
    ## CRUK0032       16       33       15       29       38       68      122
    ## CRUK0033       16       33       15       17       38       68      122
    ## CRUK0034       29       26       28       42       51       81      115
    ## CRUK0035       37       54       36       50       59       89      112
    ## CRUK0036       47       64       46       48       69       99      153
    ## CRUK0037       30       27       29       43       52       82      116
    ## CRUK0038       26       23       25       39       48       78      112
    ## CRUK0039       32       29       31       45       54       84      118
    ## CRUK0040       29       26       28       42       51       81      115
    ## CRUK0041       30       47       29       43       52       58      116
    ## CRUK0042       23       20       22       36       45       75      109
    ## CRUK0043                23        5       19       28       58      112
    ## CRUK0044       23                22       36       45       75      109
    ## CRUK0045        5       22                18       27       57      111
    ## CRUK0046       19       36       18                37       67      125
    ## CRUK0047       28       45       27       37                68      134
    ## CRUK0048       58       75       57       67       68               131
    ## CRUK0049      112      109      111      125      134      131         
    ## CRUK0050       24       41       23       37       25       68      130
    ## CRUK0051      112      109      111      125      134      131      117
    ## CRUK0052      115      112      114      116      137      167      153
    ## CRUK0054       23       40       22       36       45       55      109
    ## CRUK0055        8       25        7       21       30       60      114
    ## CRUK0056       19       36       18       32       41       71      125
    ## CRUK0057       16       33       15       29       38       68      122
    ## CRUK0058       36       53       35       49       58       55      109
    ## CRUK0059       23       20       22       36       45       75      109
    ## CRUK0060       38       55       37       51       60       90      139
    ## CRUK0061       11       28       10       24       25       63      117
    ## CRUK0062       87      104       86      100      109      139      162
    ## CRUK0063       90      107       89      103      112      142      196
    ## CRUK0064       42       59       41       55       64       94      117
    ## CRUK0065       86      103       85       99      108      138      161
    ## CRUK0066       52       69       51       65       74      104      158
    ## CRUK0067       71       88       70       84       93      123      177
    ## CRUK0068       94      111       93      107      116      146      169
    ## CRUK0069       55       72       54       68       77      107      130
    ## CRUK0070       60       77       59       73       82      112      135
    ## CRUK0071       46       63       45       59       68       98      152
    ## CRUK0072       90      107       89      103      104      101      163
    ## CRUK0073       52       69       51       65       66       96      158
    ## CRUK0074       88      105       87      101      110      140      163
    ## CRUK0075       67       84       66       80       89      119      173
    ## CRUK0076       93      110       92      106      115      145      168
    ## CRUK0077       47       64       46       48       69       99      122
    ## CRUK0078       52       69       51       65       74      104      158
    ## CRUK0079       86      103       85       99      108      138      161
    ## CRUK0080       45       62       44       58       67       64      118
    ## CRUK0081       43       60       42       56       65       95      149
    ## CRUK0082       97      114       96      110      119      149      172
    ## CRUK0083       69       86       68       82       83      113      175
    ## CRUK0084        7       24        6       20       29       59      113
    ## CRUK0085       12       29       11       25       34       64      118
    ## CRUK0086       43       60       42       56       65       95      118
    ## CRUK0087       64       81       63       77       86      116      139
    ## CRUK0088       36       53       35       49       58       88      111
    ## CRUK0089       36       53       35       37       58       88      142
    ## CRUK0090       28       45       27       41       50       80      129
    ## CRUK0091       30       47       29       43       52       82      136
    ## CRUK0092       38       55       37       51       60       90      144
    ## CRUK0093       44       61       43       57       66       96      145
    ## CRUK0094        9       26        8       22       31       61      115
    ## CRUK0095       18       35       17       31       40       70      124
    ## CRUK0096       27       24       26       40       49       79      113
    ## CRUK0097       39       56       38       52       61       91      114
    ## CRUK0098       43       60       42       56       65       95      118
    ## CRUK0099       54       71       53       55       68      106      129
    ## CRUK0100       46       63       45       59       60       98      152
    ##          CRUK0050 CRUK0051 CRUK0052 CRUK0054 CRUK0055 CRUK0056 CRUK0057
    ## CRUK0001       74      129      159       53       58       69       66
    ## CRUK0002       35      123      126       34       19       30       24
    ## CRUK0003       78      146      169       57       62       73       70
    ## CRUK0004       61      116      152       40       45       56       53
    ## CRUK0005       73      130      133       72       57       68       65
    ## CRUK0006       78      135      126       77       62       73       70
    ## CRUK0007       64      132      152       43       48       59       56
    ## CRUK0008       46      150      141       61       46       57       54
    ## CRUK0009       78      135      138       77       62       73       70
    ## CRUK0010       45      113      136       24       29       40       34
    ## CRUK0011       42      110      113       41       26       37       34
    ## CRUK0012       41      109      132       20       25       36       33
    ## CRUK0013       24      123      126       34       19       30       27
    ## CRUK0014       91      111      114       90       75       86       83
    ## CRUK0015       61      116      152       40       45       56       53
    ## CRUK0016       81      169      172       80       65       76       71
    ## CRUK0017       74      139      130       81       66       77       74
    ## CRUK0018       50      118      117       49       34       45       42
    ## CRUK0019       41      109      132       20       25       36       33
    ## CRUK0020      133      153      137      132      117      128      125
    ## CRUK0021       80      135      171       59       64       75       72
    ## CRUK0022       56      111      147       35       40       51       48
    ## CRUK0023       89      148      148       88       73       84       81
    ## CRUK0024       41      124      140       48       33       44       41
    ## CRUK0025       93      113      112       92       77       88       85
    ## CRUK0026       60      115      151       39       44       55       52
    ## CRUK0027       93      113      116       92       77       88       85
    ## CRUK0028       45      113      136       24       29       40       37
    ## CRUK0029       60      117      120       59       44       55       52
    ## CRUK0030      102      118      121      101       86       97       92
    ## CRUK0031       64      152      141       63       48       59       56
    ## CRUK0032       34      122      125       33       18       29       26
    ## CRUK0033       34      122      113       33       18       29       26
    ## CRUK0034       47      115      118       46       31       42       39
    ## CRUK0035       55      112      115       54       39       50       47
    ## CRUK0036       65      153      141       64       49       60       54
    ## CRUK0037       48      116      119       47       32       39       40
    ## CRUK0038       44      112      112       43       28       39       36
    ## CRUK0039       50      118      121       49       34       45       42
    ## CRUK0040       47      115      118       46       31       42       39
    ## CRUK0041       48      116      139       27       32       43       40
    ## CRUK0042       41      109      112       40       25       36       33
    ## CRUK0043       24      112      115       23        8       19       16
    ## CRUK0044       41      109      112       40       25       36       33
    ## CRUK0045       23      111      114       22        7       18       15
    ## CRUK0046       37      125      116       36       21       32       29
    ## CRUK0047       25      134      137       45       30       41       38
    ## CRUK0048       68      131      167       55       60       71       68
    ## CRUK0049      130      117      153      109      114      125      122
    ## CRUK0050               130      133       41       26       37       34
    ## CRUK0051      130               153      109      114      125      122
    ## CRUK0052      133      153               132      117      128      125
    ## CRUK0054       41      109      132                25       36       33
    ## CRUK0055       26      114      117       25                21       18
    ## CRUK0056       37      125      128       36       21                29
    ## CRUK0057       34      122      125       33       18       29         
    ## CRUK0058       54      109      145       33       38       49       46
    ## CRUK0059       41      109      112       40       25       36       33
    ## CRUK0060       56      144      144       55       40       45       48
    ## CRUK0061       21      117      120       28       13       24       21
    ## CRUK0062      105      162      162      104       89      100       97
    ## CRUK0063      108      190      199      107       92      103      100
    ## CRUK0064       60      117      120       59       44       55       52
    ## CRUK0065      104      161      164      103       88       99       96
    ## CRUK0066       70      158      161       69       54       65       62
    ## CRUK0067       89      177      180       88       73       84       81
    ## CRUK0068      112      169      172      111       96      107      104
    ## CRUK0069       73      130      133       72       57       68       65
    ## CRUK0070       78      135      138       77       62       73       70
    ## CRUK0071       64      152      155       63       48       59       56
    ## CRUK0072      100      163      199       87       92      103      100
    ## CRUK0073       62      158      158       69       54       65       62
    ## CRUK0074      106      163      166      105       90      101       98
    ## CRUK0075       85      173      176       84       69       69       77
    ## CRUK0076      111      168      171      110       95      106      103
    ## CRUK0077       65      122      113       64       49       60       57
    ## CRUK0078       70      158      161       69       54       65       62
    ## CRUK0079      104      161      164      103       88       99       96
    ## CRUK0080       63      118      154       42       47       58       55
    ## CRUK0081       61      149      152       60       45       56       53
    ## CRUK0082      115      172      175      114       99      110      107
    ## CRUK0083       79      171      178       86       71       71       79
    ## CRUK0084       25      113      116       24        9       16       17
    ## CRUK0085       30      118      121       29       12       21       22
    ## CRUK0086       61      118      121       60       45       56       53
    ## CRUK0087       82      139      142       81       66       77       74
    ## CRUK0088       54      111      114       53       38       49       46
    ## CRUK0089       54      142      133       53       38       49       46
    ## CRUK0090       46      134      137       45       30       41       38
    ## CRUK0091       48      136      139       47       32       43       37
    ## CRUK0092       56      144      147       55       40       40       48
    ## CRUK0093       62      150      153       61       46       57       54
    ## CRUK0094       27      115      118       26       11       22       13
    ## CRUK0095       36      124      123       35       20       20       28
    ## CRUK0096       45      113      113       44       29       40       37
    ## CRUK0097       57      114      117       56       41       52       49
    ## CRUK0098       61      118      118       60       45       56       53
    ## CRUK0099       64      129      120       71       56       67       64
    ## CRUK0100       56      152      155       63       48       59       56
    ##          CRUK0058 CRUK0059 CRUK0060 CRUK0061 CRUK0062 CRUK0063 CRUK0064
    ## CRUK0001       53       73       88       61      137      140       92
    ## CRUK0002       47       34       49       22       98       97       53
    ## CRUK0003       70       77       92       65      121      110       96
    ## CRUK0004       40       60       75       48      124      127       79
    ## CRUK0005       85       72       87       60      105      133       60
    ## CRUK0006       90       77       92       65      110      138       65
    ## CRUK0007       56       63       78       51      107      110       82
    ## CRUK0008       74       61       76       41      125      128       80
    ## CRUK0009       90       77       90       65      110      144       65
    ## CRUK0010       37       44       59       32      108      111       63
    ## CRUK0011       54       21       56       29      105      108       60
    ## CRUK0012       33       40       55       28      104      107       59
    ## CRUK0013       47       34       49       14       98      101       53
    ## CRUK0014      103       70      105       78      123      157       78
    ## CRUK0015       40       60       75       48      124      127       79
    ## CRUK0016       93       80       95       68      144      117       92
    ## CRUK0017       94       81       96       69      114      148       69
    ## CRUK0018       62       29       64       37      113      116       68
    ## CRUK0019       33       40       55       28      104      107       59
    ## CRUK0020      145      112      142      120      165      196      120
    ## CRUK0021       59       79       94       67      143      122       98
    ## CRUK0022       35       55       70       43      119      122       74
    ## CRUK0023      101       68      103       76      152      131      107
    ## CRUK0024       48       48       63       28      112      115       67
    ## CRUK0025      105       72      107       80      125      159       80
    ## CRUK0026       39       59       71       47      123      126       78
    ## CRUK0027      105       72      107       80      125      159       80
    ## CRUK0028       37       44       59       32      108      111       63
    ## CRUK0029       72       59       74       47       88      126       47
    ## CRUK0030      114       81      116       89      134      164       89
    ## CRUK0031       76       63       78       51      127      113       82
    ## CRUK0032       46       33       48       21       97      100       52
    ## CRUK0033       46       33       48       21       97      100       52
    ## CRUK0034       59       26       61       34      110      113       65
    ## CRUK0035       67       54       69       42       85      121       42
    ## CRUK0036       77       64       79       52      108      108       83
    ## CRUK0037       60       27       59       35      111      114       66
    ## CRUK0038       56       23       58       31      107      110       62
    ## CRUK0039       62       29       59       37      113      116       68
    ## CRUK0040       59       26       61       34      110      113       65
    ## CRUK0041       40       47       62       35      111      114       66
    ## CRUK0042       53       20       55       28      104      107       59
    ## CRUK0043       36       23       38       11       87       90       42
    ## CRUK0044       53       20       55       28      104      107       59
    ## CRUK0045       35       22       37       10       86       89       41
    ## CRUK0046       49       36       51       24      100      103       55
    ## CRUK0047       58       45       60       25      109      112       64
    ## CRUK0048       55       75       90       63      139      142       94
    ## CRUK0049      109      109      139      117      162      196      117
    ## CRUK0050       54       41       56       21      105      108       60
    ## CRUK0051      109      109      144      117      162      190      117
    ## CRUK0052      145      112      144      120      162      199      120
    ## CRUK0054       33       40       55       28      104      107       59
    ## CRUK0055       38       25       40       13       89       92       44
    ## CRUK0056       49       36       45       24      100      103       55
    ## CRUK0057       46       33       48       21       97      100       52
    ## CRUK0058                53       68       41      117      120       72
    ## CRUK0059       53                55       28      104      107       59
    ## CRUK0060       68       55                43      119      120       74
    ## CRUK0061       41       28       43                92       95       47
    ## CRUK0062      117      104      119       92               137       92
    ## CRUK0063      120      107      120       95      137               126
    ## CRUK0064       72       59       74       47       92      126         
    ## CRUK0065      116      103      118       91      102      136       91
    ## CRUK0066       82       69       82       57      133      106       88
    ## CRUK0067      101       88      103       76      118       97      107
    ## CRUK0068      124      111      126       99      110      133       99
    ## CRUK0069       85       72       87       60      105      139       53
    ## CRUK0070       90       77       92       65       96      130       65
    ## CRUK0071       76       63       78       51       89       96       82
    ## CRUK0072       87      107      122       95      137      140      126
    ## CRUK0073       82       69       81       57      133      122       88
    ## CRUK0074      118      105      120       93       98      138       93
    ## CRUK0075       97       84       93       72      128      131       96
    ## CRUK0076      123      110      120       98      109      143       98
    ## CRUK0077       77       64       79       52       97      131       52
    ## CRUK0078       82       69       84       57       99      102       88
    ## CRUK0079      116      103      118       91      102      136       84
    ## CRUK0080       42       62       77       50      122      129       81
    ## CRUK0081       73       60       75       48      124      103       72
    ## CRUK0082      127      114      129      102      113      147      102
    ## CRUK0083       99       86       95       74      116      115      105
    ## CRUK0084       37       24       39       12       88       91       43
    ## CRUK0085       42       29       44       17       93       96       48
    ## CRUK0086       73       60       73       48       93      127       41
    ## CRUK0087       94       81       96       69       94      128       69
    ## CRUK0088       66       53       68       41       86      120       41
    ## CRUK0089       66       53       68       41       97      100       72
    ## CRUK0090       58       45       52       33      109       98       64
    ## CRUK0091       60       47       62       35      111       90       66
    ## CRUK0092       68       55       64       43       99      102       74
    ## CRUK0093       74       61       71       49      125      104       80
    ## CRUK0094       39       26       41       14       90       93       45
    ## CRUK0095       48       35       44       23       99      102       54
    ## CRUK0096       57       24       59       32      108      111       63
    ## CRUK0097       69       56       71       44       89      123       44
    ## CRUK0098       73       60       75       48       90      127       48
    ## CRUK0099       84       71       86       51      104      138       59
    ## CRUK0100       76       63       75       43      127      106       82
    ##          CRUK0065 CRUK0066 CRUK0067 CRUK0068 CRUK0069 CRUK0070 CRUK0071
    ## CRUK0001      136       96      121      144      105      110       96
    ## CRUK0002       97       63       82      105       66       71       57
    ## CRUK0003      120       92       91      128      109      114       80
    ## CRUK0004      123       84      103      131       92       97       83
    ## CRUK0005      104       95      120      106       73       78       91
    ## CRUK0006      109      100      125      111       78       83      100
    ## CRUK0007      106       92       91      114       95      100       66
    ## CRUK0008      124       90      109      132       93       98       84
    ## CRUK0009      104      106      125      117       78       83      100
    ## CRUK0010      107       73       92      115       76       81       67
    ## CRUK0011      104       70       89      112       73       78       64
    ## CRUK0012      103       69       88      111       72       77       63
    ## CRUK0013       97       63       82      105       66       71       57
    ## CRUK0014      122      119      138      130       91       96      113
    ## CRUK0015      123       89      108      131       92       97       83
    ## CRUK0016      143       79      104      145      105      117      103
    ## CRUK0017      113      110      129      121       82       87      104
    ## CRUK0018      112       78       97      120       81       86       68
    ## CRUK0019      103       69       88      111       72       77       63
    ## CRUK0020      164      161      180      172      133      138      155
    ## CRUK0021      142       84      103      150      111      116      102
    ## CRUK0022      118       84      103      126       87       92       78
    ## CRUK0023      151       87      112      159      120      125      111
    ## CRUK0024      111       77       96      119       80       85       71
    ## CRUK0025      124      121      140      132       93       98      115
    ## CRUK0026      122       88      107      130       91       96       82
    ## CRUK0027      124      121      140      132       93       98      115
    ## CRUK0028      107       73       92      115       76       81       67
    ## CRUK0029       91       88      107       99       60       65       82
    ## CRUK0030      133      130      149      141      102      107      124
    ## CRUK0031      126       78       97      134       86      100       86
    ## CRUK0032       96       62       81      104       65       70       56
    ## CRUK0033       96       62       81      104       65       70       56
    ## CRUK0034      109       75       94      117       78       83       69
    ## CRUK0035       86       83      102       94       55       60       77
    ## CRUK0036      107       93       92      112       96      101       67
    ## CRUK0037      110       76       95      118       79       84       70
    ## CRUK0038      106       72       91      114       75       80       66
    ## CRUK0039      112       78       97      120       81       86       68
    ## CRUK0040      109       75       94      117       78       83       69
    ## CRUK0041      110       76       95      118       79       84       70
    ## CRUK0042      103       69       88      111       72       77       63
    ## CRUK0043       86       52       71       94       55       60       46
    ## CRUK0044      103       69       88      111       72       77       63
    ## CRUK0045       85       51       70       93       54       59       45
    ## CRUK0046       99       65       84      107       68       73       59
    ## CRUK0047      108       74       93      116       77       82       68
    ## CRUK0048      138      104      123      146      107      112       98
    ## CRUK0049      161      158      177      169      130      135      152
    ## CRUK0050      104       70       89      112       73       78       64
    ## CRUK0051      161      158      177      169      130      135      152
    ## CRUK0052      164      161      180      172      133      138      155
    ## CRUK0054      103       69       88      111       72       77       63
    ## CRUK0055       88       54       73       96       57       62       48
    ## CRUK0056       99       65       84      107       68       73       59
    ## CRUK0057       96       62       81      104       65       70       56
    ## CRUK0058      116       82      101      124       85       90       76
    ## CRUK0059      103       69       88      111       72       77       63
    ## CRUK0060      118       82      103      126       87       92       78
    ## CRUK0061       91       57       76       99       60       65       51
    ## CRUK0062      102      133      118      110      105       96       89
    ## CRUK0063      136      106       97      133      139      130       96
    ## CRUK0064       91       88      107       99       53       65       82
    ## CRUK0065               132      117      109      104       95       92
    ## CRUK0066      132                88      134       99      106       92
    ## CRUK0067      117       88               125      120      111       77
    ## CRUK0068      109      134      125               112      103      100
    ## CRUK0069      104       99      120      112                78       95
    ## CRUK0070       95      106      111      103       78                86
    ## CRUK0071       92       92       77      100       95       86         
    ## CRUK0072      124      136      121      144      139      130       96
    ## CRUK0073      132       84      103      140       92      106       92
    ## CRUK0074       89      134      119      111      106       97       94
    ## CRUK0075      127      108      103      135      100      121       87
    ## CRUK0076      108      139      124      116      102       99       99
    ## CRUK0077       96       93      112      104       65       70       87
    ## CRUK0078       98       98       83      101       92       92       58
    ## CRUK0079      101      132      117      109       88       95       92
    ## CRUK0080      125       91      110      133       94       99       85
    ## CRUK0081      123       60       79      131       85       97       83
    ## CRUK0082      112      143      128      113      106       99      103
    ## CRUK0083      115      115      100      123      109      109       75
    ## CRUK0084       87       53       72       95       56       61       47
    ## CRUK0085       92       58       77      100       61       66       52
    ## CRUK0086       92       89      108      100       54       66       83
    ## CRUK0087       84      110      109      101       82       87       84
    ## CRUK0088       85       82      101       93       54       59       76
    ## CRUK0089       96       82       81      104       85       90       56
    ## CRUK0090      108       60       79      116       77       82       68
    ## CRUK0091      110       52       71      118       79       84       70
    ## CRUK0092       98       84       83      106       87       92       58
    ## CRUK0093      124       66       85      132       93       94       84
    ## CRUK0094       89       55       74       97       58       63       49
    ## CRUK0095       98       64       83      106       67       72       58
    ## CRUK0096      107       73       92      115       76       81       67
    ## CRUK0097       88       85      104       91       57       62       79
    ## CRUK0098       92       89      108       95       61       66       83
    ## CRUK0099      103      100      119      111       72       77       94
    ## CRUK0100      126       68       87      134       95       96       86
    ##          CRUK0072 CRUK0073 CRUK0074 CRUK0075 CRUK0076 CRUK0077 CRUK0078
    ## CRUK0001      107      102      138      114      143       97      102
    ## CRUK0002      101       63       99       78      104       58       63
    ## CRUK0003      104       92      122      101      127      101       86
    ## CRUK0004       94       89      125       99      130       84       89
    ## CRUK0005      139      101      106      116      111       65      101
    ## CRUK0006      144      106      111      121      116       58      106
    ## CRUK0007       90       92      108       87      113       87       72
    ## CRUK0008      120       82      126      105      131       73       90
    ## CRUK0009      139      106      106      121      116       70      106
    ## CRUK0010       91       73      109       88      114       68       73
    ## CRUK0011      108       70      106       85      111       65       70
    ## CRUK0012       87       69      105       84      110       64       69
    ## CRUK0013      101       63       99       78      104       58       63
    ## CRUK0014      157      119      124      134      129       83      119
    ## CRUK0015       94       89      125      104      130       84       89
    ## CRUK0016      147       95      145      117      150      104      109
    ## CRUK0017      140      102      115      125      118       62      110
    ## CRUK0018      116       78      114       93      119       73       78
    ## CRUK0019       87       69      105       84      110       64       69
    ## CRUK0020      199      161      166      176      171      113      161
    ## CRUK0021      113       94      144      123      149      103      108
    ## CRUK0022       89       84      120       99      125       79       84
    ## CRUK0023      155      101      153      132      158      112      117
    ## CRUK0024      102       77      113       92      118       72       77
    ## CRUK0025      159      121      126      136      131       85      121
    ## CRUK0026       93       88      124      103      126       83       88
    ## CRUK0027      159      121      126      136      131       85      121
    ## CRUK0028       91       73      109       88      114       68       73
    ## CRUK0029      126       88       89      100       98       52       88
    ## CRUK0030      168      130      135      145      140       94      130
    ## CRUK0031      130       69      128       98      124       75       83
    ## CRUK0032      100       62       98       77      103       57       62
    ## CRUK0033      100       62       98       77      103       45       62
    ## CRUK0034      113       75      111       90      116       70       75
    ## CRUK0035      121       83       88       98       93       47       83
    ## CRUK0036      111       93      109       88      114       76       73
    ## CRUK0037      114       76      112       91      117       71       76
    ## CRUK0038      110       72      108       87      113       67       72
    ## CRUK0039      116       78      114       93      119       73       78
    ## CRUK0040      113       75      111       90      116       70       75
    ## CRUK0041       94       76      112       91      117       71       76
    ## CRUK0042      107       69      105       84      110       64       69
    ## CRUK0043       90       52       88       67       93       47       52
    ## CRUK0044      107       69      105       84      110       64       69
    ## CRUK0045       89       51       87       66       92       46       51
    ## CRUK0046      103       65      101       80      106       48       65
    ## CRUK0047      104       66      110       89      115       69       74
    ## CRUK0048      101       96      140      119      145       99      104
    ## CRUK0049      163      158      163      173      168      122      158
    ## CRUK0050      100       62      106       85      111       65       70
    ## CRUK0051      163      158      163      173      168      122      158
    ## CRUK0052      199      158      166      176      171      113      161
    ## CRUK0054       87       69      105       84      110       64       69
    ## CRUK0055       92       54       90       69       95       49       54
    ## CRUK0056      103       65      101       69      106       60       65
    ## CRUK0057      100       62       98       77      103       57       62
    ## CRUK0058       87       82      118       97      123       77       82
    ## CRUK0059      107       69      105       84      110       64       69
    ## CRUK0060      122       81      120       93      120       79       84
    ## CRUK0061       95       57       93       72       98       52       57
    ## CRUK0062      137      133       98      128      109       97       99
    ## CRUK0063      140      122      138      131      143      131      102
    ## CRUK0064      126       88       93       96       98       52       88
    ## CRUK0065      124      132       89      127      108       96       98
    ## CRUK0066      136       84      134      108      139       93       98
    ## CRUK0067      121      103      119      103      124      112       83
    ## CRUK0068      144      140      111      135      116      104      101
    ## CRUK0069      139       92      106      100      102       65       92
    ## CRUK0070      130      106       97      121       99       70       92
    ## CRUK0071       96       92       94       87       99       87       58
    ## CRUK0072               128      126      131      143      131      102
    ## CRUK0073      128               134      100      130       93       89
    ## CRUK0074      126      134               129      110       98      100
    ## CRUK0075      131      100      129               125      108       84
    ## CRUK0076      143      130      110      125               103       96
    ## CRUK0077      131       93       98      108      103                93
    ## CRUK0078      102       89      100       84       96       93         
    ## CRUK0079      136      123      103      111       99       96       89
    ## CRUK0080       96       91      123      106      132       86       91
    ## CRUK0081      127       75      125       92      130       84       89
    ## CRUK0082      147      134      114      129      103      107       95
    ## CRUK0083      111       98      117       90      113      110       72
    ## CRUK0084       91       53       89       68       94       48       53
    ## CRUK0085       96       58       94       73       99       53       58
    ## CRUK0086      127       89       94       97       99       53       89
    ## CRUK0087      119      110       86      105      100       74       90
    ## CRUK0088      120       82       87       97       92       46       82
    ## CRUK0089      100       82       98       77      103       65       62
    ## CRUK0090      112       60      110       89      115       69       74
    ## CRUK0091      114       62      112       91      117       71       76
    ## CRUK0092      102       84      100       68      105       79       64
    ## CRUK0093      128       74      126      105      131       85       90
    ## CRUK0094       93       55       91       70       96       50       55
    ## CRUK0095      102       64      100       68      105       59       64
    ## CRUK0096      111       73      109       88      114       68       73
    ## CRUK0097      123       85       90      100       95       49       80
    ## CRUK0098      127       89       94      104       99       53       84
    ## CRUK0099      138      100      105      115      110       52      100
    ## CRUK0100      130       78      128      107      133       87       92
    ##          CRUK0079 CRUK0080 CRUK0081 CRUK0082 CRUK0083 CRUK0084 CRUK0085
    ## CRUK0001      136       62       93      147      119       57       62
    ## CRUK0002       97       56       54      108       80       18       23
    ## CRUK0003      120       79       83      131      103       61       66
    ## CRUK0004      123       49       75      134      106       44       49
    ## CRUK0005      104       94       92      115      118       56       61
    ## CRUK0006      109       99       97      120      123       61       66
    ## CRUK0007      106       65       83      117       89       47       52
    ## CRUK0008      124       83       81      135       99       45       50
    ## CRUK0009      109       99       97      120      123       61       66
    ## CRUK0010      107       46       64      118       90       28       33
    ## CRUK0011      104       63       61      115       87       25       30
    ## CRUK0012      103       42       60      114       86       24       29
    ## CRUK0013       97       56       54      108       80       18       23
    ## CRUK0014      122      112      110      133      136       74       79
    ## CRUK0015      123       49       80      134      106       44       49
    ## CRUK0016      136      102       69      154      126       64       69
    ## CRUK0017      113      103      101      124      119       65       70
    ## CRUK0018      112       71       69      123       95       33       38
    ## CRUK0019      103       42       60      114       86       24       29
    ## CRUK0020      164      154      152      175      178      116      121
    ## CRUK0021      142       68       75      153      125       63       66
    ## CRUK0022      118       44       75      129      101       39       44
    ## CRUK0023      151      110       84      162      134       72       77
    ## CRUK0024      109       57       68      122       94       32       37
    ## CRUK0025      124      114      112      135      138       76       81
    ## CRUK0026      122       48       79      133      105       43       48
    ## CRUK0027      124      114      112      135      138       76       81
    ## CRUK0028      107       46       64      118       90       28       33
    ## CRUK0029       91       77       79      102      105       43       48
    ## CRUK0030      133      123      121      144      143       85       90
    ## CRUK0031      117       85       69      128      100       47       52
    ## CRUK0032       96       55       53      107       79       17       22
    ## CRUK0033       96       55       53      107       79       17       22
    ## CRUK0034      109       68       66      120       92       30       35
    ## CRUK0035       86       76       74       97      100       38       43
    ## CRUK0036      107       86       84      118       90       48       53
    ## CRUK0037      110       69       67      121       93       27       32
    ## CRUK0038      106       65       63      117       89       27       32
    ## CRUK0039      112       71       69      123       95       33       38
    ## CRUK0040      109       68       66      120       92       30       35
    ## CRUK0041      110       49       67      121       93       31       36
    ## CRUK0042      103       62       60      114       86       24       29
    ## CRUK0043       86       45       43       97       69        7       12
    ## CRUK0044      103       62       60      114       86       24       29
    ## CRUK0045       85       44       42       96       68        6       11
    ## CRUK0046       99       58       56      110       82       20       25
    ## CRUK0047      108       67       65      119       83       29       34
    ## CRUK0048      138       64       95      149      113       59       64
    ## CRUK0049      161      118      149      172      175      113      118
    ## CRUK0050      104       63       61      115       79       25       30
    ## CRUK0051      161      118      149      172      171      113      118
    ## CRUK0052      164      154      152      175      178      116      121
    ## CRUK0054      103       42       60      114       86       24       29
    ## CRUK0055       88       47       45       99       71        9       12
    ## CRUK0056       99       58       56      110       71       16       21
    ## CRUK0057       96       55       53      107       79       17       22
    ## CRUK0058      116       42       73      127       99       37       42
    ## CRUK0059      103       62       60      114       86       24       29
    ## CRUK0060      118       77       75      129       95       39       44
    ## CRUK0061       91       50       48      102       74       12       17
    ## CRUK0062      102      122      124      113      116       88       93
    ## CRUK0063      136      129      103      147      115       91       96
    ## CRUK0064       84       81       72      102      105       43       48
    ## CRUK0065      101      125      123      112      115       87       92
    ## CRUK0066      132       91       60      143      115       53       58
    ## CRUK0067      117      110       79      128      100       72       77
    ## CRUK0068      109      133      131      113      123       95      100
    ## CRUK0069       88       94       85      106      109       56       61
    ## CRUK0070       95       99       97       99      109       61       66
    ## CRUK0071       92       85       83      103       75       47       52
    ## CRUK0072      136       96      127      147      111       91       96
    ## CRUK0073      123       91       75      134       98       53       58
    ## CRUK0074      103      123      125      114      117       89       94
    ## CRUK0075      111      106       92      129       90       68       73
    ## CRUK0076       99      132      130      103      113       94       99
    ## CRUK0077       96       86       84      107      110       48       53
    ## CRUK0078       89       91       89       95       72       53       58
    ## CRUK0079               125      116      103      106       87       92
    ## CRUK0080      125                82      134      108       46       51
    ## CRUK0081      116       82               134      106       44       49
    ## CRUK0082      103      134      134               117       98      103
    ## CRUK0083      106      108      106      117                70       75
    ## CRUK0084       87       46       44       98       70                 9
    ## CRUK0085       92       51       49      103       75        9         
    ## CRUK0086       85       82       73      103      106       44       49
    ## CRUK0087       93      103      101      104      107       65       70
    ## CRUK0088       85       75       73       96       99       37       42
    ## CRUK0089       96       75       73      107       79       37       42
    ## CRUK0090      108       67       51      119       91       29       34
    ## CRUK0091      110       69       43      121       93       31       36
    ## CRUK0092       98       77       75      109       70       39       44
    ## CRUK0093      124       83       57      131      107       45       50
    ## CRUK0094       89       48       46      100       72       10       15
    ## CRUK0095       98       57       55      109       70       19       24
    ## CRUK0096      107       66       64      118       90       28       33
    ## CRUK0097       88       78       76       94      102       40       45
    ## CRUK0098       92       82       80       98      106       44       49
    ## CRUK0099      103       93       91      114      117       55       60
    ## CRUK0100      126       85       59      133      109       47       52
    ##          CRUK0086 CRUK0087 CRUK0088 CRUK0089 CRUK0090 CRUK0091 CRUK0092
    ## CRUK0001       93      114       86       86       78       80       88
    ## CRUK0002       54       75       47       47       39       41       49
    ## CRUK0003       97       98       90       70       68       70       72
    ## CRUK0004       80      101       73       73       65       67       73
    ## CRUK0005       61       82       54       85       77       79       87
    ## CRUK0006       66       87       59       78       82       84       92
    ## CRUK0007       83       84       76       56       68       70       58
    ## CRUK0008       81      102       74       62       66       68       76
    ## CRUK0009       66       82       59       90       82       84       92
    ## CRUK0010       64       85       57       57       49       51       59
    ## CRUK0011       61       82       54       54       46       48       56
    ## CRUK0012       60       81       53       53       45       47       55
    ## CRUK0013       54       75       47       47       39       41       49
    ## CRUK0014       79      100       72      103       95       97      105
    ## CRUK0015       80      101       73       73       65       67       75
    ## CRUK0016       93      121       93       93       71       63       93
    ## CRUK0017       70       91       63       82       86       88       96
    ## CRUK0018       69       90       62       62       54       56       64
    ## CRUK0019       60       81       53       53       45       47       55
    ## CRUK0020      121      142      114      133      132      139      147
    ## CRUK0021       99      120       92       92       70       62       94
    ## CRUK0022       75       96       68       68       60       62       70
    ## CRUK0023      108      129      101      101       79       71      103
    ## CRUK0024       68       89       61       61       53       55       63
    ## CRUK0025       81      102       74      105       97       99      107
    ## CRUK0026       79      100       72       72       64       66       74
    ## CRUK0027       81      102       74      105       97       99      107
    ## CRUK0028       64       85       57       57       49       51       59
    ## CRUK0029       48       69       41       72       64       66       74
    ## CRUK0030       90      111       83      114      106      108      116
    ## CRUK0031       83      104       76       64       54       56       78
    ## CRUK0032       53       74       46       46       38       40       48
    ## CRUK0033       53       74       46       34       38       40       48
    ## CRUK0034       66       87       59       59       51       53       61
    ## CRUK0035       43       64       36       67       59       61       69
    ## CRUK0036       84       85       77       45       69       71       59
    ## CRUK0037       67       88       60       60       49       54       62
    ## CRUK0038       63       84       56       56       48       50       58
    ## CRUK0039       69       90       62       62       54       56       64
    ## CRUK0040       66       87       59       59       51       53       61
    ## CRUK0041       67       88       60       60       52       54       62
    ## CRUK0042       60       81       53       53       45       47       55
    ## CRUK0043       43       64       36       36       28       30       38
    ## CRUK0044       60       81       53       53       45       47       55
    ## CRUK0045       42       63       35       35       27       29       37
    ## CRUK0046       56       77       49       37       41       43       51
    ## CRUK0047       65       86       58       58       50       52       60
    ## CRUK0048       95      116       88       88       80       82       90
    ## CRUK0049      118      139      111      142      129      136      144
    ## CRUK0050       61       82       54       54       46       48       56
    ## CRUK0051      118      139      111      142      134      136      144
    ## CRUK0052      121      142      114      133      137      139      147
    ## CRUK0054       60       81       53       53       45       47       55
    ## CRUK0055       45       66       38       38       30       32       40
    ## CRUK0056       56       77       49       49       41       43       40
    ## CRUK0057       53       74       46       46       38       37       48
    ## CRUK0058       73       94       66       66       58       60       68
    ## CRUK0059       60       81       53       53       45       47       55
    ## CRUK0060       73       96       68       68       52       62       64
    ## CRUK0061       48       69       41       41       33       35       43
    ## CRUK0062       93       94       86       97      109      111       99
    ## CRUK0063      127      128      120      100       98       90      102
    ## CRUK0064       41       69       41       72       64       66       74
    ## CRUK0065       92       84       85       96      108      110       98
    ## CRUK0066       89      110       82       82       60       52       84
    ## CRUK0067      108      109      101       81       79       71       83
    ## CRUK0068      100      101       93      104      116      118      106
    ## CRUK0069       54       82       54       85       77       79       87
    ## CRUK0070       66       87       59       90       82       84       92
    ## CRUK0071       83       84       76       56       68       70       58
    ## CRUK0072      127      119      120      100      112      114      102
    ## CRUK0073       89      110       82       82       60       62       84
    ## CRUK0074       94       86       87       98      110      112      100
    ## CRUK0075       97      105       97       77       89       91       68
    ## CRUK0076       99      100       92      103      115      117      105
    ## CRUK0077       53       74       46       65       69       71       79
    ## CRUK0078       89       90       82       62       74       76       64
    ## CRUK0079       85       93       85       96      108      110       98
    ## CRUK0080       82      103       75       75       67       69       77
    ## CRUK0081       73      101       73       73       51       43       75
    ## CRUK0082      103      104       96      107      119      121      109
    ## CRUK0083      106      107       99       79       91       93       70
    ## CRUK0084       44       65       37       37       29       31       39
    ## CRUK0085       49       70       42       42       34       36       44
    ## CRUK0086                70       42       73       65       67       75
    ## CRUK0087       70                63       74       86       88       76
    ## CRUK0088       42       63                66       56       60       68
    ## CRUK0089       73       74       66                58       60       48
    ## CRUK0090       65       86       56       58                38       60
    ## CRUK0091       67       88       60       60       38                62
    ## CRUK0092       75       76       68       48       60       62         
    ## CRUK0093       81      102       74       74       47       44       76
    ## CRUK0094       46       67       39       39       31       30       41
    ## CRUK0095       55       76       48       48       40       42       39
    ## CRUK0096       64       85       57       57       49       51       59
    ## CRUK0097       45       66       38       69       61       63       71
    ## CRUK0098       49       70       42       73       65       67       75
    ## CRUK0099       60       81       53       72       76       78       86
    ## CRUK0100       83      104       76       76       54       46       78
    ##          CRUK0093 CRUK0094 CRUK0095 CRUK0096 CRUK0097 CRUK0098 CRUK0099
    ## CRUK0001       94       59       64       77       89       93      104
    ## CRUK0002       55       20       29       38       50       54       65
    ## CRUK0003       84       63       72       81       93       97      108
    ## CRUK0004       81       46       55       64       76       80       91
    ## CRUK0005       93       58       67       76       57       61       72
    ## CRUK0006       98       63       72       81       62       66       65
    ## CRUK0007       84       49       58       64       79       83       94
    ## CRUK0008       82       47       56       65       77       81       72
    ## CRUK0009       98       63       72       81       62       66       77
    ## CRUK0010       65       27       39       48       60       64       75
    ## CRUK0011       62       27       36       25       57       61       72
    ## CRUK0012       61       26       35       44       56       60       71
    ## CRUK0013       55       20       29       38       50       54       57
    ## CRUK0014      111       76       85       74       75       79       90
    ## CRUK0015       81       46       55       64       76       80       91
    ## CRUK0016       77       66       75       84       96      100      111
    ## CRUK0017      102       67       76       85       66       70       69
    ## CRUK0018       70       35       44       33       65       69       80
    ## CRUK0019       61       26       35       44       56       60       71
    ## CRUK0020      148      118      127      116      117      121      120
    ## CRUK0021       76       65       74       83       95       99      110
    ## CRUK0022       74       41       50       59       71       75       86
    ## CRUK0023       85       74       83       72      104      108      119
    ## CRUK0024       69       34       43       52       64       68       71
    ## CRUK0025      113       78       87       76       77       81       92
    ## CRUK0026       80       45       54       63       75       79       90
    ## CRUK0027      113       78       87       76       77       81       92
    ## CRUK0028       65       30       39       48       60       64       75
    ## CRUK0029       80       45       54       63       44       48       59
    ## CRUK0030      122       87       92       85       86       90      101
    ## CRUK0031       70       49       58       67       79       83       82
    ## CRUK0032       54       19       28       37       49       53       64
    ## CRUK0033       54       19       28       37       49       53       52
    ## CRUK0034       67       32       41       30       62       66       77
    ## CRUK0035       75       40       49       58       39       43       54
    ## CRUK0036       85       50       59       68       80       84       83
    ## CRUK0037       68       33       42       31       63       67       78
    ## CRUK0038       64       29       38       27       59       63       74
    ## CRUK0039       70       35       44       33       65       69       80
    ## CRUK0040       65       32       41       30       62       66       77
    ## CRUK0041       68       33       42       51       63       67       78
    ## CRUK0042       61       26       35       24       56       60       71
    ## CRUK0043       44        9       18       27       39       43       54
    ## CRUK0044       61       26       35       24       56       60       71
    ## CRUK0045       43        8       17       26       38       42       53
    ## CRUK0046       57       22       31       40       52       56       55
    ## CRUK0047       66       31       40       49       61       65       68
    ## CRUK0048       96       61       70       79       91       95      106
    ## CRUK0049      145      115      124      113      114      118      129
    ## CRUK0050       62       27       36       45       57       61       64
    ## CRUK0051      150      115      124      113      114      118      129
    ## CRUK0052      153      118      123      113      117      118      120
    ## CRUK0054       61       26       35       44       56       60       71
    ## CRUK0055       46       11       20       29       41       45       56
    ## CRUK0056       57       22       20       40       52       56       67
    ## CRUK0057       54       13       28       37       49       53       64
    ## CRUK0058       74       39       48       57       69       73       84
    ## CRUK0059       61       26       35       24       56       60       71
    ## CRUK0060       71       41       44       59       71       75       86
    ## CRUK0061       49       14       23       32       44       48       51
    ## CRUK0062      125       90       99      108       89       90      104
    ## CRUK0063      104       93      102      111      123      127      138
    ## CRUK0064       80       45       54       63       44       48       59
    ## CRUK0065      124       89       98      107       88       92      103
    ## CRUK0066       66       55       64       73       85       89      100
    ## CRUK0067       85       74       83       92      104      108      119
    ## CRUK0068      132       97      106      115       91       95      111
    ## CRUK0069       93       58       67       76       57       61       72
    ## CRUK0070       94       63       72       81       62       66       77
    ## CRUK0071       84       49       58       67       79       83       94
    ## CRUK0072      128       93      102      111      123      127      138
    ## CRUK0073       74       55       64       73       85       89      100
    ## CRUK0074      126       91      100      109       90       94      105
    ## CRUK0075      105       70       68       88      100      104      115
    ## CRUK0076      131       96      105      114       95       99      110
    ## CRUK0077       85       50       59       68       49       53       52
    ## CRUK0078       90       55       64       73       80       84      100
    ## CRUK0079      124       89       98      107       88       92      103
    ## CRUK0080       83       48       57       66       78       82       93
    ## CRUK0081       57       46       55       64       76       80       91
    ## CRUK0082      131      100      109      118       94       98      114
    ## CRUK0083      107       72       70       90      102      106      117
    ## CRUK0084       45       10       19       28       40       44       55
    ## CRUK0085       50       15       24       33       45       49       60
    ## CRUK0086       81       46       55       64       45       49       60
    ## CRUK0087      102       67       76       85       66       70       81
    ## CRUK0088       74       39       48       57       38       42       53
    ## CRUK0089       74       39       48       57       69       73       72
    ## CRUK0090       47       31       40       49       61       65       76
    ## CRUK0091       44       30       42       51       63       67       78
    ## CRUK0092       76       41       39       59       71       75       86
    ## CRUK0093                47       56       65       77       81       92
    ## CRUK0094       47                21       30       42       46       57
    ## CRUK0095       56       21                39       51       55       66
    ## CRUK0096       65       30       39                60       64       75
    ## CRUK0097       77       42       51       60                40       56
    ## CRUK0098       81       46       55       64       40                60
    ## CRUK0099       92       57       66       75       56       60         
    ## CRUK0100       54       49       58       67       79       83       86
    ##          CRUK0100
    ## CRUK0001       96
    ## CRUK0002       57
    ## CRUK0003       86
    ## CRUK0004       83
    ## CRUK0005       95
    ## CRUK0006      100
    ## CRUK0007       86
    ## CRUK0008       76
    ## CRUK0009      100
    ## CRUK0010       67
    ## CRUK0011       64
    ## CRUK0012       63
    ## CRUK0013       49
    ## CRUK0014      113
    ## CRUK0015       83
    ## CRUK0016       77
    ## CRUK0017      104
    ## CRUK0018       72
    ## CRUK0019       63
    ## CRUK0020      155
    ## CRUK0021       78
    ## CRUK0022       78
    ## CRUK0023       87
    ## CRUK0024       63
    ## CRUK0025      115
    ## CRUK0026       82
    ## CRUK0027      115
    ## CRUK0028       67
    ## CRUK0029       82
    ## CRUK0030      124
    ## CRUK0031       72
    ## CRUK0032       56
    ## CRUK0033       56
    ## CRUK0034       69
    ## CRUK0035       77
    ## CRUK0036       87
    ## CRUK0037       70
    ## CRUK0038       66
    ## CRUK0039       69
    ## CRUK0040       69
    ## CRUK0041       70
    ## CRUK0042       63
    ## CRUK0043       46
    ## CRUK0044       63
    ## CRUK0045       45
    ## CRUK0046       59
    ## CRUK0047       60
    ## CRUK0048       98
    ## CRUK0049      152
    ## CRUK0050       56
    ## CRUK0051      152
    ## CRUK0052      155
    ## CRUK0054       63
    ## CRUK0055       48
    ## CRUK0056       59
    ## CRUK0057       56
    ## CRUK0058       76
    ## CRUK0059       63
    ## CRUK0060       75
    ## CRUK0061       43
    ## CRUK0062      127
    ## CRUK0063      106
    ## CRUK0064       82
    ## CRUK0065      126
    ## CRUK0066       68
    ## CRUK0067       87
    ## CRUK0068      134
    ## CRUK0069       95
    ## CRUK0070       96
    ## CRUK0071       86
    ## CRUK0072      130
    ## CRUK0073       78
    ## CRUK0074      128
    ## CRUK0075      107
    ## CRUK0076      133
    ## CRUK0077       87
    ## CRUK0078       92
    ## CRUK0079      126
    ## CRUK0080       85
    ## CRUK0081       59
    ## CRUK0082      133
    ## CRUK0083      109
    ## CRUK0084       47
    ## CRUK0085       52
    ## CRUK0086       83
    ## CRUK0087      104
    ## CRUK0088       76
    ## CRUK0089       76
    ## CRUK0090       54
    ## CRUK0091       46
    ## CRUK0092       78
    ## CRUK0093       54
    ## CRUK0094       49
    ## CRUK0095       58
    ## CRUK0096       67
    ## CRUK0097       79
    ## CRUK0098       83
    ## CRUK0099       86
    ## CRUK0100         
    ## 
    ## 
    ## $cluster$parameters
    ## $cluster$parameters$hc.method
    ## [1] "ward"
    ## 
    ## $cluster$parameters$split.method
    ## [1] "cutreeHybrid"
    ## 
    ## $cluster$parameters$min.group.size
    ## [1] 2
    ## 
    ## 
    ## $cluster$fits
    ## $cluster$fits$hc
    ## Call:     cluster::agnes(x = cluster$distances$dist_obj, method = hc.method) 
    ## Agglomerative coefficient:  0.8491595 
    ## Order of objects:
    ##  [1] CRUK0001 CRUK0004 CRUK0015 CRUK0022 CRUK0058 CRUK0026 CRUK0080
    ##  [8] CRUK0048 CRUK0021 CRUK0003 CRUK0007 CRUK0010 CRUK0012 CRUK0019
    ## [15] CRUK0054 CRUK0028 CRUK0041 CRUK0072 CRUK0002 CRUK0032 CRUK0043
    ## [22] CRUK0045 CRUK0084 CRUK0055 CRUK0094 CRUK0085 CRUK0057 CRUK0056
    ## [29] CRUK0095 CRUK0033 CRUK0046 CRUK0013 CRUK0061 CRUK0050 CRUK0047
    ## [36] CRUK0024 CRUK0060 CRUK0008 CRUK0031 CRUK0073 CRUK0016 CRUK0066
    ## [43] CRUK0081 CRUK0090 CRUK0091 CRUK0093 CRUK0100 CRUK0011 CRUK0042
    ## [50] CRUK0044 CRUK0059 CRUK0038 CRUK0096 CRUK0040 CRUK0034 CRUK0037
    ## [57] CRUK0018 CRUK0039 CRUK0023 CRUK0036 CRUK0089 CRUK0092 CRUK0071
    ## [64] CRUK0078 CRUK0083 CRUK0075 CRUK0063 CRUK0067 CRUK0005 CRUK0029
    ## [71] CRUK0035 CRUK0088 CRUK0097 CRUK0098 CRUK0064 CRUK0086 CRUK0069
    ## [78] CRUK0009 CRUK0070 CRUK0006 CRUK0077 CRUK0099 CRUK0017 CRUK0062
    ## [85] CRUK0065 CRUK0087 CRUK0074 CRUK0068 CRUK0076 CRUK0079 CRUK0082
    ## [92] CRUK0014 CRUK0027 CRUK0025 CRUK0030 CRUK0052 CRUK0020 CRUK0049
    ## [99] CRUK0051
    ## Height (summary):
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    5.00   31.95   56.07   68.11   87.69  352.24 
    ## 
    ## Available components:
    ## [1] "order"     "height"    "ac"        "merge"     "diss"      "call"     
    ## [7] "method"    "order.lab"
    ## 
    ## $cluster$fits$dendrogram
    ## 'dendrogram' with 2 branches and 99 members total, at height 352.2393 
    ## 
    ## $cluster$fits$K
    ## [1] 11
    ## 
    ## $cluster$fits$labels
    ## CRUK0001 CRUK0004 CRUK0015 CRUK0022 CRUK0058 CRUK0026 CRUK0080 CRUK0048 
    ##     "C2"     "C2"     "C2"     "C2"     "C2"     "C2"     "C2"     "C2" 
    ## CRUK0021 CRUK0003 CRUK0007 CRUK0010 CRUK0012 CRUK0019 CRUK0054 CRUK0028 
    ##     "C2"     "C2"     "C2"     "C2"     "C2"     "C2"     "C2"     "C2" 
    ## CRUK0041 CRUK0072 CRUK0002 CRUK0032 CRUK0043 CRUK0045 CRUK0084 CRUK0055 
    ##     "C2"     "C2"     "C1"     "C1"     "C1"     "C1"     "C1"     "C1" 
    ## CRUK0094 CRUK0085 CRUK0057 CRUK0056 CRUK0095 CRUK0033 CRUK0046 CRUK0013 
    ##     "C1"     "C1"     "C1"     "C1"     "C1"     "C1"     "C1"     "C1" 
    ## CRUK0061 CRUK0050 CRUK0047 CRUK0024 CRUK0060 CRUK0008 CRUK0031 CRUK0073 
    ##     "C1"     "C1"     "C1"     "C1"     "C1"     "C1"     "C1"     "C1" 
    ## CRUK0016 CRUK0066 CRUK0081 CRUK0090 CRUK0091 CRUK0093 CRUK0100 CRUK0011 
    ##     "C5"     "C5"     "C5"     "C5"     "C5"     "C5"     "C5"     "C4" 
    ## CRUK0042 CRUK0044 CRUK0059 CRUK0038 CRUK0096 CRUK0040 CRUK0034 CRUK0037 
    ##     "C4"     "C4"     "C4"     "C4"     "C4"     "C4"     "C4"     "C4" 
    ## CRUK0018 CRUK0039 CRUK0023 CRUK0036 CRUK0089 CRUK0092 CRUK0071 CRUK0078 
    ##     "C4"     "C4"     "C4"     "C6"     "C6"     "C6"     "C6"     "C6" 
    ## CRUK0083 CRUK0075 CRUK0063 CRUK0067 CRUK0005 CRUK0029 CRUK0035 CRUK0088 
    ##     "C6"     "C6"    "C10"    "C10"     "C3"     "C3"     "C3"     "C3" 
    ## CRUK0097 CRUK0098 CRUK0064 CRUK0086 CRUK0069 CRUK0009 CRUK0070 CRUK0006 
    ##     "C3"     "C3"     "C3"     "C3"     "C3"     "C3"     "C3"     "C3" 
    ## CRUK0077 CRUK0099 CRUK0017 CRUK0062 CRUK0065 CRUK0087 CRUK0074 CRUK0068 
    ##     "C3"     "C3"     "C3"     "C8"     "C8"     "C8"     "C8"     "C8" 
    ## CRUK0076 CRUK0079 CRUK0082 CRUK0014 CRUK0027 CRUK0025 CRUK0030 CRUK0052 
    ##     "C9"     "C9"     "C9"     "C7"     "C7"     "C7"     "C7"     "C7" 
    ## CRUK0020 CRUK0049 CRUK0051 
    ##     "C7"    "C11"    "C11" 
    ## 
    ## 
    ## 
    ## attr(,"class")
    ## [1] "rev_cohort_fit"
    ## attr(,"call")
    ## revolver_cohort(dataset = subset_data, ONLY.DRIVER = T, MIN.CLUSTER.SIZE = 0)

# Access patient-level data

**Note** Since the new release of REVOLVER, we have implemented the
internal structure of the objects using the tidy data.frame
representations from [tidyverse](https://www.tidyverse.org/). Most
functions now return `tibble` data.frames that can be processed with the
`dplyr` jargon.

### Getters

We have made available several types of getters to perform queries on
the data. Getter functions for the data have a common parametrization;
for instance getter function`Drivers` takes as input

  - `x` a REVOLVER cohort object;
  - `patients` a list of patients IDs that will be used to subset the
    outputs (all by default);

<!-- end list -->

``` r
# Access all data for a patient
Data(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001')
```

    ## # A tibble: 7 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0001  NF1       TRUE      FALSE     1                  1
    ## 2 __mu… CRUK… CRUK0001  ARHGAP35  TRUE      FALSE     2                  1
    ## 3 __mu… CRUK… CRUK0001  TP53      TRUE      TRUE      3                  4
    ## 4 __mu… CRUK… CRUK0001  MGA       TRUE      TRUE      3                  4
    ## 5 __mu… CRUK… CRUK0001  WRN       TRUE      TRUE      3                  4
    ## 6 __mu… Anno… CRUK0001  EGFR      TRUE      TRUE      3                  4
    ## 7 __mu… CRUK… CRUK0001  PASK      TRUE      FALSE     5                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>

``` r
# Access only the drivers for a patient
Drivers(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001')
```

    ## # A tibble: 7 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0001  NF1       TRUE      FALSE     1                  1
    ## 2 __mu… CRUK… CRUK0001  ARHGAP35  TRUE      FALSE     2                  1
    ## 3 __mu… CRUK… CRUK0001  TP53      TRUE      TRUE      3                  4
    ## 4 __mu… CRUK… CRUK0001  MGA       TRUE      TRUE      3                  4
    ## 5 __mu… CRUK… CRUK0001  WRN       TRUE      TRUE      3                  4
    ## 6 __mu… Anno… CRUK0001  EGFR      TRUE      TRUE      3                  4
    ## 7 __mu… CRUK… CRUK0001  PASK      TRUE      FALSE     5                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>

``` r
# Access the names of the samples for a patient
Samples(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001')
```

    ## [1] "R1" "R2" "R3"

``` r
# Get the list of truncal (i.e., clonal) mutations in a patient
Truncal(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001')
```

    ## # A tibble: 4 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0001  TP53      TRUE      TRUE      3                  4
    ## 2 __mu… CRUK… CRUK0001  MGA       TRUE      TRUE      3                  4
    ## 3 __mu… CRUK… CRUK0001  WRN       TRUE      TRUE      3                  4
    ## 4 __mu… Anno… CRUK0001  EGFR      TRUE      TRUE      3                  4
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>

``` r
# Get the list of subclonal mutations in a patient
Subclonal(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001')
```

    ## # A tibble: 3 x 12
    ##   id    Misc  patientID variantID is.driver is.clonal cluster cluster_size
    ##   <chr> <chr> <chr>     <chr>     <lgl>     <lgl>     <chr>          <int>
    ## 1 __mu… CRUK… CRUK0001  NF1       TRUE      FALSE     1                  1
    ## 2 __mu… CRUK… CRUK0001  ARHGAP35  TRUE      FALSE     2                  1
    ## 3 __mu… CRUK… CRUK0001  PASK      TRUE      FALSE     5                  1
    ## # … with 4 more variables: CCF <chr>, R1 <dbl>, R2 <dbl>, R3 <dbl>

``` r
# Return the CCF entry for all the mutations of a patient,
CCF(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001')
```

    ## # A tibble: 7 x 8
    ##   id            variantID is.driver is.clonal cluster    R1    R2    R3
    ##   <chr>         <chr>     <lgl>     <lgl>     <chr>   <dbl> <dbl> <dbl>
    ## 1 __mut_id_756  NF1       TRUE      FALSE     1        0.86  0     0   
    ## 2 __mut_id_1225 ARHGAP35  TRUE      FALSE     2        0.19  0     0.95
    ## 3 __mut_id_1350 TP53      TRUE      TRUE      3        0.99  0.99  1   
    ## 4 __mut_id_1466 MGA       TRUE      TRUE      3        0.99  0.99  1   
    ## 5 __mut_id_1519 WRN       TRUE      TRUE      3        0.97  0.98  0.99
    ## 6 __mut_id_1540 EGFR      TRUE      TRUE      3        0.99  0.99  1   
    ## 7 __mut_id_1796 PASK      TRUE      FALSE     5        0.82  0     0.71

``` r
# Return the CCF entry for all the clones of a patient, the overall CCF
# values are obtained by REVOLVER from the average of CCF values across clones.
CCF_clusters(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001')
```

    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 3           4 TRUE      TRUE       0.99  0.99  1   
    ## 2 1           1 TRUE      FALSE      0.86  0     0   
    ## 3 2           1 TRUE      FALSE      0.19  0     0.95
    ## 4 5           1 TRUE      FALSE      0.82  0     0.71

### Summary statistics for patients’ data

You can get a broad set of summary statistics about the
`TRACERx_NEJM_2017_REVOLVER` cohort for a custom set of patients. The
statistics that are available in summarised format are patient-level
(mutatational burdern, drivers etc.), and driver-level (frequency,
clonality
etc.).

``` r
# This returns patient-level statistics like the number of biopsies, overall mutations, drivers,
# clones with drivers, truncal and subclonal mutations.
# 
# This is also synonim to `Stats(TRACERx_NEJM_2017_REVOLVER)`
Stats_cohort(TRACERx_NEJM_2017_REVOLVER)
```

    ## # A tibble: 99 x 7
    ##    patientID numBiopsies numMutations numDriverMutati… numClonesWithDr…
    ##    <chr>           <int>        <int>            <int>            <int>
    ##  1 CRUK0001            3            7                7                4
    ##  2 CRUK0002            3            7                7                4
    ##  3 CRUK0003            5            4                4                2
    ##  4 CRUK0004            4            4                4                2
    ##  5 CRUK0005            4            6                6                2
    ##  6 CRUK0006            2            6                6                3
    ##  7 CRUK0007            2            3                3                1
    ##  8 CRUK0008            2            6                6                2
    ##  9 CRUK0009            4            7                7                2
    ## 10 CRUK0010            2            3                3                1
    ## # … with 89 more rows, and 2 more variables: numTruncalMutations <int>,
    ## #   numSubclonalMutations <int>

``` r
# This returns driver-level statistics like the number of times the driver is clonal,
# subclonal, or found in general, and for quantity normalized by cohort size (i.e., the percentage)
Stats_drivers(TRACERx_NEJM_2017_REVOLVER)
```

    ## # A tibble: 79 x 7
    ##    variantID numClonal p_clonal numSubclonal p_subclonal N_tot  p_tot
    ##    <chr>         <dbl>    <dbl>        <dbl>       <dbl> <dbl>  <dbl>
    ##  1 TP53             53   0.535             3      0.0303    56 0.566 
    ##  2 KRAS             24   0.242             4      0.0404    28 0.283 
    ##  3 EGFR             21   0.212             1      0.0101    22 0.222 
    ##  4 PIK3CA           20   0.202             1      0.0101    21 0.212 
    ##  5 CDKN2A           14   0.141             0      0         14 0.141 
    ##  6 SOX2             14   0.141             0      0         14 0.141 
    ##  7 KEAP1            12   0.121             0      0         12 0.121 
    ##  8 TERT             11   0.111             2      0.0202    13 0.131 
    ##  9 FGFR1             9   0.0909            0      0          9 0.0909
    ## 10 STK11             8   0.0808            0      0          8 0.0808
    ## # … with 69 more rows

The list of all patients in the cohort is accessible as
`TRACERx_NEJM_2017_REVOLVER$patients`, and these functions can be run on
a smaller subset of
patients.

``` r
Stats_cohort(TRACERx_NEJM_2017_REVOLVER, patients = TRACERx_NEJM_2017_REVOLVER$patients[1:5])
```

    ## # A tibble: 5 x 7
    ##   patientID numBiopsies numMutations numDriverMutati… numClonesWithDr…
    ##   <chr>           <int>        <int>            <int>            <int>
    ## 1 CRUK0001            3            7                7                4
    ## 2 CRUK0002            3            7                7                4
    ## 3 CRUK0003            5            4                4                2
    ## 4 CRUK0004            4            4                4                2
    ## 5 CRUK0005            4            6                6                2
    ## # … with 2 more variables: numTruncalMutations <int>,
    ## #   numSubclonalMutations <int>

# Access the trees in the cohort

Trees have getters similar to the data, and getters distinguish from
trees before and after the fit.

**Note** The tree fits might be slightly different from the trees before
the fit, because their Informatin Transfer is not expanded. Therefore
keep this in mind when comparing trees.

## Getters

You can to extract the tree of a patient, before its fit. This can be
one specific tree, or all of them at once. Trees before the fit are
indexed by their rank, which is obtained from the ordering of the tree
scores, which are obtained by the evaluated tree structure before the
fit.

These getters, for instance `Phylo`, take as parameter

  - `x` the cohort object;
  - `p` the patient identifier;
  - `rank` the rank of the tree to extract;
  - `data` to decide whether one wants the trees before the fit
    (`trees`), or the actual fit tree `fits`.

By logic, if you are asking for the fit trees (`data = 'fits'`), the
`rank` parameter is not considered (because there is only 1 tree fit by
REVOLVER).

``` r
# Access the top-rank tree for a patient
Phylo(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001', rank = 1)
```

    ##  [ ctree - ctree rank 1/3 for CRUK0001 ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 3           4 TRUE      TRUE       0.99  0.99  1   
    ## 2 1           1 TRUE      FALSE      0.86  0     0   
    ## 3 2           1 TRUE      FALSE      0.19  0     0.95
    ## 4 5           1 TRUE      FALSE      0.82  0     0.71
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-3 [R2] :: TP53, MGA, WRN, EGFR
    ##     |-1 :: NF1
    ##     | \-5 :: PASK
    ##     \-2 :: ARHGAP35
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> TP53 
    ##    GL ---> MGA 
    ##    GL ---> WRN 
    ##    GL ---> EGFR 
    ##    TP53 ---> NF1 
    ##    MGA ---> NF1 
    ##    WRN ---> NF1 
    ##    EGFR ---> NF1 
    ##    TP53 ---> ARHGAP35 
    ##    MGA ---> ARHGAP35 
    ##    WRN ---> ARHGAP35 
    ##    EGFR ---> ARHGAP35 
    ##    NF1 ---> PASK 
    ## 
    ## Tree score 0.111111111111111

``` r
# Access all trees for a patient. We use CRUK0002 because it has only 3 trees
Phylo(TRACERx_NEJM_2017_REVOLVER, 'CRUK0002', rank = NULL)
```

    ## $`1`
    ##  [ ctree - ctree rank 1/2 for CRUK0002 ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      FALSE      0     0.92  0   
    ## 2 2           2 TRUE      TRUE       0.99  0.98  0.99
    ## 3 5           1 TRUE      FALSE      0.78  0     0   
    ## 4 6           1 TRUE      FALSE      0.96  0.03  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 :: MET, TERT
    ##     |-6 :: EP300
    ##     | \-5 :: NF1
    ##     \-1 :: RB1, IKZF1, KRAS
    ## 
    ## Information transfer  
    ## 
    ##    MET ---> RB1 
    ##    MET ---> IKZF1 
    ##    MET ---> KRAS 
    ##    TERT ---> RB1 
    ##    TERT ---> IKZF1 
    ##    TERT ---> KRAS 
    ##    GL ---> MET 
    ##    GL ---> TERT 
    ##    EP300 ---> NF1 
    ##    MET ---> EP300 
    ##    TERT ---> EP300 
    ## 
    ## Tree score 0.75 
    ## 
    ## $`2`
    ##  [ ctree - ctree rank 2/2 for CRUK0002 ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 1           3 TRUE      FALSE      0     0.92  0   
    ## 2 2           2 TRUE      TRUE       0.99  0.98  0.99
    ## 3 5           1 TRUE      FALSE      0.78  0     0   
    ## 4 6           1 TRUE      FALSE      0.96  0.03  0.98
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-2 :: MET, TERT
    ##     \-1 :: RB1, IKZF1, KRAS
    ##      \-6 :: EP300
    ##       \-5 :: NF1
    ## 
    ## Information transfer  
    ## 
    ##    MET ---> RB1 
    ##    MET ---> IKZF1 
    ##    MET ---> KRAS 
    ##    TERT ---> RB1 
    ##    TERT ---> IKZF1 
    ##    TERT ---> KRAS 
    ##    GL ---> MET 
    ##    GL ---> TERT 
    ##    EP300 ---> NF1 
    ##    RB1 ---> EP300 
    ##    IKZF1 ---> EP300 
    ##    KRAS ---> EP300 
    ## 
    ## Tree score 0.0833333333333333

Notice that in the printing of a tree to screen you can immediately see
the Information Transfer (IT) for the driver genes. In general, you can
access the IT of a tree with another getter, which takes as extra
parameter `type` in order to return either the transfer across drivers,
or across clones annotated in a tree.

``` r
# Information Transfer for the drivers, top-ranking tree
ITransfer(TRACERx_NEJM_2017_REVOLVER, "CRUK0001", rank = 1, type = 'drivers')
```

    ## # A tibble: 13 x 2
    ##    from  to      
    ##    <chr> <chr>   
    ##  1 GL    TP53    
    ##  2 GL    MGA     
    ##  3 GL    WRN     
    ##  4 GL    EGFR    
    ##  5 TP53  NF1     
    ##  6 MGA   NF1     
    ##  7 WRN   NF1     
    ##  8 EGFR  NF1     
    ##  9 TP53  ARHGAP35
    ## 10 MGA   ARHGAP35
    ## 11 WRN   ARHGAP35
    ## 12 EGFR  ARHGAP35
    ## 13 NF1   PASK

``` r
# Information Transfer for the clones, top-ranking tree
ITransfer(TRACERx_NEJM_2017_REVOLVER, "CRUK0001", rank = 1, type = 'clones')
```

    ## # A tibble: 4 x 2
    ##   from  to   
    ##   <chr> <chr>
    ## 1 GL    3    
    ## 2 3     1    
    ## 3 3     2    
    ## 4 1     5

Fit trees can be accessed using the `data` argument. Essentially this is
like before, but does not require specifying a `rank` parameter.

``` r
# Access the fit tree for a patient
Phylo(TRACERx_NEJM_2017_REVOLVER, 'CRUK0001', data = 'fits')
```

    ##  [ ctree - ctree rank 1/3 for CRUK0001 - Information Transfer expanded via Transfer Learning ] 
    ## 
    ## # A tibble: 4 x 7
    ##   cluster nMuts is.driver is.clonal    R1    R2    R3
    ##   <chr>   <int> <lgl>     <lgl>     <dbl> <dbl> <dbl>
    ## 1 3           4 TRUE      TRUE       0.99  0.99  1   
    ## 2 1           1 TRUE      FALSE      0.86  0     0   
    ## 3 2           1 TRUE      FALSE      0.19  0     0.95
    ## 4 5           1 TRUE      FALSE      0.82  0     0.71
    ## 
    ## Tree shape (drivers annotated)  
    ## 
    ##   \-GL
    ##    \-3 [R2] :: TP53, MGA, WRN, EGFR
    ##     |-1 :: NF1
    ##     | \-5 :: PASK
    ##     \-2 :: ARHGAP35
    ## 
    ## Information transfer  
    ## 
    ##    GL ---> EGFR 
    ##    GL ---> WRN 
    ##    GL ---> MGA 
    ##    EGFR ---> TP53 
    ##    WRN ---> TP53 
    ##    TP53 ---> NF1 
    ##    MGA ---> NF1 
    ##    TP53 ---> ARHGAP35 
    ##    MGA ---> ARHGAP35 
    ##    NF1 ---> PASK 
    ## 
    ## Tree score 0.111111111111111

``` r
# Information Transfer for the drivers, top-ranking tree. Notice that this is different
# from the result of the above call, because the transfer after fitting is expanded
ITransfer(TRACERx_NEJM_2017_REVOLVER, "CRUK0001", rank = 1, type = 'drivers', data = 'fits')
```

    ## # A tibble: 10 x 2
    ##    from  to      
    ##    <chr> <chr>   
    ##  1 GL    EGFR    
    ##  2 GL    WRN     
    ##  3 GL    MGA     
    ##  4 EGFR  TP53    
    ##  5 WRN   TP53    
    ##  6 TP53  NF1     
    ##  7 MGA   NF1     
    ##  8 TP53  ARHGAP35
    ##  9 MGA   ARHGAP35
    ## 10 NF1   PASK

### Summary statistics for trees and fits

There are getters for summary statistics that work for trees and fits,
with the same principles fo the getters for the data discussed
above

``` r
# This returns patient-level statistics for the trees available in a patient. The tibble reports
# whether the patient has trees annotated, the total number of trees, their minimum and maximum
# scores mutations and the total number of differnet combinations of Information Transfer for 
# the available trees.
Stats_trees(TRACERx_NEJM_2017_REVOLVER)
```

    ## # A tibble: 99 x 6
    ##    patientID hasTrees numTrees maxScore minScore combInfTransf
    ##    <chr>     <lgl>       <int>    <dbl>    <dbl>         <int>
    ##  1 CRUK0001  TRUE            3    0.111   0.111              3
    ##  2 CRUK0002  TRUE            2    0.75    0.0833             2
    ##  3 CRUK0003  TRUE            1    1       1                  1
    ##  4 CRUK0004  TRUE            1    1       1                  1
    ##  5 CRUK0005  TRUE            1    1       1                  1
    ##  6 CRUK0006  TRUE            2    0.667   0.167              2
    ##  7 CRUK0007  TRUE            1    1       1                  1
    ##  8 CRUK0008  TRUE            1    1       1                  1
    ##  9 CRUK0009  TRUE            1    1       1                  1
    ## 10 CRUK0010  TRUE            1    1       1                  1
    ## # … with 89 more rows

``` r
# This returns the same table of above, but with some extended information on the fits (like the fit rank, etc)
Stats_fits(TRACERx_NEJM_2017_REVOLVER)
```

    ## # A tibble: 99 x 9
    ##    patientID hasTrees numTrees maxScore minScore combInfTransf Solution
    ##    <chr>     <lgl>       <int>    <dbl>    <dbl>         <int>    <int>
    ##  1 CRUK0001  TRUE            3    0.111   0.111              3        1
    ##  2 CRUK0002  TRUE            2    0.75    0.0833             2        1
    ##  3 CRUK0003  TRUE            1    1       1                  1        1
    ##  4 CRUK0004  TRUE            1    1       1                  1        1
    ##  5 CRUK0005  TRUE            1    1       1                  1        1
    ##  6 CRUK0006  TRUE            2    0.667   0.167              2        1
    ##  7 CRUK0007  TRUE            1    1       1                  1        1
    ##  8 CRUK0008  TRUE            1    1       1                  1        1
    ##  9 CRUK0009  TRUE            1    1       1                  1        1
    ## 10 CRUK0010  TRUE            1    1       1                  1        1
    ## # … with 89 more rows, and 2 more variables: converged <lgl>,
    ## #   penalty <dbl>
