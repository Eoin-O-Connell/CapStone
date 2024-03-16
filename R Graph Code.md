# R Code
To get % ERV Basepairs
---
After import of CSV files this will make a new table With only the W chromosome hits 
```
WChromo <- ChainInfo[ChainInfo$Chromosome == "W", ]
```

This is the one for the autosomes 
```
Autosomes <- ChainInfo[!(ChainInfo$Chromosome %in% c("W", "Z")), ]
```

This Will get the size of each hit 
```
WChromoSize <- (WChromo$Start - WChromo$End)
```

used to make all sizes positive
```
WChromoSizeT<-abs(WChromoSize)
```

adds all the lengths together
```
sum(WChromoSizeT)

WPercent<-(sum(WChromoSizeT)/Bp of Chromosome)*100
```


this just outputs a basic graph 
```
Graph <- cbind(ZPercent, WPercent, AutosomePercent)

OrderedGraph <- Graph[, order(-colSums(data))]

barplot(OrderedGraph, beside = TRUE, names.arg = c("W", "Autosomes", "Z"),
        xlab = "Chromosome", ylab = "Percentage", 
        main = "Zootoca vivipara Percentage ERV",
        cex.names = 2, cex.axis = 2, cex.main = 2)
```
# To get full length ERVs
---
Creates selection criteria From the Retrotector output
```
ENV <- ChainInfo[grepl("TM|SU", ChainInfo$SubGenes), ]
Pol <- ChainInfo[grepl("DU|IN|RNH|RT", ChainInfo$SubGenes), ]
Pro <- ChainInfo[grepl("PR|DU", ChainInfo$SubGenes), ]
Gag <- ChainInfo[grepl("MA|CA|NC", ChainInfo$SubGenes), ]
Ltr5 <- ChainInfo[grepl("5LTR", ChainInfo$SubGenes), ]
Ltr3 <- ChainInfo[grepl("3LTR", ChainInfo$SubGenes), ]
```
This selects the samples with all the criteria 
```
FL_ERVs <- ChainInfo[which(rownames(ChainInfo) %in% rownames(Ltr3) & 
                          rownames(ChainInfo) %in% rownames(Ltr5) &
                          rownames(ChainInfo) %in% rownames(Gag) &
                          rownames(ChainInfo) %in% rownames(Pol) &
                          rownames(ChainInfo) %in% rownames(Pro) &
                          rownames(ChainInfo) %in% rownames(ENV)), ]

```
This Filters out the rows by chromosome 
```
WChromo_FL <- FL_ERVs[FL_ERVs$Chromosome == "W", ]
```
For the autosomes
```
Autosomes_FL <- FL_ERVs[!(FL_ERVs$Chromosome %in% c("W", "Z")), ]
```
