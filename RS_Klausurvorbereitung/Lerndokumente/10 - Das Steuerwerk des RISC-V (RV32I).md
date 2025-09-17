[[#Überblick und Ressourcen|Zum Überblick]]

>[!target]- Prüfungsrelevante Inhalte
>- Verteilte Implementierung des Steuerwerks
>	- Datenpfad und Datensenken setzen
>	- Wahl der Operanden (Register und Immediate)
>	- Operation der ALU
>- Befehlstypen und Auswertung (keine Bitnummern!)
>- Datenpfade und aktive Funktionseinheiten bei einzelnen Befehlen
>
>---
>(Siehe Foliensatz 14 - Zusammenfassung)

Implementierung, Befehlstypen, Datenpfade.

---
## Verteilte Implementierung des Steuerwerks

Das *Steuerwerk* ist modular aufgebaut, um Geschwindigkeit und Erweiterbarkeit zu verbessern:

- *Control*:
	- Dekodiert den Opcode → legt Datenpfad fest
	- Schaltet Multiplexer (ALUSrc, MemToReg)
	- Aktiviert Datensenken (RegWrite, MemWrite, MemRead)
	- Erzeugt ALU-Op (Vorselektion für ALU Control)
- *ALU-Control*:
	- Erzeugt die konkrete ALU-Operation (Add, Sub, AND, OR, ...)
	- Nutzt ALU-Op + Funct3 + Funct7[5]
- *Immediate Generation Unit (ImmGen)*:
	- Extrahiert und vorzeichenerweitert Immediate-Werte aus Maschinenbefehl
	- Je nach Befehlstyp unterschiedliche Bitpositionen zusammensetzen

Vorteil: parallele Verarbeitung der Teilaufgaben → schnelleres Decoding und klarer modularer Aufbau.

---
## Befehlstypen & Auswertung

- [[02 - Assemblerprogrammierung des RISC-V#^rtype|R-Type]]
	- Operanden: 2 Register
	- Ziel: 1 Register
	- Steuerung: RegWrite=1, ALUSrc=0, MemRead=0, MemWrite=0

#todo 

---
## Überblick und Ressourcen

>[!tldr] tl;dr
>#todo
>^tldr

>[!link] Hilfreiche Links
>#todo

>[!source] Quellen
>- RS Foliensatz 10 - Die Kontroller Übernehmen: Das Steuerwerk des RISC-V
>^sources
