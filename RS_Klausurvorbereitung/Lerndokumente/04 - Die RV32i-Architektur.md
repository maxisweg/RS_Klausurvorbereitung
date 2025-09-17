[[#Überblick und Ressourcen|Zum Überblick]]

>[!target]- Prüfungsrelevante Inhalte
>- Speicherorganisation: Von-Neumann-Architektur vs Harvard-Architektur
>- Funktionseinheiten einer CPU: Nennen, erklären können
>- Anzahl der Takte je Befehl
>- Architektur des RISC-V (RV32I) erläutern können
>	- Datenpfadnutzung einzelner Befehle
>- Von-Neumann Zyklus des RISC-V
>
>---
>(Siehe Foliensatz 14 - Zusammenfassung)

Wie kann man mit einem Chip aus Silizium einen Maschinenbefehl ausführen?
Zerlegung des Befehls: Aufteilen in Teilaufgaben, ableiten der Komponenten der CPU.

---
## Speicherorganisation

*Speicher* ist eine adressierbare Folge von Speicherzellen, die bei einem $n$-Bit breiten Adressbus im Adressbereich $0$ bis $2^n-1$ liegt. Eine Speicherzelle besteht aus einer Folge von $k$ Bits. Die Länge $k$ dieser Bitfolge (auch Speicherwort genannt) wird als *Wortbreite* des Speichers bezeichnet. Üblich sind Wortbreiten von $8,16,32,64$ Bit.
Die Speicherzelle ist die kleinste adressierbare Einheit des Speichers, sie wird im Allgemeinen komplett gelesen oder geschrieben (RISC-V kann Teile lesen/schreiben: Byte, Halbwort, Wort).

Unter *Speicherorganisation* versteht man, wie ein Computer Programmcode und Daten ablegt und darauf zugreift, was die Geschwindigkeit und Komplexität der CPU beeinflusst.

#todo obigen Text kürzen?
### Von-Neumann- vs. Harvard-Architektur

<table style="width:100%"> <tr>
<th>Von-Neuman-Architektur</th>
<td>- Programm und Daten im gleichen Speicher<br>- Interpretation, ob Inhalt Befehl oder Datum ist, entscheidet die CPU<br>- Einfachere Architektur<br>- Von Neumann Bottleneck: Es kann nur eine Instruktion bzw. Daten zurzeit durch den Bus geladen werden; die CPU wartet viel.</td>
</tr>
<tr>
<th>Harvard-Architektur</th>
<td>- Separate Speicher für Programm und Daten<br>- Bedeutung des Speicherinhalts als Befehl oder Datum durch Speichermodul vorgegeben<br>- Komplexer im Aufbau, aber besser erweiterbar und optimierbar</td>
</tr></table>

---
## Funktionseinheiten einer CPU

Die *Funktionseinheiten* einer CPU sind die einzelnen Bausteine, die zusammen die Befehlsausführung ermöglichen.

>[!info]- Steuerwerk
>Das *Steuerwerk* ist die Einheit, die den Befehl interpretiert und das Operationswerk über Steuerleitungen kontrolliert. Es ist verantwortlich für die Abarbeitung des Befehls, ggf. in mehreren Schritten und unter Beachtung des CPU-Zustands ([[!Begriffe#^flags|Flags]]).

>[!info]- Operationswerk
>Das *Operationswerk* besteht unter anderem aus:
>
>- [[!Begriffe#^alu|Arithmetisch-Logische Einheit (ALU)]]
>- [[!Begriffe#^datenregister|Datenregister]]

>[!info]- Spezialregister
>Einige *Spezialregister* sind:
>- [[!Begriffe#^pc|Programm Counter (PC)]]
>- [[!Begriffe#^ir|Instruktionsregister (IR)]]
>- Status der CPU (z.B. der letzten Berechnung der ALU) → "[[!Begriffe#^flags|Flags]]"

>[!info]- Interne Leitungen
>Interne Leitungen wie Busse, Status- und Steuerleitungen

>[!info]- Speicheranbindung
>Speicheranbindung von Programm- und Datenspeicher (Harvard-Architektur).

---
## Anzahl der Takte je Befehl

Ein *Takt* ist die kleinste zeitliche Einheit, in der eine CPU eine bestimmte Teilarbeit verrichten kann. Wie viele Takte ein Befehl benötigt, bestimmt, wie schnell ein Programm ausgeführt wird.

- *Ein-Zyklus-Prozessor*: Jeder Befehl in $1$ Takt.
- *Mehrzyklus-Prozessor*: Befehle benötigen feste Anzahl $\gt 1$.
- *CISC*: Variable Anzahl Takte pro Befehl (komplexe Befehle unterschiedlich lang)

Moderne RISC-Architekturen wie RISC-V streben an, jeden Befehl in einem einzigen Takt auszuführen. Einige komplexere Architekturen, wie etwa CISC, benötigen oft mehrere Takte oder eine variable Anzahl, abhängig vom Befehl.

---
## Architektur des RISC-V (RV32i)

Der RISC-V ist eine Minimalarchitektur für den Befehlssatz RV32i.

Eigenschaften:

- *1-Zyklus Architektur*: kompletter Befehl in einem Takt.
- *Harvard-Architektur*: getrennte Speicher für Programm und Daten.
- *Einfaches Steuerwerk*: nur $7$ Eingabebits, $8$ Ausgänge.
- *Keine [[!Begriffe#^flags|Flags]] nötig*: Bedingungen werden direkt mit ALU ausgewertet.

Wichtige Komponenten sind *[[!Begriffe#^datenregister|Registerbank]]*, *[[!Begriffe#^alu|ALU]]*, *[[!Begriffe#^adressaddierer|Adress-Addierer]]*, *[[!Begriffe#^4addierer|+4-Addierer]]*, *[[!Begriffe#^multiplexer|Multiplexer]]*.

### Datenpfadnutzung einzelner Befehle

- Load ([[02 - Assemblerprogrammierung des RISC-V#^itype|I-Type]], `lw`):
	- Register → Adressberechnung (Basis + Offset) → Speicher → Registerbank.
- Store ([[02 - Assemblerprogrammierung des RISC-V#^stype|S-Type]], `sw`):
	- Register → Adressberechnung → Speicher (Daten speichern).
- [[02 - Assemblerprogrammierung des RISC-V#^rtype|R-Type]] (`add`, `sub`, `and`, `or`):
	- Register → ALU → Register.
- Branch ([[02 - Assemblerprogrammierung des RISC-V#^btype|B-Type]], `beq`):
	- Register → ALU → ggf. neuer PC-Wert (Sprungadresse).

---
## Von-Neumann Zyklus des RISC-V

Das einfache Operationswerk des RISC-V lässt sich die Befehlsbearbeitung in 5 Schritten zerlegen:

1. *Instruction Fetch*: Befehl aus Programmspeicher in [[!Begriffe#^ir|IR]] laden.
2. *Instruction Decode (with operand fetch)*: Befehl dekodieren, Unterscheidung Befehlstypen, Bereitstellung der Operanden (aus Register und unmittelbar).
3. *Execute*: ALU berechnet Ergebnis oder Adresse.
4. *Memory Access*: Zugriff auf Datenspeicher.
5. *Write back*: Ergebnis der ALU-Operation oder die Daten aus dem Speicher in Registerbank schreiben und Ermittlung der nächsten Befehlsadresse (Sequenz oder bedingter Sprung).

Da es sich beim RISC-V RV32i um einen Ein-Zyklus-Prozessor handelt, erfolgt dieser gesamte Zyklus in einem Takt.

---
## Überblick und Ressourcen

>[!tldr] tl;dr
>#todo
>^tldr

>[!source] Quellen
>- RS Foliensatz 4 - Vom Befehl zur Handlung: Was man braucht, um Befehle auszuführen
>^sources
