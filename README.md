# Bundesrat Repraesentation

### Analyse des Bundesrats seit 1848


![Historische Vertretung im Bundesrat](title.png)


In der vorliegenden Analyse wurden für die Sonntagszeitung Lebensläufe aller 119 Bundesräte ausgewertet. Auf Basis manuell zusammengetragener Informationen (Wikipedia, Historisches Lexikon der Schweiz) und ergänzt durch vom BFS bereitgestellten Statistiken werden beschreibende Statisiken zur Regierung seit bestehen des Schweizer Bundesstaats erstellt.

Zusätzlich wurde ein Repräsentations-Index erstellt, der beschreibt wie stark die Zusammensetzung des Bundesrats die Parteienstärke in Nationalrat widerspiegelt. Die Repräsentation des Parlaments pro Bundesratspartei wurde ermittelt, indem untersucht wurde, mit welchem Anteil sie im jeweiligen Jahr im Bundesrat vertreten war. Dieser Anteil wurde mit der Parteistärke im Nationalrat verglichen. Je stärker diese Werte voneinander abweichen, desto schlechter war der Wählerwille im Bundesrat vertreten, so die Annahme. Die Summe dieser Differenzen, normalisiert auf die Skala von 0 bis 1, ergibt den Repräsentations-Index. Hohe Werte bedeuten eine gute Repräsentation, tiefe Werte eine schlechte.

Zum Schluss wurde auf Basis der Einwohnerzahlen 2018 berechnet, wie viele Bundesratssitze (und wieviele Amtstage) einzelnen Kantonen und Regionen eigentlich zugeständen wären, wenn die Sitze nach Anzahl der Kantons-Bevölkerung verteilt würden.


#### 


