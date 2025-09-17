[[#Überblick und Ressourcen|Zum Überblick]]

>[!target]- Prüfungsrelevante Inhalte
>- CISC, RISC
>	- Beschreiben können: Eigenschaften, Vergleich
>		- Die Tabelle aus den Folien ist kein vollwertiger Vergleich!
>
>---
>(Siehe Foliensatz 14 - Zusammenfassung)

CISC vs. RISC.

---
## CISC, RISC

Prozessoren werden gemäß dem Umfang ihres Befehlssatzes eingeteilt. CISC und RISC stellen Gegensätze dar. Es gibt auch Klassifizierungen dazwischen.

>[!info] CISC (Complex Instruction Set Computer)
>Prozessoren mit einer großen Anzahl an Maschinensprachen-Befehlen gehören zu *CISC*.
>
>---
>##### Eigenschaften
>
>- Großer, komplexer Befehlssatz (100+ Instruktionen).
>- Befehle mit variabler Länge (1-15 Byte möglich).
>- Direkter Speicherzugriff in vielen Befehlen (Load, Operate, Store in einem Schritt).
>- Mikroprogrammierung häufig genutzt → einfachere CPU-Entwicklung, aber langsamere Ausführung.
>- Viele Adressierungsmodi, teils komplex.
>- Höhere Hardwarekomplexität.
>- Weniger Instruktionen im Code bedeutet weniger Speicherbedarf.
>
>Z.B. x86, VAX, PDP-11.

>[!info] RISC (Reduced Instruction Set Computer)
>Prozessoren mit einer kleinen Anzahl an Maschinensprachen-Befehlen gehören zu *RISC*.
>
>---
>##### Eigenschaften:
>
>- Kleiner, einheitlicher Befehlssatz (ca. 30-50 Instruktionen).
>- Befehle fester Länge (bei RISC-V 32 Bit).
>- Strikte Trennung von Speicher- und Rechenoperationen (Load/Store-Architektur).
>- Jeder Befehl in 1 Takt (Single-Cycle) ausführbar.
>- Wenige einfache Adressierungsmodi.
>- Hohe Taktfrequenz durch einfachen Datenpfad.
>- Hardware für Pipeline-Optimierung ausgelegt.
>- Durch die eingesparte Hardwarekomplexität (mehr Platz), sind z.B. mehr Register verfügbar.
>- Da mehr Instruktionen im Code benötigt werden, wird ebenfalls erhöhter Speicherbedarf benötigt.
>
>Z.B. RISC-V, ARM, MIPS, PowerPC, SPARC.

Die vielen, komplexen Maschinen-Befehle der CISC-Architekturen verkleinern die *semantische Lücke*, also den Unterschied der Komplexität zwischen Maschinen- und Hochsprache.

Auf einem Blick:

| Merkmal                   | CISC                  | RISC               |
| ------------------------- | --------------------- | ------------------ |
| *Ausführungszeit*         | $\geq1$ Takt          | $1$ Takt           |
| *Instruktionsanzahl*      | groß (100+)           | klein (<100)       |
| *Befehlslänge*            | variabel              | fest               |
| *Steuerung über*          | Mikroprogramm         | Hardware           |
| *Hauptspeicherzugriffe*   | viele Befehle         | `LOAD` / `STORE`   |
| *Pipelining*              | aufwändig             | einfach möglich    |
| *Codegröße (Compiler)*    | weniger Instruktionen | mehr Instruktionen |
| *Verlagerung Komplexität* | Hardware              | Compiler           |
| *Speicherbedarf*          | weniger               | mehr               |
| *Registeranzahl*          | weniger               | mehr               |
| *Energieverbrauch*        | moderat bis hoch      | gering             |

---
## Überblick und Ressourcen

>[!tldr] tl;dr
>#todo
>^tldr

>[!link] Hilfreiche Links
>- [Video: RISC vs CISC - Bina Bhatt](https://www.youtube.com/watch?v=bTCuFmY0sUg)

>[!source] Quellen
>- RS Foliensatz 11 - Klassifikation von Architekturen: CISC vs. RISC
>^sources
