Reading in MRICloud Data
========================================================
author: Brian Caffo
date: 4/11/2017
autosize: true

Reading in T1 Volumetric output and working with it
========================================================

- MRICloud formats structrual and functional output in
a text format
- In this tutorial, we discuss how to text process MRICloud
output
- We're creating a set of utilies for working with MRICloud output
- We'll discuss T1 output today

Example T1 output
========================================================


```r
##working in the directory where the ROIs are at
roiDir = "data/"
fileList = dir(roiDir)
subjects = sapply(strsplit(fileList, "_"), function(x) x[2])
```

These have to be downloaded from github
=====




```r
source("readSubject.R")
source("splitFileName.R")
source("subject2df.R")
source("utils.R")
```

Read in a subject (this just grabs volume)
===

```r
fullPath = paste(roiDir, fileList[1], sep = "")
dat = readSubject(fullPath)
length(dat)
```

```
[1] 10
```

```r
dat[[1]]
```

```
                rawid             roi volume type level
1 T1_BNR_131111_A.img Telencephalon_L 406093    1     1
2 T1_BNR_131111_A.img Telencephalon_R 455216    1     1
3 T1_BNR_131111_A.img  Diencephalon_L   7130    1     1
4 T1_BNR_131111_A.img  Diencephalon_R   7570    1     1
5 T1_BNR_131111_A.img   Mesencephalon   9561    1     1
6 T1_BNR_131111_A.img   Metencephalon 142452    1     1
7 T1_BNR_131111_A.img  Myelencephalon   4836    1     1
8 T1_BNR_131111_A.img             CSF 199929    1     1
```

Turns the whole subject into a data frame
===

```r
dat = subject2df(dat)
##makes printing easier gets rid of the id variable
dat$rawid = NULL 
head(dat, 20)
```

```
                roi volume type level
1   Telencephalon_L 406093    1     1
2   Telencephalon_R 455216    1     1
3    Diencephalon_L   7130    1     1
4    Diencephalon_R   7570    1     1
5     Mesencephalon   9561    1     1
6     Metencephalon 142452    1     1
7    Myelencephalon   4836    1     1
8               CSF 199929    1     1
9  CerebralCortex_L 204741    1     2
10 CerebralCortex_R 233382    1     2
11  CerebralNucli_L   9868    1     2
12  CerebralNucli_R  11816    1     2
13       Thalamus_L   4713    1     2
14       Thalamus_R   5086    1     2
15 BasalForebrain_L   2417    1     2
16 BasalForebrain_R   2484    1     2
17  Mesencephalon_L   4863    1     2
18  Mesencephalon_R   4698    1     2
19  Metencephalon_R  70349    1     2
20  Metencephalon_L  72103    1     2
```

Adds ICV variable
===

```r
dat = addSubjectICV(dat)
head(dat)
```

```
              roi volume type level     icv
1 Telencephalon_L 406093    1     1 1232787
2 Telencephalon_R 455216    1     1 1232787
3  Diencephalon_L   7130    1     1 1232787
4  Diencephalon_R   7570    1     1 1232787
5   Mesencephalon   9561    1     1 1232787
6   Metencephalon 142452    1     1 1232787
```

Adds Subject TBV variable
===











```
Error in eval(expr, envir, enclos) : 
  could not find function "addSubjectTBV"
```
