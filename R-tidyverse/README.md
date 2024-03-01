# Datenanalyse mit R und tidyverse

Im Folgenden werden einige Möglichkeiten eingeführt, wie Datenanalyse
und -visualisierung mit R und dem tidyverse durchgeführt werden können.
Hierbei werden grundlegende Kenntnisse von R vorausgesetzt. Das Ziel
diese Tutorials ist es, R NutzerInnen ohne tidyverse Kenntnisse einen
Einstieg und allen mit tidyverse vertrauten eine Zusammenfassung zu
geben.

Folgende Installationen werden benötigt:

-   R version 4.2.0 oder neuer
-   `tidyverse` packages via
    `install.packages(c("tidyverse", "readxl", "writexl"))`
    -   `magrittr` -
        [Cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/magrittr.pdf)
    -   `readr`, `readxl`, `writexl` -
        [Cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/data-import.pdf)
    -   `dplyr` -
        [Cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/data-transformation.pdf)
    -   `stringr` -
        [Cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/strings.pdf)
    -   `tidyr` -
        [Cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/data-import.pdf)
    -   `ggplot2` -
        [Cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/data-visualization-2.1.pdf)

Alle Codebeispiele können in RStudio ausgeführt werden, wenn zuvor
`tidyverse` geladen wurde. Zum Beispiel via `library(tidyverse)`.

