---
title       : Übungsaufgaben 
description : Basierend auf den Aufgaben der Klausur aus dem WS 15/16.
attachments :
 



--- type:NormalExercise lang:r xp:100 skills:1 key:a31a0683bf
## Daten einlesen


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
# Speichern Sie das Ergebnis unter dem Objekt *daten* .
```

*** =solution
```{r}
daten<-read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosa.csv", sep = ",")
```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:36071e0bd3
## Regressionskoeffizienten

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
# Die Variablen *gehalt*, *umsaetze* und *gewinne* sind bereits eingelesen.
# Speichern Sie das Ergebnis der Regression unter dem Objekt *reg1* .
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




--- type:NormalExercise lang:r xp:100 skills:1 key:5732029514
## P-Werte

*** =instructions
Berechnen Sie den P-Wert der Variablen *umsaetze*. Es muss der exakte Wert ohne Rundungen und unter Berücksichtigung von normalverteilten Koeffizienten berechnet werden.
*** =hint
Nutzen Sie den Befehl *pnorm* und die Hinweise aus der Übung/ Vorlesung !

*** =pre_exercise_code
```{r}
data<-read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosa.csv", sep = ",")
gehalt<-data$gehalt
umsaetze<-data$umsaetze
gewinne<-data$gewinne
alter<-data$alter
ausbildung<-data$ausbildung
reg1<-lm(gehalt~umsaetze+gewinne)
summaryObj<- summary(reg1)
b_umsaetze<- summaryObj$coefficients[2, 1]
se_umsaetze<- summaryObj$coefficients[2, 2]
```

*** =sample_code
```{r}
# Der Regressionskoeffizient ist bereits unter der Variable *b_umsaetze* eingelesen.
# Der Standardfehler des Regressionskoeffizienten ist bereits unter der Variable *se_umsaetze* eingelesen.

# Speichern Sie Ihr Ergebnis unter dem Objekt *pwert* ab!
```

*** =solution
```{r}
pwert<- pnorm(-abs(b_umsaetze/se_umsaetze)) * 2 
```

*** =sct
```{r}
test_error()
test_object("pwert",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
```








--- type:NormalExercise lang:r xp:100 skills:1 key:980b862ec8
## Hypothesentests


*** =instructions
Berechnen Sie die Teststatistik zu \[ H_0: \beta_{2}=0.1 \] mit Hilfe eines zweiseitigen Tests. 

Treffen Sie eine Testenscheidung auf einem 10% Signifikanzniveau.

*** =hint
Für die Berechnung der Teststatistik siehe z.B. die Übung zum zweiten Termin.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}


#Für den Fall einer abgelehnten Nullhypothese speichern Sie Ihre Testenscheidung mit *ablehnung <- True'
#Für den Fall einer nicht abgelehnten Nullhypothese speichern Sie Ihre Testenscheidung mit *ablehnung <- False'
```

*** =solution
```{r}

```

*** =sct
```{r}

```
