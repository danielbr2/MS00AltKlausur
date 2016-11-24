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
read.csv( url , sep="," )

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
test_error()
test_object("daten",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
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
# Nutzen Sie *umsaetze* als ersten und *gewinne* als zweiten Regressor.
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

Berechnen Sie dazu die Teststatistik und den relevanten kritischen Wert (5% Irrtumswahrscheinlichkeit). 

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
R2u<-summary(reg2)$r.squared
R2r<- 0
teststat<- ((R2u-R2r)/(1-R2u))*((177-2-1)/2)
kritWert<- qf(1-0.05,2,177-2-1)
```

*** =sct
```{r}
test_error()
test_object("teststat",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
test_object("kritWert",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
```




--- type:NormalExercise lang:r xp:100 skills:1 key:926ab53810
## Funktionale Form (1)


*** =instructions
Schätzen Sie ein Modell, sodass Sie folgende Interpretation des Regressionskoeffizienten erhalten:

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
# Nutzen Sie *umsaetze* als ersten und *gewinne* als zweiten Regressor.
# Speichern Sie Ihr Ergebnis unter dem Objekt *reg2* .
```

*** =solution
```{r}
reg2<-lm(I(log(gehalt))~umsaetze+gewinne)
```

*** =sct
```{r}
test_error()
test_object("reg2",
            undefined_msg = "Hier hat etwas nicht geklappt. Versuchen Sie es erneut!",
            incorrect_msg = "Es wurden falsche Werte zugewiesen.")
success_msg("Richtig!")
```





--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:2fbd51b6fe
## Heteroskedastie

Testen Sie für die Regression *gehalt* auf *umsaetze* und *gewinne*, ob ein Problem mit Heteroskedastie vorliegt.

*** =instructions
- Es liegt kein Problem mit Heteroskedastie vor.
- Die Homoskedastie Hypothese kann nicht verworfen werden.
- Es liegt ein Problem mit Heteroskedastie vor.

*** =hint
Verwenden Sie die Funktion bptest().
*** =pre_exercise_code
```{r}
data<-read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosa.csv", sep = ",")
gehalt<-data$gehalt
umsaetze<-data$umsaetze
gewinne<-data$gewinne
alter<-data$alter
ausbildung<-data$ausbildung
library(lmtest)
#reg2<-lm(gehalt~umsaetze+gewinne)
#bptest(reg2)
```

*** =sct
```{r}
msg1 = "Falsch."
msg2 = "Richtig!"
msg3 = "Falsch. Beachte den P-Wert des BP Tests."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3))
```



--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:ad0a22b311
## Funktionale Form (2)

Testen Sie, ob Anzeichen für eine Fehlspezifikation der funktionalen Form vorliegen. Führen Sie dazu einen RESET Test mit zweiten und dritten Polynomen durch. 

Es gilt weiterhin das Regressionsmodell von *gehalt* auf *umsaetze* und *gewinne*. 

*** =instructions
- auf einem 1% Signifikanzniveau lässt sich H0 verwerfen.
- auf einem 5% Signifikanzniveau lässt sich H0 verwerfen.
- auf einem 10% Signifikanzniveau lässt sich H0 verwerfen.
- H0 lässt sich nicht verwerfen auf den gängigen Signifikanzniveaus.
*** =hint
Verwenden Sie den linearHypothesis() Befehl und Übung oder Vorlesung (siehe z.B. Skript S. 197)

*** =pre_exercise_code
```{r}
library(car)
data<-read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2219/datasets/ceosa.csv", sep = ",")
gehalt<-data$gehalt
umsaetze<-data$umsaetze
gewinne<-data$gewinne
alter<-data$alter
ausbildung<-data$ausbildung

#reg4<-lm(gehalt~umsaetze + gewinne)
#summary(reg4)

#ydach2 <- fitted(reg4)^2
#ydach3 <- fitted(reg4)^3

#summary(unrestr <- lm(gehalt~umsaetze + gewinne + ydach2 + ydach3))

#linearHypothesis(unrestr,c("ydach2=0","ydach3=0"))

```

*** =sct
```{r}
msg1 = "Falsch."
msg2 = "Falsch."
msg3 = "Richtig!"
msg4 = "Falsch."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```