Als zusätzliche Lektüre und für einen detaillierten Einstieg im
Selbststudium empfehlen wir das frei verfügbare Buch [R for Data
Science](https://r4ds.hadley.nz/).

## Datenstrukturen

Für die Verarbeitung von tabellarischen Daten werden in R i.d.R.
`data.frame`s verwendet. Das `tidyverse` package liefert eine erweiterte
Version des `data.frame`s, das `tibble`, welches etwas transparenter in
seiner Verwendung ist. In einem `tibble` (oder `data.frame`) entspricht
jede Zeile einem Datensatz (oder einer Beobachtung) und jede Spalte
einer Variable (oder einem Merkmal) dieses Datensatzes. Damit haben alle
Daten in der gleichen Spalte den gleichen Datentyp, z.B. “Zahl”
(`numeric`), “Kommazahl” (`double`), “Ganzzahl” (`integer`), “Text”
(`character`), “Datum” (`date`), etc. Im Folgenden wird der
[Beispieldatensatz
`storms`](https://dplyr.tidyverse.org/reference/storms.html) aus dem
`dplyr` package gezeigt.

    dplyr::storms

    ## # A tibble: 19,066 × 13
    ##    name   year month   day  hour   lat  long status      category  wind pressure
    ##    <chr> <dbl> <dbl> <int> <dbl> <dbl> <dbl> <fct>          <dbl> <int>    <int>
    ##  1 Amy    1975     6    27     0  27.5 -79   tropical d…       NA    25     1013
    ##  2 Amy    1975     6    27     6  28.5 -79   tropical d…       NA    25     1013
    ##  3 Amy    1975     6    27    12  29.5 -79   tropical d…       NA    25     1013
    ##  4 Amy    1975     6    27    18  30.5 -79   tropical d…       NA    25     1013
    ##  5 Amy    1975     6    28     0  31.5 -78.8 tropical d…       NA    25     1012
    ##  6 Amy    1975     6    28     6  32.4 -78.7 tropical d…       NA    25     1012
    ##  7 Amy    1975     6    28    12  33.3 -78   tropical d…       NA    25     1011
    ##  8 Amy    1975     6    28    18  34   -77   tropical d…       NA    30     1006
    ##  9 Amy    1975     6    29     0  34.4 -75.8 tropical s…       NA    35     1004
    ## 10 Amy    1975     6    29     6  34   -74.8 tropical s…       NA    40     1002
    ## # ℹ 19,056 more rows
    ## # ℹ 2 more variables: tropicalstorm_force_diameter <int>,
    ## #   hurricane_force_diameter <int>

Bei der Verwendung von `tibble`s sind unter den Spaltennamen die
Datentypen der Spalten abgekürzt dargestellt.

Ziel der Datenverarbeitung ist es, die Daten so zu transformieren, dass
sie für die Analyse und Visualisierung geeignet sind und ein Format wie
oben gezeigt vorweisen. Wenn das der Fall ist, sprich

-   jede Zeile entspricht einem Datensatz und
-   jede Spalte entspricht einer Variable,

wird der Datensatz als “tidy” bezeichnet.

## Tabellendaten von Dateien einlesen und in Dateien schreiben/exportieren

In R können Daten aus verschiedenen Quellen und von verschiedenen Orten
eingelesen werden.

Die gängigsten Quellen sind:

-   Textdateien (z.B. `.csv`, `.tsv`, `.txt`)
-   Excel-Dateien (z.B. `.xlsx`, `.xls`)
-   Datenbanken (z.B. `MySQL`, `PostgreSQL`, `SQLite`)

Die gängigsten Orte sind:

-   lokale Dateien
-   URLs, also direkter Datenimport aus dem Internet oder lokalem
    Netzwerk

Im Folgenden einige Beispiele zum Einlesen von Daten in R.

    library(readr)
    # CSV aus dem Internet
    read_csv("https://raw.githubusercontent.com/tidyverse/dplyr/master/data-raw/storms.csv")

    # lokale Excel-Datei
    readxl::read_xlsx("storms-2019-2021.xlsx", 
                      sheet = "storms-2020") # explizite Angabe des Tabellenblatts

    # lokale CSV Datei Semikolon getrennt (";") und mit westeuropäischem Zahlenformat ("," als Dezimaltrenner)
    read_csv2("storms-2019-2021.csv")

    # explizite Einstellung des Datenformats
    read_delim(
      "storms-2019-2021.csv", 
      delim = ";", # Spaltentrenner
      locale = locale( # zusätzliche Einstellungen wie gespeicherte Informationen kodiert sind
        decimal_mark = ",", # Dezimaltrenner
        grouping_mark = ".", # Tausendertrenner
        encoding = "latin1" # (alte) westeuropäisches Buchstabenkodierung (z.B. Umlaute)
        )
      )

Das Schreiben von Dateien erfolgt analog, indem einfach `write_`
anstelle von `read_` verwendet wird.

## Tabellen transformieren

Die Transformation von Daten erfolgt i.d.R. mittels des `dplyr`
packages.

*Grundlegend gilt: das erste Argument einer Funktion ist immer der
Datensatz!*

Innerhalb von `dplyr` Funktionen können *Spaltennamen ohne
Anführungzeichen* (quoting) verwendet werden.

Basistransformationen sind:

-   Filtern von Zeilen mit gegebenen Kriterien (formulieren was man
    BEHALTEN will!)
    -   `filter(storms, year == 2020)` = alle Sturmdaten aus dem Jahr
        2020
    -   `filter(storms, year == 2020 & month == 6)` = alle Sturmdaten
        aus dem Juni 2020
    -   `filter(storms, !is.na(category))` = alle Sturmdaten, bei denen
        die Kategorie bekannt ist
-   Sortieren von Zeilen
    -   `arrange(storms, year)` = Sturmdaten nach Jahr aufsteigend
        sortieren
    -   `arrange(storms, year, desc(month))` = Sturmdaten aufsteigend
        nach Jahr sortieren und innerhalb eines Jahres absteigend nach
        Monat
-   Duplikate entfernen
    -   `distinct(storms)` = alle Zeilen mit identischen Werten in allen
        Spalten entfernen
    -   `distinct(storms, year, month, day)` = alle Zeilen mit gleichen
        Werten in den Spalten `year`, `month` und `day` entfernen
        (reduziert die Spalten auf die Ausgewählten)
    -   `distinct(storms, year, month, day, .keep_all = TRUE)` = alle
        Zeilen mit gleichen Werten in den Spalten `year`, `month` und
        `day` entfernen, aber *alle Spalten behalten*
-   Auswählen/Entfernen von Spalten
    -   `select(storms, name, year, month, day)` = nur Spalten mit
        Zeitinformation und Namen der Stürme behalten
    -   `select(storms, -year, -month, -day)` = Spalte mit
        Zeitinformation entfernen
-   Umbenennen von Spalten
    -   `rename(storms, sturmname = name)` = Spalte `name` in
        `sturmname` umbenennen
-   Zusammenfassen von Daten: nur eine Zeile mit aggregierten
    Informationen (z.B. Mittelwert, Summe, Anzahl, etc.) pro Gruppe
    -   `summarize(storms, max_wind = max(wind), num_datasets = n())` =
        maximale Windgeschwindigkeit und Anzahl der Datensätze (Zeilen)
-   Gruppierung von Daten = “Zerlegung” des Datensatzes in Teiltabellen,
    für die anschliessende Arbeitsschritte unabängig voneinander
    durchgeführt werden. Wird i.d.R. verwendet, wenn die Aufgabe “pro …”
    oder “für jede …” lautet.
    -   `group_by(storms, year)` = Gruppierung der Sturmdaten nach Jahr
        (aber noch keine Aggregation!)
    -   `group_by(storms, year) |>  summarize(max_wind = max(wind))` =
        maximale Windgeschwindigkeit *pro Jahr* (eine “summarize” Zeile
        pro Teiltabelle = Gruppe = Jahr)
    -   `group_by(storms, year) |> filter(wind == max(wind)) |> ungroup()`
        = alle Sturmdaten, bei denen die maximale Windgeschwindigkeit
        *pro Jahr* erreicht wurde (keine Zusammenfassung!)
    -   Grouping ist ein extrem mächtiges Werkzeug, das in vielen
        Situationen verwendet wird, um Daten zu transformieren.
        Allerdings braucht es etwas Übung, um zu verstehen, wie es
        funktioniert.
-   Spalten hinzufügen/ausrechnen oder bestehende Spalten verändern
    (z.B. Einheiten umrechnen)
    -   `mutate(storms, wind_kmh = wind * 1.60934)` =
        Windgeschwindigkeit in km/h berechnen und als *neue Spalte
        hinzufügen*
    -   `mutate(storms, wind = wind * 1.60934)` = Windgeschwindigkeit in
        km/h umrechnen und *bestehende Spalte überschreiben*
    -   `mutate(storms, wind_kmh = wind * 1.60934, wind_kmh_rounded = round(wind_kmh, 1))`
        = es können auch mehrere Spalten auf einmal berechnet werden und
        dabei direkt neue angelegte Spalten in anschliessenden Formeln
        verwendet werden (hier Runden auf eine Nachkommastelle)

Details und weitere Funktionen und Beispiele sind im [`dplyr`
Cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/data-transformation.pdf)
zusammengefasst.

## Workflows mittels Piping

Seit R 4.1.0 ist der Pipe-Operator `|>` standardmäßig in R enthalten.
Alternativ bietet das `magrittr` package den Pipe-Operator `%>%`,
welcher eine etwas umfangreichere Funktionalität bietet. Für die meisten
Anwendungen ist der Standard-Pipe-Operator `|>` ausreichend und
äquivalent zu `%>%` verwendbar.

Der Pipe-Operator ist ein nützliches Werkzeug, um den Code lesbarer zu
machen und die Arbeitsschritte in einer logischen Reihenfolge zu
verketten. Hierbei wird das Ergebnis des vorherigen Arbeitsschrittes als
erstes Argument des nächsten Arbeitsschrittes verwendet. Da das erste
Argument von (den meisten) Funktionen der Datensatz ist, ermöglicht dies
die Verknüpfung von Arbeitsschritten zu einem Workflow ohne
Zwischenergebnisse speichern zu müssen oder Funktionsaufrufe zu
verschachteln.

Zum Beispiel:

    # Beispiel: maximale Windgeschwindigkeit pro Monat im Jahr 2020

    # geschachtelte Schreibweise = schwer lesbar, da von "innen nach aussen" gelesen werden muss
    summarize( group_by( filter(storms, year == 2020), month), max_wind = max(wind))

    # mit temporären Variablen (die i.d.R. nicht wieder verwendet werden...!)
    storms_2020 <- filter(storms, year == 2020)
    storms_2020_monthly <- group_by(storms_2020, month)
    summarize(storms_2020_monthly, max_wind = max(wind))

    # Workflow mit Pipe-Operator = einfach lesbar und erweiterbar  *thumbs-up*
    storms |> # Datensatz
      filter(year == 2020) |> # Zeilenauswahl
      group_by(month) |> # Gruppierung
      summarize(max_wind = max(wind)) # Zusammenfassung

Pipe-basierte workflows sind …

-   einfach lesbar, da sie der normalen Leserichtung entsprechen.
-   reduzieren die Anzahl der temporären Variablen, die im globalen
    Workspace herumliegen und die Lesbarkeit des Codes beeinträchtigen.
-   einfach zu erweitern, da neue Arbeitsschritte einfach an das Ende
    der Kette angehängt werden können (z.B. `write_csv("bla.csv")` oder
    bestehende Arbeitsschritte ausgetauscht werden können.
-   einfach zu debuggen, da Zwischenergebnisse einfach ausgegeben werden
    können (einfach `view()` oder `print()` an das Ende der
    entsprechenden Zeile anhängen).
-   einfach zu wiederzuverwenden, da der gesamte Workflow in einer Zeile
    zusammengefasst ist und immer als Block aufgerufen wird. Dadurch
    können keine Zwischenschritte vergessen werden und der Workflow ist
    immer konsistent.

*Wichtig:* R Kommandos können über mehrere Zeilen verteilt werden, wie
im Beispiel zu sehen ist, was die Übersichtlichkeit des Codes erhöht.
Hierzu wird z.B. der Pipe-Operator `|>` am Ende der Zeile geschrieben
und der nächste Arbeitsschritt in der nächsten Zeile fortgesetzt.
Gleiches gilt für jeden Operator (`+`, `==`, `&`, ..) sowie
unvollständige Funktionsaufrufe, bei denen die Klammerung noch nicht
geschlossen ist (d.h. schließende Klammer wird in der nächsten oder
einer späteren Zeile geschrieben).

## Textdaten verändern und verwenden

Um Textdaten (*Strings*) zu verändern, gibt es verschiedene Funktionen
des `stringr` Paketes, die in Kombination mit `mutate()` oder anderen
Funktionen verwendet werden können. Die meisten Funktionen des `stringr`
Paketes sind sehr intuitiv und haben eine ähnliche Syntax wie die
Funktionen des `dplyr` Paketes. Zudem sind viele mit regulären
Ausdrücken verwendbar, um Textdaten aufgrund von allgemeineren
Textmustern zu erkennen und zu verändern. Alle Funktionen des `stringr`
Paketes beginnen mit `str_` und sind in der
[Dokumentation](https://stringr.tidyverse.org/reference/index.html)
aufgeführt. Einige wichtige sind:

-   `str_c()`: Verkettet mehrere Strings zu einem
-   `str_detect()`: Prüft, ob ein String einen bestimmten Textteil
    enthält
-   `str_replace()`: Ersetzt einen Teil eines Strings durch einen
    anderen
-   `str_to_lower()`/`str_to_upper`: Wandelt alle Buchstaben in
    Klein-/Grossbuchstaben um
-   `str_sub()`: Extrahiert einen Teil eines Strings
-   `str_trim()`: Entfernt Leerzeichen am Anfang und Ende eines Strings
-   `str_extract()`: Extrahiert einen Teil eines Strings, der einem
    bestimmten Muster entspricht
-   `str_remove()`: Entfernt einen Teil eines Strings, der einem
    bestimmten Muster entspricht
-   `str_split()`: Teilt einen String an einem bestimmten Trennzeichen
    auf

Die meisten Funktionen liefern nur einen Treffer oder verändern nur den
ersten Treffer. Daher gibt es von vielen Funktionen Varianten, die alle
Treffer finden und/oder verarbeiten, z.B. `str_detect_all()`,
`str_replace_all()`, `str_extract_all()`.

Die Funktionen sind im [`stringr`
Cheatsheet](https://raw.githubusercontent.com/rstudio/cheatsheets/master/strings.pdf)
zusammengefasst.

Beispiele für deren Verwendung mit `mutate()` und Co. sind:

    # Beispiel: Grossbuchstaben in Spalte "name" in Kleinbuchstaben umwandeln 
    # (und nur eindeutige Einträge in Spalte "name" anzeigen)
    mutate(storms, name = str_to_lower(name)) |> distinct(name)
    # Beispiel: Jahrhundert aus Spalte "year" extrahieren
    mutate(storms, century = str_sub(year, 1, 2)) |> distinct(name, century)
     # oder via regulärem Ausdruck
    mutate(storms, century = str_extract(year, "^\\d{2}"))
    mutate(storms, century = str_remove(year, "..$"))
    # Beispiel: Nur Stürme mit "storm" im Status behalten
    filter(storms, str_detect(status, "storm")) |> distinct(name)

Beachte:

1.  wenn die (Daten)Eingabe einer `stringr` Funktion ein *Vektor* ist,
    wird die Funktion auf jedes Element des Vektors angewendet und gibt
    einen Vektor mit den Ergebnissen zurück. (= *vektorisierte
    Prozessierung* = zentrales Verarbeitungsprinzip in R)
2.  wenn die Eingabe *kein* String ist (z.B. eine Zahl), wird die
    Eingabe in einen String umgewandelt und die Funktion auf den
    entstandenen String angewendet. (= *automatische Typumwandlung*,
    sogenanntes *coercion* in R)

## Daten visualisieren