---
title       : Insert the chapter title here
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf


--- type:NormalExercise lang:r xp:100 skills:1 key:36071e0bd3
## <<<New Exercise>>> 


*** =instructions
Der vorliegende Datensatz enthält Daten über 177 CEO's und dient dazu den Effekt der Unternehmensperformance auf das Gehalt zu ermitteln. 

Ermitteln Sie die Regressionskoeffizienten einer Regression von *gehalt* auf *umsaetze* und *gewinne*. 

*** =hint
Nutzen Sie den Befehl *lm* !

*** =pre_exercise_code
```{r}
load(http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosal1.RData)
gehalt<-data$salary
umsaetze<-data$sales
gewinne<-data$profits
alter<-data$age
ausbildung<-data$college
```

*** =sample_code
```{r}
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
success_msg("Richtig! Zur nächsten Aufgabe...")
```
