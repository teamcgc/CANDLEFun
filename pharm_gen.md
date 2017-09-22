# CANDLEfun for pharmacogenomics
US  
`r doc_date()`  



# Resources

## [Pharmacodb]


```r
library(dplyr)
pdb = src_mysql("pharmacodb", host = "solexadb.cpmth1vkdqqx.us-east-1.rds.amazonaws.com", 
    user = "deeplearn", password = "deeplearn")
```

Tables available include:


```r
pdb_t = sapply(db_list_tables(pdb$con), function(tblname) tbl(pdb, tblname), 
    USE.NAMES = TRUE, simplify = FALSE)
names(pdb_t)
```

```
##  [1] "ar_internal_metadata" "cell_tissues"         "cellosaurus"         
##  [4] "cells"                "datasets"             "dose_responses"      
##  [7] "drug_annots"          "drug_targets"         "drugs"               
## [10] "experiments"          "mol_cells"            "profiles"            
## [13] "schema_migrations"    "source_cell_names"    "source_drug_names"   
## [16] "source_statistics"    "source_tissue_names"  "sources"             
## [19] "targets"              "tissues"
```

Datasets include:


```r
pdb_t$datasets %>% left_join(pdb_t$source_statistics, c(dataset_id = "id")) %>% 
    knitr::kable()
```



 dataset_id.x  dataset_name    dataset_id.y   cell_lines   tissues   drugs   experiments
-------------  -------------  -------------  -----------  --------  ------  ------------
            1  CCLE                       1          504        23      24         11670
            2  CTRPv2                     2          707        29     139         79903
            3  FIMM                       3          887        25     545        395263
            4  gCSI                       4          410        24      16          6560
            5  GDSC1000                   5           71         1      90          9413
            6  GRAY                       6            0         0       0             0
            7  UHNBreast                  7           15         1       4            52

[Pharmacodb]: http://pharmacodb.pmgenomics.ca/

# References


