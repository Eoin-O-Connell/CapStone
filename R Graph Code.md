# R Graph Code


After import of CSV files this will make a new table With only the W chromosome hits 
```
WChromo <- ChainInfo[ChainInfo$Chromosome == "W", ]
```

This is the one for the autosomes 
```
Autosomes <- TableName[!(TableName$Chromosome %in% c("W", "Z")), ]
```

This Will get the size of each hit 
```
WChromoSize <- (TableName$Start - TableName$End)
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
