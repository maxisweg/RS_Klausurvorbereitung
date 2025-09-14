## Informationen

> [!info] Offizielle Ankündigung
> - #todo
> 
> [Quelle](placeholder)

>[!info] Weitere Informationen
>Es steht eine RISC-V Befehlsliste und ISO-Gatterliste für die Klausur bereit. Diese wird vor Ort verteilt. Sie ist im [Lernraum](https://lernraum.th-luebeck.de/course/section.php?id=73536) zu finden.

---
## Mitzubringen

>[!info] Hilfsmittel
> - Schreibzeug (kein eigenes Papier)
> - Ein nicht-programmierbarer Taschenrechner

>[!failure] Verboten
>- Eigene Notizen, Skript
>- Elektronische Geräte, insbesondere:
>	- Mobiltelefone, Smart-Watches
>		- Müssen außer Reichweite weggepackt sein (nicht am Körper)

Studierendenausweis nicht vergessen!

---
## Inhalte

- [ ] Maschinensprache und Assembler
	- [ ] Unterschiede Assemblerprogrammierung zu Hochsprachen wie C
	- [ ] Aufbau eines Assemblerprogramms für den RISC-V
	- [ ] Aufbau Assembler- und Maschinensprachebefehle (Opcode, Operanden)
- [ ] Assemblerprogrammierung des RISC-V
	- [ ] Assemblersprache: Aufbau, Opcode, Operanden, 1-, 2- und 3-Adressformat
	- [ ] Adressierungsmodi
	- [ ] Befehlstypen des RISC-V
	- [ ] Befehle des RISC-V, Register-Konventionen (ABI)
	- [ ] Aufbau, Struktur und Syntax eines Assemblerprogramms für den RISC-V
		- [ ] Speicherbelegung beim RISC-V@THL
		- [ ] Assembler-Direktiven
	- [ ] Assemblerprogrammierung (Bedingte Sprünge, Schleifen, Stack, Unterprogramme, ...)
	- [ ] Zustandsbasierte Programmierung
	- [ ] Assemblerprogramm lesen und erklären können (z.B. Fehler finden)
- [ ] Historisches
	- [ ] Originale von-Neumann-Architektur
	- [ ] Moore's Law
- [ ] Die RV32-Architektur
	- [ ] Speicherorganisation: Von-Neumann vs. Harvard-Architektur
	- [ ] Funktionseinheiten einer CPU
	- [ ] Anzahl der Takte je Befehl
	- [ ] Architektur des RISC-V (RV32I)
		- [ ] Datenpfadnutzung einzelner Befehle
	- [ ] Von-Neumann Zyklus des RISC-V
- [ ] Zahlendarstellung und rechnen im Binärsystem
	- [ ] Definitionen
	- [ ] Stellenwertsystem
	- [ ] Zahlendarstellungen
		- [ ] Festkommazahl
		- [ ] Negative Zahlen (Vorzeichen + Betrag, Komplementdarstellungen, Exzesscodierung)
		- [ ] Gleitkommadarstellung (Mantisse, Exponent, IEEE-Darstellung, Normalisierung)
	- [ ] Eigenschaften (Vor-, Nachteile), damit rechnen und umgehen können
- [ ] Das Operationswerk des RISC-V (RV32I)
	- [ ] Halbaddierer
	- [ ] Volladdierer
	- [ ] Aufbau der ALU
		- [ ] 1-Bit ALUs
		- [ ] Struktur der kompletter ALU
	- [ ] Ripple-Carry Adder: Aufbau und Funktionsweise
- [ ] Boolesche Algebra
	- [ ] Boolesche Algebra (damit rechnen können: Regeln, Präzendenzen der Operatoren, ...)
	- [ ] Boolesche Funktionen
		- [ ] Total vs. partiell
		- [ ] Formal angeben können
		- [ ] Eigenschaften ((Nicht-) Erfüllbarkeitsmenge, Definitionsbereich, Don't-Care-Bereich)
		- [ ] Darstellung als Tabelle
		- [ ] Boolesche Ausdrücke
		- [ ] Definition, atomare Ausdrücke
		- [ ] Tiefe eines Booleschen Ausdrucks
		- [ ] Operatorbaum
		- [ ] Erweiterte boolesche Ausdrücke (erweiterter Operatorbaum)
- [ ] Schaltnetze
	- [ ] Schaltnetz (SN)
		- [ ] Begriffe
		- [ ] Tabellendarstellung
	- [ ] Aufbau aus Gattern
		- [ ] Gegebenes SN lesen können
	- [ ] Gatter: Für eigenen Lösungen ISO-Darstellungen (dt. und US Darstellung)
	- [ ] Halbaddierer, Volladdierer
	- [ ] Schaltnetzentwurf
		- [ ] Struktureller Entwurf
		- [ ] Systematisches Vorgehen Schaltnetzentwurf
			- [ ] Tabellendarstellung
			- [ ] Minimieren mit KV
			- [ ] Funktion des SN gegeben in verschiedenen Formen (Text, Boolescher Ausdruck)
		- [ ] Darstellungen (kDNF, DNF, kKNF, KNF)
		- [ ] Rechen mit booleschen Ausdrücken, z.B. zum Minimieren
	- [ ] Strukturbeschreibung
		- [ ] Kopplung von Modulen
		- [ ] Blockbildung/Parallelintranziierung
		- [ ] Kaskadierung
		- [ ] Rechnen mit Schaltnetzen (Halb-, Volladdierer, Multiplizierer)
		- [ ] Multiplexer
		- [ ] SN lesen, verstehen und ggf. erweitern können
- [ ] Schaltwerke
	- [ ] Darstellungen (Tabelle, Zustandsdiagramm)
	- [ ] Automatenverhalten formal
	- [ ] Automatentypen
		- [ ] Zustandsdiagramm für Moore (Autonom, Medwedjew) und Mealy
	- [ ] Schaltwerkentwurf
	- [ ] Verhalten rückgekoppelter SN. Ideal vs. Real
	- [ ] Flipflops (RS-FF (NOR- und NAND-Varianten), Flankengesteuerters D-FF)
- [ ] Das Steuerwerk des RISC-V (RV32I)
	- [ ] Verteilte Implementierung des Steuerwerks
		- [ ] Datenpfad und Datensenken setzen
		- [ ] Wahl der Operanden (Register und Immediate)
		- [ ] Operation der ALU
	- [ ] Befehlstypen und Auswertung
	- [ ] Datenpfade und aktive Funktionseinheiten bei einzelnen Befehlen
- [ ] Architekturkonzepte - CISC und RISC
	- [ ] Eigenschaften
	- [ ] Vergleich
- [ ] Pipelining im RISC-V
	- [ ] Funktionsprinzip
	- [ ] Pipelinestufen
	- [ ] Geschwindigkeitszuwachs
	- [ ] Probleme (Hazards)
		- [ ] Benennen, beschreiben
		- [ ] Umgang
- [ ] Die Akkumulatormaschine
	- [ ] Eigenschaften
	- [ ] Mikroprogrammiert
		- [ ] Funktion eines mikroprogrammierten Steuerwerks
		- [ ] Mikroprogramm und -befehle lesen und ergänzen können

---
# Weiteres

> [!link] Hilfreiche Links
> \-
