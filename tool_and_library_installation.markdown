# Packages and dependencies installation

## CellChat installation
```{r}
# define your library path
user_lib <- "/cluster/home/xxxxxxxx/library"

# make sure the folder exists
dir.create(user_lib, recursive = TRUE, showWarnings = FALSE)

# prepend to .libPaths so R installs & loads from there first
.libPaths(c(user_lib, .libPaths()))


user_lib <- "/cluster/home/t138390uhn/library"
dir.create(user_lib, recursive = TRUE, showWarnings = FALSE)
.libPaths(c(user_lib, .libPaths()))

# CRAN deps
install.packages("NMF", repos="https://cloud.r-project.org", lib=user_lib)

# Bioconductor deps (make sure version matches R 4.4 → Bioc 3.20)
if (!requireNamespace("BiocManager", quietly=TRUE))
  install.packages("BiocManager", repos="https://cloud.r-project.org", lib=user_lib)

BiocManager::install(version="3.20", ask=FALSE, lib=user_lib)
BiocManager::install(c("ComplexHeatmap","SingleCellExperiment"), ask=FALSE, lib=user_lib)

# circlize
install.packages("circlize", repos="https://cloud.r-project.org", lib=user_lib)
# or, if CRAN version fails:
# devtools::install_github("jokergoo/circlize", lib=user_lib)

# CellChat
if (!requireNamespace("devtools", quietly=TRUE))
  install.packages("devtools", repos="https://cloud.r-project.org", lib=user_lib)

devtools::install_github("jinworks/CellChat", lib=user_lib)

# test
library(CellChat, lib.loc=user_lib)
packageVersion("CellChat")

```


