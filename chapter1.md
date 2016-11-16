---
title       : Insert the chapter title here
description : Insert the chapter description here
attachments :
 



--- type:NormalExercise lang:r xp:100 skills:1 key:a31a0683bf
## <<<New Exercise>>> 


*** =instructions
Der vorliegende Datensatz enthält Daten über 177 CEO's und dient dazu den Effekt der Unternehmensperformance auf das Gehalt zu ermitteln. 

Lesen Sie den Datensatz ein.
*** =hint
read.csv()

*** =pre_exercise_code
```{r}
daten<-read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosa.csv", sep = ",")
```

*** =sample_code
```{r}
# Die Daten liegen im CSV Format unter
# http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosa.csv
# Als Seperator wurde "," verwendet.
# Speichern Sie das Ergebnis unter dem Objekt *daten*
```

*** =solution
```{r}
daten<-read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosa.csv", sep = ",")
```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:36071e0bd3
## <<<New Exercise>>> 

*** =instructions
Ermitteln Sie die Regressionskoeffizienten einer Regression von *gehalt* auf *umsaetze* und *gewinne*. 

*** =hint
Nutzen Sie den Befehl *lm* !

*** =pre_exercise_code
```{r}
data<-read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosa.csv", sep = ",")
gehalt<-data$gehalt
umsaetze<-data$umsaetze
gewinne<-data$gewinne
alter<-data$alter
ausbildung<-data$ausbildung
```

*** =sample_code
```{r}
# Die Variablen *gehalt*, *umsaetze* und *gewinne* sind bereits eingelesen
# Speichern Sie das Ergebnis der Regression unter dem Objekt *reg1*
```

*** =solution
```{r}
reg1<-lm(gehalt~umsaetze+gewinne)
```

*** =sct
```{r}
test_error()
test_object("reg1",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
```