**Artikel**: [Titel des Artikels (inkl. Link)](https://github.com/tamedia-ddj/brennpunkt_bauernhof_public/blob/master/1_Kuerzungen.ipynb)

**Code**: [Notebook "br_representation.ipynb"](https://github.com/tamedia-ddj/bundesraete_repraesentation_2019/blob/master/br_representation.ipynb)

**Datenquellen**: BFS, Wikipedia, Historisches Lexikon der Schweiz, Historische Statistik der Schweiz

## Inhaltsverzeichnis
1. Beschreibende Statistik Bundesrat
2. Repräsentations-Index
3. Verteilung nach Kanton und Region
4. Output-Files
5. Lizenz



## 1. Beschreibende Statistik Bundesrat

Nach dem Laden der Basisinformationen zu den Bundesräten seit 1848 aus Wikipedia ([de](https://de.wikipedia.org/wiki/Liste_der_Mitglieder_des_Schweizerischen_Bundesrates) und [en](https://en.wikipedia.org/wiki/List_of_members_of_the_Swiss_Federal_Council)), wird ein csv exportiert (`internal/data_edit.csv`), dass manuell bearbeitet werden musste. In dieser Recherche (vorwiegend stammen die Informationen von Wikipedia und/oder dem Historischen Lexikon der Schweiz) wird das csv pro Bundesrat um folgende Variablen ergänzt:

Variable | Beschreibunng
--- | --- 
`Geburtsort` | Geburtsort
`Reichtum` | Stammt die Person aus einer vermögenden Familie? (0 oder 1)
`Akad-Familie` | Hatten die Vorfahren eine akademische Bildung? (0 oder 1)
`Akademiker` | Ist die Person selbst Akademiker? (0 oder 1)
`Beruf` | Beruf vor Eintritt in den Bundesrat
`Geschlecht` | m=1, f=0

Nach erneutem Import der Datei werden für die weiteren Untersuchungen die Variable `Reichtum` und `Akad-Familie` zusammengefasst.

Die Haupttabelle für anschliessende Untersuchung ist `data`. In ihr ist für jedes Jahr seit 1848 die Zusammenstellung des Bundesrats festgehalten. Zusätzliche Informationen wie das Durschnittsalter des Bundesrats wird während des Erstellens von `data` berechnet (Aktuelles Jahr minus Geburtsjahr (ohne Tag und Monat)), weitere werden pro Jahr summiert (z.B. Anzahl weiblicher Bundesräte). Für die Zusammenstellung des Bundesrats pro Jahr, wurde alle Bundesräte berücksichtigt, die vor dem Oktober des jeweiligen Jahres im Amt waren.

Ergänzt durch Informationen des Bundesamts für Statistik und der Historischen Statistik Schweiz konnte Entwicklung einzelner Kennzahlen berechnet und zur späteren Visualisierung als csv exportiert werden:

* `output/viz_altersverteilung.csv`
* `output/viz_br_frauenanteil.csv`
* `output/viz_br_social_mobility.csv`





## 2. Repräsentations-Index

Der Repräsentations-Index soll beschreiben wie stark die Zusammensetzung des Bundesrats die Parteienstärke in Nationalrat widerspiegelt.

Einige Beispielelemente:

**Text:**

In der Tabelle `cutbacks` werden auf Ebene der Gemeinde die Anzahl der Betriebe ermittelt, bei denen in 3 oder mehr Jahren (von insgesamt 4 Jahren) Kürzungen veranlasst wurden. Während des Exportprozesses wird der Spalte `multiple_cutbacks` die Anzahl Betriebe hinterlegt, die diese Bedingungen erfüllen.

**Liste**

* item 1
* item 2
* item 3
* ...


**Abschnitt mit code:**

```
for filename in os.listdir(directory):
    if (("srt" in filename)):
        with open(directory+filename, "rb") as file:
            ### decode and parse data
            data = file.read().decode("iso-8859-1")
            subtitle_generator = srt.parse(data)
            subtitle = list(subtitle_generator)
            identified_subtitles = identify_subtitles(subtitle)
            
            ### handle 1. counter for host, 2. comments and 3. counter for rest
            for line in identified_subtitles:
                if line[0] == "Moderator":
                    words_moderator += len(tokenizer.tokenize(line[1]))
                elif line[0] == "<---> Kommentar <--->":
                    comments.append([filename, line[1]])
                else:
                    words_rest += len(tokenizer.tokenize(line[1]))
``` 

**Tabelle:**

Variable | Beschreibunng
--- | --- 
`KUERZUNGEN` | Anzahl Kürzungen auf Gemeindeebene
`BETRIEBE_TOTAL` | Anzahl Betriebe auf Gemeindeebene
`KUERZUNGEN_ANTEIL` | Prozentualer Anteil der Betriebe die Kürzungen erhalten haben
`KUERZUNGEN_BETRAG_AVG` | Durchschnittliche Höhe der Kürzungen pro Gemeinde

## 3. Verteilung nach Kanton und Region



## 4. Output Files

### output/viz\_altersverteilung.csv


Variable | Beschreibunng
--- | --- 
`year ` | eindeutiger Identifikator
`mean_age ` | Beschreibung der ersten Variable
`age_population` | und so weiter...


### output/viz\_br\_frauenanteil.csv


Variable | Beschreibunng
--- | --- 
`year` | eindeutiger Identifikator
`share_female` | Beschreibung der ersten Variable

### output/viz\_br\_parties.csv


Variable | Beschreibunng
--- | --- 
`year` | eindeutiger Identifikator
`BR_closeness` | Beschreibung der ersten Variable

### output/viz\_br\_social\_mobility.csv


Variable | Beschreibunng
--- | --- 
`year ` | eindeutiger Identifikator
`nr_family ` | Beschreibung der ersten Variable

### output/viz\_kantone\_br\_bars\_online.csv


Variable | Beschreibunng
--- | --- 
`kte_kurz ` | eindeutiger Identifikator
`BR_diff ` | Beschreibung der ersten Variable

### output/viz\_kantone\_br\_bars\_print.csv


Variable | Beschreibunng
--- | --- 
`kte_kurz ` | eindeutiger Identifikator
`BR_diff ` | Beschreibung der ersten Variable
`time_diff ` | und so weiter...

### output/viz\_kantone\_br\_map.csv


Variable | Beschreibunng
--- | --- 
`kte_kurz ` | eindeutiger Identifikator
`Kanton ` | Beschreibung der ersten Variable
`BR_diff ` | und so weiter...
`time_diff ` | und so weiter...

### output/viz\_regions\_br\_bars.csv


Variable | Beschreibunng
--- | --- 
`region ` | eindeutiger Identifikator
`BR_diff ` | Beschreibung der ersten Variable

## 5. Lizenz

*Bundesrat Repraesentation* is free and open source software released under the permissive MIT License.

