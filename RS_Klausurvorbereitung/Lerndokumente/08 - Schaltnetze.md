[[#Überblick und Ressourcen|Zum Überblick]]

>[!target]- Prüfungsrelevante Inhalte
>- Schaltnetz (SN)
>	- Begriffe (z.B. Eingangsvektor, Eingangsbelegung), Konventionen, verbotene Eingangsbelegungen
>	- Tabellendarstellung, "don't care"
>- Aufbau aus Gattern
>	- Gegebenes SN lesen können
>- Gatter: Für eigenen Lösungen ISO-Darstellungen
>	- dt. und US Darstellung lesen können
>- Halbaddierer, Volladdierer
>- Begriffe beherrschen, z.B. Elementarkonjunktion, ...
>- Schaltnetzentwurf
>	- Struktureller Entwurf
>	- Systematisches Vorgehen Schaltnetzentwurf
>		- Tabellendarstellung, "don't care"
>		- Minimieren mit KV
>		- Funktion des SN gegeben in verschiedenen Formen
>			- ON(f), OFF(f), Text, Boolescher Ausdruck, ...
>	- Darstellungen
>		- kDNF, DNF, (kKNF, KNF)
>	- Rechnen mit Booleschen Ausdrücken, z.B. zum Minimieren
>- Strukturbeschreibung
>	- Kopplung von Modulen
>	- Blockbildung / Parallelinstranziierung
>	- Kaskadierung
>	- Rechnen mit Schaltnetzen
>		- Halb- und Volladdierer, Multiplizierer
>	- Multiplexer
>	- SN lesen, verstehen und ggf. erweitern können
>
>---
>(Siehe Foliensatz 14 - Zusammenfassung)

Implementierung digitaler Schaltungen, die durch Boolesche Funktionen beschrieben sind.

---
## Schaltnetz

Ein *Schaltnetz* bezeichnet ein Netz aus elementaren logischen Schaltgliedern ([[#Gatter|Gattern]]), das analytisch mit Hilfe der Booleschen Algebra untersucht werden kann. Das Schaltnetz stellt also die Realisierung einer Booleschen Funktion dar.

### Schaltalgebra

Die Anwendung der Booleschen Algebra für den Schaltnetzentwurf bezeichnet man als *Schaltalgebra*.

Es dürfen alle Booleschen Operationen verwendet werden, doch aufgrund der Herstellungstechnik für Halbleiter wird meist nur $\neg,\wedge,\vee$ genutzt.

>[!info] Eingangsvektoren
>Die Elemente der Urbildmenge $\mathbb B^n$ werden auch als *Eingangsvektoren* $\text{X}=(x_{n-1},\dots,x_0)$ bezeichnet.

>[!info] Eingangsbelegung
>Eine *Belegung des Eingangsvektors $\text{X}$* (kurz *Eingangsbelegung*) ist eine Kombination von Werten der Bits (aus $\mathbb B$) für alle Komponenten $x_i$.

Belegungen, die nicht in $\text{DEF}(f)$ liegen heißen *verbotene Eingangsbelegungen*. Da sie im Betrieb nicht auftreten sollten, ist die Ausgabe dieser frei wählbar. In der Wahrheitstabelle können sie mit "Don't Care" (\*) markiert werden.

### Tabelle

>[!example] Beispiel | Wertetabelle und Begriffe
>Die *Eingangsbelegung* für bspw. $i=1$ ist $\text{X}_1=(0,0,1)$.
>
>Bei Index $6,7$ handelt es sich um *verbotene Eingangsbelegungen*. Ihre Ausgaben sind mit '\*' ("Don't Care") markiert.
>
>| $i$ | $x_2$ | $x_1$ | $x_0$ | $y_1$ | $y_2$ |
>| :---: | :-----: | :-----: | :-----: | :-----: | :-----: |
>| $0$ | $0$   | $0$   | $0$   | $1$   | $1$   |
>| $1$ | $0$   | $0$   | $1$   | $0$   | $0$   |
>| $2$ | $0$   | $1$   | $0$   | $0$   | $1$   |
>| $3$ | $0$   | $1$   | $1$   | $1$   | $0$   |
>| $4$ | $1$   | $0$   | $0$   | $1$   | $1$   |
>| $5$ | $1$   | $0$   | $1$   | $0$   | $1$   |
>| $6$ | $1$   | $1$   | $0$   | \*    | \*    |
>| $7$ | $1$   | $1$   | $1$   | \*    | \*    |
>
>---
>$i$ - Index
>$x$ - Elemente der Eingangsvektoren
>$y$ - Elemente der Ausgabevektoren
>

#todo Blockbildung / Parallelinstranziierung & Kaskadierung

---
## Gatter

Schaltnetze sind aus *Gattern* zusammengesetzt.

Gattersymbole nach ISO:

![[gatter.png]]

*Für die Klausur wird eine Tabelle der obigen Gatter bereitgestellt. Das Dokument ist im [Lernraum](https://lernraum.th-luebeck.de/course/section.php?id=73536) abrufbar.*

>[!info]- US Gattersymbole
>![[gatter_us.png]]

>[!example]- Beispiel | Schaltnetz
>Zum Lesen eines Schaltnetzes:
>
>- Von Eingängen zu Ausgängen verfolgen.
>- Logische Verknüpfung jeder "Stufe" bestimmen.
>- Gesamtfunktion durch sukzessive Ableitung bestimmen.
>
>#todo Beispiel-Schaltnetz

---
## Schaltnetzentwurf

Dieser Abschnitt behandelt alles rund um den Schaltnetzentwurf, darunter Begriffe, [[#Schaltalgebraische Darstellungen]], [[#Vorgehen]] und [[#Minimierung|Minimierung mit KV-Diagramm]].

Wichtige Begriffe zum Schaltnetzentwurf:

- $\text{ON}(f)$ - Menge aller Eingangsvektoren, wo  $f=1$
- $\text{OFF}(f)$ - Menge aller Eingangsvektoren, wo $f=0$
- $\text{DC}(f)$ - Don't-Care-Menge (frei wählbar)
- Die Konjunktion ($\wedge$) aller (ggf. negierten) Eingangsvariablen ($x_{n-1},\dots,x_0$) nennt man *Elementarkonjunktion $k_i$* (auch: *Minterm*).
	- Z.B.: $k_3=\overline{x_2}\wedge x_1\wedge x_0$

### Schaltalgebraische Darstellungen

Es gibt verschiedene Darstellungsmöglichkeiten von einer Tabelle zum Schaltalgebraischen Ausdruck.

>[!info] Disjunkte Normalform (DNF)
>Ein Ausdruck der booleschen Algebra ist in  *disjunkter Normalform*, wenn dieser nur aus Disjunktionen von Konjunktionen besteht, also: $$\bigvee_{i=1}^m \bigwedge_{j=1}^m L_{ij}$$ Wobei $L_{ij}$ Literale sind.
>
>>[!example]- Beispiel
>>$$(x_2 \wedge x_1 \wedge \overline{x_0}) \vee (x_2 \wedge x_0)$$

>[!info] Kanonische Disjunkte Normalform (kDNF)
>Die *kanonische Disjunkte Normalform* bildet sich aus der Disjunktion aller Elementarkonjunktionen $k_i$, die in $\text{ON}(f)$ liegen. $$y=\bigvee_{i\in\text{ON}(f)}k_i$$
>
>>[!example]- Beispiel
>>Man nehme die nachfolgende Wertetabelle an:
>>
>>| $i$ | $x_2$ | $x_1$ | $x_0$ | $y$ |
>>| :-: | :---: | :---: | :---: | :-: |
>>| $0$ |  $0$  |  $0$  |  $0$  | $0$ |
>>| $1$ |  $0$  |  $0$  |  $1$  | $0$ |
>>| $2$ |  $0$  |  $1$  |  $0$  | $0$ |
>>| $3$ |  $0$  |  $1$  |  $1$  | $1$ |
>>| $4$ |  $1$  |  $0$  |  $0$  | $0$ |
>>| $5$ |  $1$  |  $0$  |  $1$  | $1$ |
>>| $6$ |  $1$  |  $1$  |  $0$  | $1$ |
>>| $7$ |  $1$  |  $1$  |  $1$  | $1$ |
>>
>>Die *kDNF* hat dann die Form $$(\overline{x_2} \wedge x_1 \wedge x_0) \vee (x_2 \wedge \overline{x_1} \wedge x_0) \vee (x_2 \wedge x_1 \wedge \overline{x_0}) \vee (x_2 \wedge x_1 \wedge x_0).$$

>[!sparkles]- Extra: KNF und kKNF
>>[!info] Konjunktive Normalform (KNF)
>>Ein Ausdruck der booleschen Algebra ist in *konjunktiver Normalform*, wenn dieser nur aus Konjunktionen von Disjunktionen besteht, also $$\bigwedge_{i=1}^n \bigvee_{j=1}^m L_{ij}$$ hat, wobei $L_{ij}$ Literale sind.
>>>[!example]- Beispiel
>>>$$(x_2 \vee x_1 \vee \overline{x_0}) \wedge (x_2 \vee x_0)$$
>
>>[!info] Kanonische Konjunktive Normalform (kKNF)
>>Die *kanonische konjunktive Normalform* bildet sich aus der Konjunktion aller Elementardisjunktionen $d_i$ (Eingangsvariablen invertiert), die in $\text{OFF}(f)$ liegen. $$y=\bigwedge_{i\in\text{OFF}(f)}d_i$$
>>>[!example]- Beispiel
>>>Man nehme die nachfolgende Wertetabelle an:
>>>
>>>| $i$ | $x_2$ | $x_1$ | $x_0$ | $y$ |
>>>| :-: | :---: | :---: | :---: | :-: |
>>>| $0$ |  $0$  |  $0$  |  $0$  | $0$ |
>>>| $1$ |  $0$  |  $0$  |  $1$  | $0$ |
>>>| $2$ |  $0$  |  $1$  |  $0$  | $0$ |
>>>| $3$ |  $0$  |  $1$  |  $1$  | $1$ |
>>>| $4$ |  $1$  |  $0$  |  $0$  | $0$ |
>>>| $5$ |  $1$  |  $0$  |  $1$  | $1$ |
>>>| $6$ |  $1$  |  $1$  |  $0$  | $1$ |
>>>| $7$ |  $1$  |  $1$  |  $1$  | $1$ |
>>>
>>>Die *kKNF* hat dann die Form $$(x_2 \vee x_1 \vee x_0) \wedge (x_2 \vee x_1 \vee \overline{x_0}) \wedge (x_2 \vee \overline{x_1} \vee x_0) \wedge (\overline{x_2} \vee x_1 \vee x_0).$$
### Vorgehen

1. (Verbale) Beschreibung der Funktion
2. Darstellen als [[#Schaltalgebra|Schaltalgebraischer]] Ausdruck
3. Darstellen als [[#Tabelle|Tabelle]]
4. [[#Minimierung|Minimieren]] des Ausdrucks
5. Aufbau des minimierten Ausdrucks als 2-stufitges Schaltnetz

#### Minimierung

Beim Erstellen des Schaltnetzes ist es nicht unwahrscheinlich den Schaltalgebraischen Ausdruck bzw. das Schaltnetz *minimieren* zu können, um Gatter einzusparen. Das hat Auswirkung auf den Platz- und somit auch den Zeitbedarf eines Programms.

Ein boolescher Ausdruck in DNF, der nicht weiter vereinfacht werden kann, bezeichnet man als *Minimalpolynom*.

Es gibt verschiedene Verfahren zum minimieren. Die algebraische und algorithmische Verfahren sind nicht klausurrelevant und werden hier entsprechend nicht behandelt.
##### Graphische Minimierung: KV-Diagramm

Das *KV-Diagramm* dient zur einfachen Minimierung von Termen mit bis zu $4$ Eingangsvariablen; darüber hinaus wird es dreidimensional.

Das KV-Diagramm hat die folgende Form:

![[kv_diagram.png]]

- Die Variablen können in einer beliebigen Reihenfolge sein. *In diesem Modul gilt jedoch:*
	1. Horizontal;
	2. Vertikal;
	3. Bei weiteren Variablen: Spiegel die entsprechende Achse und wiederhole.
- Die *orangenen* Zahlen sind der Index der jeweiligen Elementarkonjunktion $k$.

Benachbarte Felder können zusammengefasst werden, da sich die Terme nur in der Belegung einer einzelnen Variable unterscheiden. Diese Variable $x_i$ ist somit überflüssig, da bei $x_i$ und $\overline x_i$ der Ausgang gleich ist. Z.B. $k_3\vee k_7=(\overline x_3\wedge\overline x_2\wedge x_1\wedge x_0)\vee(\overline x_3\wedge x_2\wedge x_1\wedge x_0)\Rightarrow\overline x_3\wedge x_1\wedge x_0$
Es können auch gleich $4$, $8$ Felder zusammengefasst werden und das Gruppieren ist über den Rand hinweg möglich (z.B. $4$ und $0$ oder $1,5,9$ und $13$).

Da wir die kDNF nutzen, um $\text{ON}(f)$ widerzuspiegeln, werden alle $1$-en gruppiert, um ein Minimalpolynom in DNF zu bilden.

Die einzelnen Teilterme der Gruppierungen werden konjungiert um das Minimalpolynom zu erhalten.

*Schrittweises Vorgehen:*

1. Wertetabelle bereithalten.
2. KV-Diagramm zeichnen unter Beachtung der Eingangsvariablenanzahl.
3. Für alle $i\in\text{ON}(f)$ im entsprechendem Feld des KV-Diagrams $1$ einzeichnen. Verbleibende Felder sind $0$.
4. Gruppierung aller $1$-en.
5. Bilde aus den Gruppen die Teilterme für das Minimalpolynom in DNF.
6. Bilde aus den Teiltermen das Minimalpolynom in DNF.

Schritt 3. kann auch invertiert werden: Für alle $i\in\text{OFF}(f)$ im entsprechendem Feld des KV-Diagramms $0$ einzeichnen. Die verbleibenden Felder sind dann $1$. Wähle die Variante, die mit weniger Aufwand verbunden ist.

>[!example] Beispiel | Minimierung mit KV

---

#todo [[!Begriffe#^multiplexer|multiplexer]]

---
## Überblick und Ressourcen

>[!tldr] tl;dr
>#todo
>^tldr

>[!link] Hilfreiche Links
>\-

>[!source] Quellen
>- RS Foliensatz 8 - Schaltnetze
>^sources
