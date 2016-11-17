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
## Hypothesentest: t-Test


*** =instructions
Berechnen Sie die Teststatistik zu der Nullhypothese **beta_umsaetze= -0.002** mit Hilfe eines zweiseitigen Tests. 

Treffen Sie eine Testenscheidung auf einem 10% Signifikanzniveau.

*** =hint
Für die Berechnung der Teststatistik siehe z.B. die Übung zum zweiten Termin.

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
# Die Variablen *b_umsaetze* und *se_umsaetze* sind bereits eingelesen.

# Speichern Sie die Teststatistik unter dem Objekt *teststat* .
# Für den Fall einer abgelehnten Nullhypothese speichern Sie Ihre Testenscheidung mit *ablehnung <- TRUE'
# Für den Fall einer nicht abgelehnten Nullhypothese speichern Sie Ihre Testenscheidung mit *ablehnung <- FALSE'
```

*** =solution
```{r}
teststat<- (b_umsaetze- (-0.002))/se_umsaetze
ablehnung <- TRUE
```

*** =sct
```{r}
test_error()
test_object("teststat",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
test_object("ablehnung",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:5b8ef5553f
## Hypothesentest: F-Test


*** =instructions
Beurteilen Sie die Gesamtsignifikanz der Koeffizienten *umsaetze* und *gewinne* durch den Vergleich eines restringierten und unrestringierten Modells.

Berechnen Sie dazu die Teststatistik und den relevanten kritischen Wert. 

*** =hint
Siehe die Übung zum dritten Termin.

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
# Greifen Sie mit dem summary() Befehl auf R-Quadrat zu.

# Speichern Sie Ihr Ergebnis unter *teststat* und *kritWert* .

```

*** =solution
```{r}
reg2<- lm(gehalt~umsaetze+gewinne)
R2r<-summary(reg2)$r.squared
teststat<- ((0-R2r)/(1-0))*((177-2-1)/2)
kritWert<- qf(1-0.05,2,177-2-1)
```

*** =sct
```{r}
test_error()
test_object("teststat",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
test_object("teststat",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
```




--- type:NormalExercise lang:r xp:100 skills:1 key:926ab53810
## Funktionale Form


*** =instructions
Schätzen Sie ein Modell, sodass Sie folgende Interpreation des Regressionskoeffizienten erhalten:

Eine Veränderung von *gewinne* um eine Einheit führt zu einer
Veränderung von *gehalt* um 100 * b %, während die Variable *umsaetze* konstant gehalten wird.

*** =hint
Verwenden Sie ein log Modell.

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
# Speichern Sie Ihr Ergebnis unter dem Objekt *reg2* .
```

*** =solution
```{r}
reg2<-lm(I(log(gehalt)~umsaetze+gewinne))
```

*** =sct
```{r}
test_error()
test_object("reg2",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:d100fd007c
## Heteroskedastie


*** =instructions
Beschreiben Sie kurz, welche Hypothese im Breusch-Pagan Test überprüft wird \textbf{und} wie der Test aufgebaut ist.  
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```



--- type:NormalExercise lang:r xp:100 skills:1 key:6f3df2ec32
## Funktionale Form

*** =instructions
Die funktionale Form ist korrekt
Ergebnis: verwerfe H0 auf 10 \% Signifikanzniveau, höhere Polynome erhöhen den Anteil der erklärten Varianz signifikant.

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```



--- type:NormalExercise lang:r xp:100 skills:1 key:f3487c5cae
## <<<New Exercise>>> 


*** =instructions
Interaktionseffekte...
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```
