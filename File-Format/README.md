# Dateiformate

## Text-basiert oder Binär

Dateiformate können in zwei Kategorien unterteilt werden: textbasierte
und binäre Formate. Textbasierte Formate speichern Daten als lesbaren
Text, der von Menschen gelesen und bearbeitet werden kann. Beispiele für
textbasierte Formate sind Textdateien, Markdown-Dateien und CSV-Dateien.
Binäre Formate speichern Daten als Folge von Nullen und Einsen, die von
Computern gelesen und verarbeitet werden können. Beispiele für binäre
Formate sind Bilddateien, Audiodateien und ausführbare Dateien.

Zum Datenaustausch zwischen verschiedenen Programmen und Plattformen
werden häufig textbasierte Formate verwendet, da sie plattformunabhängig
sind und von den meisten Programmen unterstützt werden. Binäre Formate
werden häufig verwendet, um große Datenmengen effizient zu speichern und
zu übertragen, da sie kompakter sind als textbasierte Formate.

### Texteditor

Ein Texteditor ist ein Programm, das es ermöglicht, (pure) Textdateien
zu erstellen, zu bearbeiten und zu speichern. Texteditoren sind einfache
Programme, die keine Formatierungen oder speziellen Funktionen
unterstützen. Sie werden häufig zum Schreiben von Code, Notizen und
anderen textbasierten Inhalten verwendet.

Grundlegend können sie *jede* Datei mit einem Texteditor öffnen. In der
Regel wird der Texteditor die Datei als Textdatei interpretieren und den
Inhalt (also die Binärinformation) als Text anzeigen. Wenn das
Dateiformat jedoch spezielle Strukturen oder Codierungen enthält, kann
der Texteditor den Inhalt nicht korrekt interpretieren und anzeigen, was
dann wie folgt aussieht.

<figure>
<img
src="https://www.nayuki.io/res/what-are-binary-and-text-files/binary-file-in-text-editor.png"
alt="" />
<figcaption
aria-hidden="true"><img src="https://www.nayuki.io/res/what-are-binary-and-text-files/binary-file-in-text-editor.png" width=300 title="Binärdatei in Texteditor geöffnet"></figcaption>
</figure>

> Über die Gründe wird ausführlich in [diesem
> Artikel](https://www.nayuki.io/page/what-are-binary-and-text-files)
> diskutiert.

Unter Microsoft Windows ist der “Editor” ein einfacher Texteditor, der
mit dem Betriebssystem geliefert wird. Allerdings ist der Editor sehr
einfach und bietet nur sehr begrenzte Funktionen. Wir empfehlen derzeit
(Stand 2024) [unter Microsoft Windows den kostenlosen Texteditor
Notepad++](https://notepad-plus-plus.org/).

[<img src="https://notepad-plus-plus.org/assets/images/notepad4ever.png" width="300" title="Notepad++ Screenshot">](https://notepad-plus-plus.org/assets/images/notepad4ever.png)

Unter macOS ist der “TextEdit” ein einfacher Texteditor, der mit dem
Betriebssystem geliefert wird.

In Linux-Systemen gibt es verschiedene Texteditoren mit grafischer
Benutzeroberfläche wie Gedit, Kate und Geany, sowie Texteditoren für die
Kommandozeile wie Vim und Emacs.

**ACHTUNG** Microsoft Word, Google Docs und andere
Textverarbeitungsprogramme sind keine reinen Texteditoren, da sie
Formatierungen und spezielle Funktionen unterstützen. Diese sind daher
ungeeignet um reine Textdateien zu erstellen oder zu bearbeiten.

### Aufgabe

Speichern sie die Datei [`README.md`](README.md) in einem beliebigen
Ordner auf ihrem Computer. Öffnen sie die heruntergeladene Datei
`README.md` in einem Texteditor und betrachten Sie den Inhalt. Handelt
es sich bei der Datei um ein textbasiertes oder binäres Dateiformat?

<details>
<summary>
Lösung
</summary>

> `.md` ist die Dateiendung für Markdown-Dateien, die ein textbasiertes
> Dateiformat sind. Die Datei `README.md` kann in einem Texteditor
> geöffnet und bearbeitet werden. Details zur Markdown-Syntax werden
> später weiter unten diskutiert.

</details>

Im Folgenden werden einige häufig verwendete textbasierte Dateiformate
und ihre Verwendungszwecke beschrieben.

## Speichern von Notizen, Metainformation, …

### MD - Markdown

Markdown ist ein einfaches Auszeichnungssprache, die es ermöglicht,
Texte mit einfachen Formatierungen zu versehen. Es ist leicht zu lesen
und zu schreiben und wird häufig in der Softwareentwicklung und im
Webdesign verwendet. Markdown-Dateien haben die Endung `.md` und können
in Texteditoren oder speziellen Markdown-Editoren geöffnet und
bearbeitet werden.

Der Vorteil von Markdown ist, dass es einfach zu lesen und zu schreiben
ist und dass es in fast allen Texteditoren und Webanwendungen
unterstützt wird. Markdown-Dateien können in HTML, PDF oder anderen
Formaten exportiert werden, um sie mit anderen zu teilen oder zu
veröffentlichen.

## Speichern von Daten

### CSV - Comma Separated Values

CSV steht für “Comma Separated Values” und ist ein einfaches
Dateiformat, das Tabellenstrukturen speichert. Jede Zeile der Datei
entspricht einer Zeile der Tabelle, und die Werte in den Spalten sind
durch ein Trennzeichen getrennt. Das Trennzeichen ist in der Regel ein
Komma, aber es können auch andere Zeichen wie Semikolons oder Tabs
verwendet werden. CSV-Dateien können in Texteditoren oder
Tabellenkalkulationsprogrammen wie Excel geöffnet und bearbeitet werden.

### JSON - JavaScript Object Notation

JSON steht für “JavaScript Object Notation” und ist ein
leichtgewichtiges Datenaustauschformat. Es ist einfach zu lesen und zu
schreiben und wird häufig in Webanwendungen verwendet, um Daten zwischen
Servern und Clients auszutauschen. JSON-Daten bestehen aus
Schlüssel-Wert-Paaren, die in geschweiften Klammern eingeschlossen sind.
Die Schlüssel und Werte sind durch Doppelpunken getrennt, und die Paare
sind durch Kommas voneinander getrennt.

------------------------------------------------------------------------

Dieses Dokument wurde mit Unterstützung von GitHub Copilot erstellt,
einem KI-gestützten Autocompletion-Tool, das auf der OpenAI
GPT-3-Technologie basiert.
