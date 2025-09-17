[[#Überblick und Ressourcen|Zum Überblick]]

>[!target]- Prüfungsrelevante Inhalte
>- Definitionen
>	- Kennen und Begriffe korrekt verwenden können
>	- Inhaltlich wiedergeben können (exakter Wortlaut nicht nötig, solange inhaltlich korrekt)
>- Stellenwertsystem
>- Zahlendarstellungen
>	- Festkommazahl
>	- Negative Zahlen:
>		- Vorzeichen + Betrag, Komplementdarstellungen
>		- Exzesscodierung
>	- Gleitkommadarstellung (Mantisse, Exponent, IEEE-Darstellung, Normalisierung)
>- Eigenschaften (Vor-, Nachteile), damit rechnen und umgehen können
>
>---
>(Siehe Foliensatz 14 - Zusammenfassung)

Information und Zahlendarstellung.

---
## Definitionen

### Information in Digitalrechnern

>[!info] Bit
>Ein *Bit* ist eine Elementarinformation in Form einer Ziffer, die den Wert `1` oder `0` annehmen kann.
>
>---
>$8$ Bit sind $1$ Byte.

Basierend auf den 16-Bit Architekturen haben sich Namen für größere Informationen etabliert. Beim RISC-V übliche Begriffe:

- *Word*: $32$ Bit
- *Half word*: $16$ Bit
- *Byte*: $8$ Bit

Bei der Darstellung von Information spricht man von *Codierungen*.

>[!info] Codierung
>Als *Codierung* wird die Belegung eines Zeichens oder einer Zeichenfolge mit einer Bedeutung definiert.
>>[!example] Beispiele
>>- Zahlen: $0,23,42$ (Dezimalsystem)
>>- Buchstaben: A, B, c, d, ...
>>- Wörter: Haus, Auto, Tür
>>- *Bitfolgen*: `01010010100`, `101000100001`

Um eine Zeichenfolge zu interpretieren benötigt man Kenntnis der verwendeten Codierung. Z.B. kann `101` verschieden interpretiert werden:

- Binärsystem: $5$
- Dezimalsystem: $101$
- Text: Albumtitel
- ...

---
## Stellenwertsystem

Die Repräsentation von Zahlen ist eine zentrale Eigenschaft von Digitalrechnern. Während man historisch das wenig flexible [Additionssystem](https://de.wikipedia.org/wiki/Additionssystem) verwendete, nutzt man heute allgemein das *Stellenwertsystem*, welches die Beschreibung komplexer Operationen ermöglicht.

>[!idea] Idee: Stellenwertsysteme
>Die Wertigkeit einer Ziffer hängt von ihrer Stelle (Position) in der Zahl ab.
>
>Die Basis des Zahlensystems definiert
>
>- die Anzahl der Ziffernwerte;
>- die Wertigkeit der Stellen

>[!info] Stellenwertsysteme
>Ein *Stellenwertsystem* ist ein Tripel $S=(b,Z,\delta)$ mit
>
>- $b\in\mathbb N,b\geq2$, die Basis des Stellenwertsystems;
>- $Z$ ist eine Menge von Symbolen (auch: Ziffern) mit $|Z|=b$;
>- $\delta:Z\to\{0,1,\dots,b-1\}$ eine Abbildung, die jeder Ziffer umkehrbar eindeutig eine natürliche Zahl zwischen $0$ und $b-1$ zuordnet.

Einige wichtige Stellenwertsysteme sind

- *Dezimalsystem*;
- *Binärsystem*:
	- Basis $2$, Ziffern: $\{0,1\}$;
- *Oktalsystem*:
	- Basis $8$, Ziffern: $\{0,1,\dots,6,7\}$,
	- $3$ Stellen im Binärsystem als $1$ Ziffer oktal darstellbar;
- *Hexadezimalsystem*:
	- Basis $16$, Ziffern $\{0,1,\dots,9,A,B,C,D,E,F\}$,
	- $4$ Stellen in Binärsystem als $1$ Hexadezimal-Ziffer,
	- Ein Byte immer mit $2$ Stellen dargestellt.

---
## Zahlendarstellungen

Die Darstellung natürlicher Zahlen ist nicht ausreichend. Es werden Brüche (Gleitkommadarstellung) und negative Zahlen (Komplementdarstellung) benötigt.

*Im Weiteren wird dies auf das Binärsystem bezogen.*

### Festkommazahl

>[!info]- Festkommazahl (nicht-negativ)
>Es gibt eine feste Position des Dezimalkommas mit
>
>- $n$ Vorkommastellen;
>- $k$ Nachkommastellen.
>
>Insgesamt hat die Ziffernfolge die Länge $d=n+k$:
>$$d:=d_{n-1}d_{n-2}\dots d_1d_0,d_{-1}\dots d_{-k}$$
>
>>[!example] Beispiel
>>$101,001_2=5,125_{10}$

### Negative Zahlen

>[!info]- Betrag und Vorzeichen
>Man betrachte eine Festkommazahl $d:=d_nd_{d-1}d_{d-2}\dots d_1d_0d_{-1}\dots d_{-k}$.
>
>Die Höchstwertigste Stelle $d_n$ wird als Vorzeichen genutzt; $d_n{n-1}$ bis $d_{-k}$ den Betrag.
>
>>[!example] Beispiel
>> Für das Höchstwertigste Bit im Binärsystem gilt: `0` = positiv; `1` = negativ.
>>
>>| `111` | `110` | `101` | `100`/`000` | `001` | `010` | `011` |
>>| :----: | :----: | :----: | :----------: | :----: | :----: | :----: |
>>| $-3$   | $-2$   | $-1$   | $0$   | $1$   | $2$  | $3$  |
>
>---
>###### Eigenschaften
>
>- Der Darstellbare Zahlenbereich ist symmetrisch um Null: $[-(2^n-2^{-k}),2^n-2^{-k}]$
>- *Es gibt zwei Darstellungen für $0$ ($0$ und $-0$); das ist problematisch.*

>[!info]- Einerkomplement
>Man betrachte eine Festkommazahl $d:=d_nd_{d-1}d_{d-2}\dots d_1d_0d_{-1}\dots d_{-k}$.
>
>Die Höchstwertigste Stelle $d_n$ wird als Vorzeichen genutzt.
>Bei positiven Zahlen entspricht $d_n{n-1}$ bis $d_{-k}$ den Betrag.
>Bei negativen Zahlen entspricht $d_n{n-1}$ bis $d_{-k}$ *bitweise invertiert* den Betrag.
>
>>[!example] Beispiel
>> Für das Höchstwertigste Bit im Binärsystem gilt: `0` = positiv; `1` = negativ.
>>
>>| `100` | `101` | `110` | `111`/`000` | `001` | `010` | `011` |
>>| :----: | :----: | :----: | :----------: | :----: | :----: | :----: |
>>| $-3$   | $-2$   | $-1$   | $0$   | $1$   | $2$  | $3$  |
>
>---
>###### Eigenschaften
>
>- *Es gibt zwei Darstellungen für $0$ ($0$ und $-0$); das ist problematisch.*

>[!info]- Zweierkomplement
>Man betrachte eine Festkommazahl $d:=d_nd_{d-1}d_{d-2}\dots d_1d_0d_{-1}\dots d_{-k}$.
>
>Die Höchstwertigste Stelle $d_n$ wird als Vorzeichen genutzt.
>Bei positiven Zahlen entspricht $d_n{n-1}$ bis $d_{-k}$ den Betrag.
>Bei negativen Zahlen entspricht $d_n{n-1}$ bis $d_{-k}$ *bitweise invertiert und $1$ an der niederwertigsten Stelle addiert* den Betrag ("Einerkomplement $+1$" für ganze Zahlen).
>
>>[!example] Beispiel
>> Für das Höchstwertigste Bit im Binärsystem gilt: `0` = positiv; `1` = negativ.
>>
>>| `100` | `101` | `110` | `111` | `000` | `001` | `010` | `011` |
>>| :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
>>| $-4$ | $-3$ | $-2$ | $-1$ | $0$ | $1$ | $2$ | $3$ |
>
>---
>###### Eigenschaften
>
>- Der Zahlenbereich ist nicht symmetrisch: $[-2^n,2^n-2^{-k}]$
>- *Es gibt eine einzige Darstellung für $0$.*
>- Ermöglicht elegante Arithmetik analog Dezimalsystem (Subtraktion als Addition einer negativen Zahl)
>- Allgemein verwendete Darstellung für Festkommazahlen.

>[!info]- Exzesscodierung (Bias)
>Die Exzesscodierung erfolgt üblicherweise nur für ganze Zahlen mit
>
>- $n$ Vorkommastellen;
>- $k$, die Verschiebung (auch: "bias"), frei wählbar zwischen $0\dots2^{n-1}$.
>
>Entspricht $k=2^{n-1}$ spricht man von einem ausgeglichenen Exzesscode und es kann die Angabe von $k$ entfallen.
>
>Ziffernfolge der Länge $n$: $d:=d_{n-1}d_{n-2}\dots d_1d_0$
>
>Zum Codieren wird $\text{Wert}+k$ als vorzeichenlose Binärzahl gespeichert.
>Zum Decodieren wird die Binärzahl vorzeichenlos interpretiert und der bias $k$ abgezogen.
>
>>[!example] Beispiel
>>Wert $a=-79$ soll mit 8 Bit in Exzesscodierung dargestellt werden. Für $k$ gilt implizit $k=2^{8-1}=128$.
>>- Codierung: $d=(-79)+128=49$; Binärsystem: `00110001`;
>>- Decodierung: `00110001` = $49$, $49-128=-79$.
>
>---
>###### Eigenschaften
>
>- Der ausgeglichene Exzesscode teilt den Wertebereich nahezu symmetrisch um die Null: $[-2^n,2^n-1]$.
>- Es gibt eine einzige Darstellung für $0$.
>- Addition und Subtraktion ist einfach möglich; Multiplikation/Division nicht.
>- Vergleich auf "<" ohne Decodierung als vorzeichenloser Vergleich möglich.

### Gleitkommadarstellung

Die Festkommadarstellung ist ungeeignet um ausreichend viele (rationale) Zahlen darzustellen. Es wird eine Darstellung mit beliebig großer Zahlen und konstanten relativen Genauigkeit benötigt.

>[!info] Gleitkommadarstellung
>Eine *Gleitkommazahl* (floating-point number) $d$ ist eine $n$-stellige Bitfolge, die als Dezimalzahl $\langle d\rangle$ interpretiert folgendes Format hat: $$\langle d\rangle:=(-1)^S\cdot M\cdot2^E$$ mit
>
>- $S$ - Vorzeichen
>- $M$ - Mantisse
>- $E$ - Exponent (vorzeichenbehaftete Darstellung)
>
>Als Bitfolge: $$\underbrace{d_{n-1}}_{S}\;\underbrace{d_{n-2}\dots d_{n-(i+1)}}_{i\text{ Bits }E}\;\underbrace{d_{n-(i+2)}\dots d_1d_0}_{n-i-1\text{ Bit }M}$$

Die Gleitkommadarstellung ist mehrdeutig:

- $0,001_2\cdot 2^5=\frac{1}{8}\cdot32=4$
- $0,100_2\cdot 2^3=\frac{1}{2}\cdot8=4$

Die eindeutige Darstellung erfolgt durch Normalisierung:

- Die Mantisse hat die Form $1,\text{xxxxx}$, also $1\leq M\lt2$
- Führende $1$ weggelassen: nur Nachkommastellen codiert
	- Nachkommateil der Mantisse heißt *Fraction*.

#### Standardisierte Darstellung: IEEE 754

Einfache Genauigkeit: 32 Bit

![[IEEE754_single_precision.png]] 

Doppelte Genauigkeit: 64 Bit

S: 1 Bit
E: 11 Bit
M: 52 Bit

#todo improve

Sonderfälle:

- $+\infty$: `0 1111 1111 0000 0000 0000 0000 0000 000`
- $-\infty$: `1 1111 1111 0000 0000 0000 0000 0000 000`
- `NaN`: Nicht darstellbare Zahlen (z.B. Division durch Null)

Eigenschaften:

- Nicht gleichabständig: kleine Zahlen feiner aufgelöst als große.
- Rechenoperationen erfordern spezielle Hardware (FPU).

Rechnen:

- Schritte bei Addition:
	1. Exponenten angleichen
	2. Mantissen addieren/subtrahieren
	3. Ergebnis normalisieren
	4. ggf. runden

#todo unfertig?

---
## Überblick und Ressourcen

>[!tldr] tl;dr
>#todo
>^tldr

>[!link] Hilfreiche Links
>Zu [[#Gleitkommadarstellung]]:
>
>- [Video: How Floating-Point Numbers Are Represented - Spanning Tree](https://www.youtube.com/watch?v=bbkcEiUjehk) 
>- [Video: HOW TO: Convert Decimal to IEEE-754 Single-Precision Binary - Steven Petryk](https://www.youtube.com/watch?v=tx-M_rqhuUA)
>
>Zu [[#Addition]]:
>- [Video: HOW TO: Adding IEEE-754 Floating Point Numbers](https://www.youtube.com/watch?v=mKJiD2ZAlwM)

>[!source] Quellen
>- RS Foliensatz 5 - Information und Zahlendarstellung
>^sources
