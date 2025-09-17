[[#Überblick und Ressourcen|Zum Überblick]]

>[!target]- Prüfungsrelevante Inhalte
>- Unterschiede Assemblerprogrammierung zu Hochsprachen wie C.
>- Aufbau eines Assemblerprogramms für den RISC-V
>- Aufbau Assembler- und Maschinensprachebefehle
>	- Opcode, Operanden
>---
>
>(Siehe Foliensatz 14 - Zusammenfassung)

Um zu verstehen, wie eine CPU funktioniert, muss man die Sprache der CPU kennen.

---
## Von der Hochsprache zur Maschinensprache

Bekannt sind bereits Programmiersprachen wie Java, C oder Python. Sogenannte "Hochsprachen".

Die CPU versteht jedoch kein Java, C oder Python, es werden binäre Werte im Programmspeicher als Anweisungen interpretiert, die sogenannte Maschinensprache. Es erfolgt eine Übersetzung von Hochsprache zur Maschinensprache über Build-Tools wie Compiler, Linker.
Eine menschenlesbare Beschreibung der Maschinensprachenbefehle nennt sich Assembler.

---
## Unterschiede Hochsprache, Assembler, Maschinensprache


<table style="width:100%"> <tr>
<th>Hochsprache</th>
<td>- Menschenlesbar<br>- Komplexe Strukturen wie Schleifen möglich<br>- Variablen mit frei wählbaren Namen, Speicherverwaltung durch Compiler<br>- Abhängigkeit von Bibliotheken und Betriebssystem (für z.B. printf)<br>- Übersetzung in Maschinensprache durch Compiler &amp; Linker</td>
</tr>
<tr>
<th>Assembler</th>
<td>- Menschenlesbare Darstellung der Maschinensprache<br>- Direkter Zugriff auf Register der CPU<br>- Keine komplexen Konstrukte; Schleifen müssen durch Sprünge (Labels) umgesetzt werden<br>- Speicherallokation entfällt, da feste Reister genutzt werden</td>
</tr>
<tr>
<th>Maschinensprache</th>
<td>- Nicht menschenlesbar<br>- Reine Folge von Binärzahlen (Opcode + Operanden)<br>- Wird direkt von der CPU verstanden</td>
</tr> </table>

---
## Aufbau eines RISC-V Assemblerprogramms

>[!code] Code
>Einfaches Assemblerprogramm zur Berechnung einer Summe.
>```asm
>.global _start
>
>_start:
>	li a2, 1        # start
>	li a3, 10       # end
>	li a0, 0        # sum
>	add t0, x0, a2  # i = start
>	
>_loop:
>	blt a3, t0, _endloop   # if (end < i) -> end loop
>	add a0, a0, t0         # sum = sum + i
>	addi t0, t0, 1         # i = i + i
>	beq x0, x0, _loop      # jump back to loop
>	
>_endloop:
>_remain:
>	beq x0, x0, _remain    # endless loop at end
>```

#### Merkmale

- `.globl _start` = Einsprungpunkt ins Programm
- Initialisierung der Register mit Konstanten (`li`)
- Schleifenstruktur durch Vergleichs- Sprungbefehle (`blt`, `beq`)
- Register statt Variablen:
	- `a2` → Startwert
	- `a3` → Endwert
	- `a0` → Summe (Rückgabewert)
	- `t0` → Zähler/Iterator

---
## Aufbau von Assembler- und Maschinensprachebefehlen

Ein Maschinensprachebefehl besteht aus *Opcode* + *Operanden*.

- *Opcode*: bestimmt die auszuführende Operation (z.B. `add`, `blt`, `li`)
- *Operanden*: geben an, welche Register oder Konstanten beteiligt sind (z.B. `a0`, `t1`, $3$)

>[!example] Beispiel | RISC-V Assemblerbefehl
>```asm
>add a0, a0, t0
>```
>
>*Opcode*: `add` (Addition)
>*Operanden*: Zielregister `a0`, Quellenregister `a0` und `t0`
>
>Diese Zeile addiert also die Zahlen die in `a0` und `t0` stehen und speichert die Summe in `a0`.

*Für die Klausur wird eine Liste von (Pseudo-)Instruktionen des RISC-V, wie `add`, bereitgestellt. Das Dokument ist im [Lernraum](https://lernraum.th-luebeck.de/course/section.php?id=73536) abrufbar.*

Dabei geht die CPU wie folgt vor:

1. Instruktion laden (Opcode + Operanden aus Speicher)
2. Dekodieren (mit digitalen Schaltungen erkennen, welche Operation gefordert ist)
3. Operanden bereitstellen (Register oder Speicher)
4. Operation durchführen (z.B. Addition)
5. Ergebnis speichern (meist in Register)
6. Nächsten Befehl ermitteln mit sequenzieller Programmbearbeitung

---
## Überblick und Ressourcen

>[!tldr] tl;dr
>#todo
>^tldr

>[!source] Quellen
>- RS Foliensatz 1 - Von der Hochsprache zur Maschinensprache
>^sources
