[[#Überblick und Ressourcen|Zum Überblick]]

>[!target]- Prüfungsrelevante Inhalte
>- Assemblersprache: Aufbau, Opcode, Operanden, 1-, 2- und 3-Adressformat
>- Adressierungsmodi
>- Befehlstypen des RISC-V
>- Befehle des RISC-V, Register-Konventionen (ABI)
>- Aufbau, Struktur und Syntax eines Assemblerprogramms für den RISC-V mit den im Modul verwendeten Tools
>	- Speicherbelegung beim RISC-V@THL
>	- Assembler-Direktiven
>- Assemblerprogrammierung
>	- Bedingte Sprünge, Schleifen, Stackverwendung, Unterprogramme, Variablen, ...
>- Zustandsbasierte Programmierung
>- Ein Assemblerprogramm lesen und erklären können, z.B. Fehler finden
>---
>
>(Siehe Foliensatz 14 - Zusammenfassung)

Grundlagen der Assemblerprogrammierung.

---
## Aufbau, Opcode, Operanden, Adressformate

Zur Erinnerung:

![[01 - Maschinensprache und Assembler#Aufbau von Assembler- und Maschinensprachebefehlen]]


Es werden folgende *Formate* unterschieden, die beschreiben, wie viele explizite Operanden ein Befehl einer Assemblersprache hat:

- 1-Adressformat
- 2-Adressformat
- 3-Adressformat

Bei einem 1-Adressformat, zum Beispiel, ist die implizite Angabe von Operanden daher erforderlich.

Nach ihrem Format werden Assemblersprachen oft klassifiziert. *RISC-V nutzt das 3-Adressformat*.

---
## Adressierungsmodi

Der *Adressierungsmodi* eines Befehls bestimmt, wie ein Operand interpretiert wird. Es wird in den folgenden Modi unterschieden:

>[!info]- Unmittelbar (immediate)
>Verwendet einen angegebenen Wert als Operand.
>>[!example] Beispiel
>>```asm
>>li t0 5           # Lade den Wert 5 in Register t0
>>```
>>Bei der `5` handelt es sich um einen unmittelbaren Operanden.

>[!info]- Direkt (direct)
>Verwendet den Inhalt der angegebenen Speicherzelle/Register als Operand.
>>[!example] Beispiel
>>```asm
>>add a0 t0 t1      # Lade Adresse der Variable var in t1
>>```
>>Bei `t0` und `t1` handelt es sich um direkte Operanden.

>[!info]- Indirekt (indirect)
>Interpretiert den Inhalt der angegebenen Speicherzelle/Register als Adresse und verwendet den Inhalt der so adressierten Speicherzelle als Operand.
>>[!example] Beispiel
>>```asm
>>la t1, var        # Lade Adresse von var in t1
>>
>>.data
>>var: .word 99
>>```
>>Das Register `t1` enthält die Adresse, die als Zeiger (Pointer) genutzt wird.

>[!info]- Indiziert/Indirekt mit Offset (indirect with replacement)
>Interpretiert den Inhalt der angegebenen Speicherzelle/Register als Adresse. Vor dem Zugriff auf die adressierte Speicherzelle wird die Zieladresse um einen Offset verändert. Der Inhalt der so adressierten Speicherzelle wird als Operand verwenden.
>>[!example] Beispiel
>>```asm
>>lw a0, (0)t1      # Lade das Element an der Adresse von t1
>>lw a1 (4)t1       # Lade das Element an der Adresse von t1 + 4 Byte
>>```
>>Das Register `t1` wird indirekt mit Offset genutzt. Prinzipiell wie Pointer in `C`.

---
## Befehlstypen des RISC-V (RV32i)

Befehle einer Assemblersprache werden oft in *Befehlstypen* eingeteilt. Innerhalb eines Typ sind Befehle gleichartig codiert und realisieren ähnliche Operation (z.B. arithmetische oder logische Befehle).

Das erleichtert die Decodierung des Befehls in der CPU und damit die Architektur dieser. Für die Assemblerprogrammierung ist die Typenunterscheidung von keiner Relevanz.

Es wird in den folgenden Typen unterschieden:

>[!info]- R-Type (Register-Register)
>Register-Register Operationen. Besitzen ausschließlich Register als Operanden. Arithmetik- und Logikbefehle.
>
>>[!example] Beispiel
>>```asm
>>add a0, a1, a2    # a0 = a1 + a2
>>and t0, t1, t2    # t0 = t1 AND t2
>>```
>
>^rtype

>[!info]- I-Type (Immediate/Load)
>Befehle mit einem Immediate-Wert, wie etwa Arithmetik und Logikbefehle mit Immediate-Operanden oder lesende Speicherzugriffe (indizierte Adressierung mit Immediate Offset.
>
>>[!example] Beispiel
>>```asm
>>addi t0, x0, 5    # t0 = t (immediate laden)
>>lw t1, 4(t2)      # t1 = Speicherwert an Adresse (t2 + 4)
>>```
>
>^itype

>[!info]- S-Type (Store)
>Speichern von Registerinhalten im Arbeitsspeicher.
>
>>[!example] Beispiel
>>```asm
>>sw t0, 0(t1)      # Speicher[t1+0] = t0
>>```
>
>^stype

>[!info]- B-Type (Branch)
>Bedingte Sprungbefehle ("branch") abhängig von Vergleichsoperationen.
>
>>[!example] Beispiel
>>```asm
>>blt t0, t1, less  # wenn t0 < t1 -> springe zu label less
>>beq t2, t3, equal # wenn t2 == t3 -> springe zu equal
>>```
>
>^btype

>[!info]- U-Type (Upper Immediate)
>Laden von großen Konstanten (20-Bit Immediate-Werte) linksbündig in ein Register. Für die Adressierung mit allen 32 Bit nötig.
>
>>[!example] Beispiel
>>```asm
>>lui t0, 0x12345   # t0 = 0x12345000
>>addi t1, t0, 0x78 # t1 = t0 + 0x78
>>```
>
>^utype

>[!info]- J-Type (Jump)
>Unbedingter Sprung an die Zieladresse ("jump").
>
>>[!example] Beispiel
>>```asm
>>j label           # springe zu label
>>jal ra, foo       # springe zu foo, speichere Rücksprungadresse in ra
>>jalr x0, 0(ra)    # zurückkehren (Adresse aus ra laden)
>>```
>
>^jtype

---
## Register-Konventionen (ABI)

Das *Application Binary Interface (ABI)* definiert die Konventionen wie Register, Speicher, Stack etc. zu verwenden sind.

Damit wird die Interoperabilität von Programmen gewährleistet.

| Name        | ABI Mnemonic | Meaning                        | Preserved across calls? |
| ----------- | ------------ | ------------------------------ | ----------------------- |
| `x0`        | `zero`       | Zero (Immutable)               | -                       |
| `x1`        | `ra`         | Return adress                  | No                      |
| `x2`        | `sp`         | Stack pointer                  | Yes                     |
| `x3`        | `gp`         | Global pointer (unallocatable) | -                       |
| `x4`        | `tp`         | Thread pointer (unallocatable) | -                       |
| `x5`-`x7`   | `t0`-`t2`    | Temporary registers            | No                      |
| `x8`-`x9`   | `s0`-`s1`    | Callee-saved registers         | Yes                     |
| `x10`-`x17` | `a0`-`a7`    | Argument registers             | No                      |
| `x18`-`x27` | `s2`-`s11`   | Callee-saved registers         | Yes                     |
| `x28`-`x31` | `t3`-`t6`    | Temporary registers            | no                      |
Die Register `tp` und `gp` dürfen gemäß ABI in Unterprogrammen nicht verändert werden, da diese von den Tools verwendet werden (z.B. für Pseudo-Instruktionen).

---
## Aufbau, Struktur und Syntax eines Assemblerprogramms

Instruktionen sind Assembler-Befehle, die eine 1:1 Entsprechung in Maschinensprache haben, während Pseudo-Instruktionen abkürzende Schreibweisen für Instruktionen sind.

### Assembler-Direktiven

*Assembler-Direktiven* sind Kommandos an den Assembler (keine Befehle/Daten).

| Direktive | Argument       | Beschreibung                                        |
| --------- | -------------- | --------------------------------------------------- |
| `.align`  | Zahl           | Richtet die nachfolgende Anweisung aus              |
| `.globl`  | Symbolname     | Fügt das Symbol der globalen Symboltabelle hinzu    |
| `.asciz`  | "Zeichenkette" | Legt eine Zeichenkette ab                           |
| `.equ`    | Name, Wert     | Definiert eine Konstante                            |
| `.byte`   | Wert...        | Legt einen oder mehrere 8-Bit Werte im Speicher ab  |
| `.half`   | Wert...        | Legt einen oder mehrere 16-Bit Werte im Speicher ab |
| `.word`   | Wert...        | Legt einen oder mehrere 32-Bit Werte im Speicher ab |
Der Speicher ist in Programmspeicher (ROM), Datenspeicher (RAM) und Ein-/Ausgabebereich (IO) gegliedert. Um im Assembler-Code einen Speicherbereich auszuwählen, werden Direktiven verwendet, die sogenannte Speichersegmente auswählen.

| Direktive | Segment                                                             |
| --------- | ------------------------------------------------------------------- |
| `.text`   | Codesegment, Programmspeicher (nur-Lese-Bereich)                    |
| `.data`   | Datensegment für initialisierte Daten (Lesen + Schreiben möglich)   |
| `.bss`    | Datensegment für uninitialisierte Daten (Lesen + Schreiben möglich) |
(Es gibt weiter solche Direktiven, die nicht behandelt werden.)

### Speicherbelegung beim RISC-V@THL

Im Assemblerprogramm kann auf Werte im Speicher per Label zugegriffen werden. Da im Disassembly (.dmp-Dateien) und im Emulator keine Label, sondern Adressen stehen ist Wissen um die Speicherbelegung notwendig.

<table style="width:100%"> <tr>
<th>Programmspeicher (ROM)</th>
<td>Adressen <code>0x40000000</code>-<code>0x40FFFFFF</code> (Länge <code>0x100000</code>)</td>
</tr>
<tr>
<th>Datenspeicher (RAM)</th>
<td>Adressen <code>0x80000000</code>-<code>0x80000FFF</code> (Länge <code>0x1000</code>)</td>
</tr>
<tr>
<th>Ein-/Ausgabebereich (IO)</th>
<td>Adressen <code>0x20000000</code>-<code>0x200001FF</code> (Länge <code>0x200</code>)</td>
</tr> </table>

---
## Assemblerprogrammierung

### Die Basics

Zur Erinnerung:

![[01 - Maschinensprache und Assembler#Aufbau eines RISC-V Assemblerprogramms]]

### Unterprogramme und Funktionen

Unterprogramme sind für strukturierte Programmierung erforderlich und ermöglichen Funktionen und Methoden in Hochsprachen.
Ein Sprung in ein Unterprogramm ist von verschiedenen Stellen des Codes möglich. Am Ende erfolgt ein Rücksprung dahin, woher der Aufruf kam.

Mit der Pseudo-Instruktion `call` wird in ein Unterprogramm gesprungen. Im callee wird die Rücksprungadresse gespeichert, die am Funktionsende (`ret`) abgerufen wird um zum Caller zurückzukehren.

```asm
_start:
	call func

func:
	# do something
	ret
```

>[!code]- Extra | Variante ohne Pseudo-Instruktionen
>Der Funktionsaufruf kann auch über die Befehle
>
>- Jump and Link (`jal`) oder
>- Jump and Link Registered (`jalr`)
>
>erfolgen.
>
>Die Adresse der nachfolgenden Instruktion wird, gemäß ABI, in `ra` gespeichert.
>
>`jalr` wird benötigt, wenn der callee weiter als der maximale Immediate-Wert (20-Bit) vom caller entfernt ist.
>
>Der Rücksprung erfolgt ebenfalls mit `jalr`. Man gibt nun die in `ra` gespeicherte Rücksprungadresse an. als Zielregister kann `zero` (`x0`) verwendet werden (da eines zwingend angegeben werden muss, es aber keine Rolle spielt).
>
>```asm
>_start:
>	# near function
>	jal ra, func
>	
>	# far function
>	la t1, func
>	jalr ra, 0(t1)
>	
>func:
>	# do something
>	jalr zero, 0(ra)  # ret
>```
>

Bei rekursiven Funktionen oder Funktionen, die andere Funktionen aufrufen, ist es wichtig die Rücksprungadresse im Stack abzulegen, damit diese nicht verloren geht.
### Stack

Der Stack wird verwendet, wenn die Register nicht mehr ausreichen. Er wächst von oben nach unten nach dem Last-In-First-Out (LiFo)-Prinzip. Der Stack sitzt bei der letzten RAM-Adresse bei Programmstart und wird im Register `sp`(`x2`) gespeichert.

#### Initialisieren des Stacks

Das Register `sp` muss zunächst initialisiert werden und startet bei der letzten Speicheradresse.

Die Initialisierung muss am Anfang des Programms mithilfe der Pseudo-Instruktion `la` ('load address') erfolgen.

```asm
.globl start
_start:
	la sp, __stack       # Initialisieren des Stacks
```

Das Symbol `__stack` wird durch dem Linker-Skript definiert. Der Linker bestimmt somit die Größe des verfügbaren Speichers.

#### Daten auf dem Stack: Push und Pop

Die Stack-Operationen `push` und `pop` müssen in RISC-V nachgebildet werden. Dazu wird der Stack-Pointer manuell de-/inkrementiert und entsprechend `sw` ('store word') bzw. `lw` ('load word') ausgeführt.

```asm
push:
	addi sp, sp, -4      # sp dekrementieren
	sw x5, 0(sp)         # Inhalt von x5 ablegen
	
pop:
	lw x5, 0(sp)         # Inhalt von x5 vom Stack
	addi sp, sp, 4       # sp inkrementieren
```

>[!code]- Extra | Mehrere Stack-Operationen zusammenfassen
>
>Es können mehrere Push/pop-Operationen zusammengefasst werden:
>
>```asm
>push3:
>	addi sp, sp, -12  # Platz für drei 32-bit Werte
>	
>	sw a0, 8(sp)      # Inhalt von x5 liegt oben
>	sw s1, 4(sp)
>	sw s2, 0(sp)
>	
>pop3:	
>	sw s2, 0(sp)      # die Werte zurückholen
>	sw s1, 4(sp)      # umgekehrte Reihenfolge beachten!
>	sw a0, 8(sp)
>	
>	addi sp, sp, 12   # Stack-Pointer wiederherstellen
>```

---
## Zustandsbasierte Programmierung

<table style="width:100%"> <tr>
<th>Kontrollflussbasiert</th>
<td>- Programmablauf verzweigt mehrfach, verästelt<br>- Einzelne Bedingungen steuern, welcher Weg duch den Code genommen wird<br>- Schleifen überall möglich</td>
</tr>
<tr>
<th>Zustandsbasiert</th>
<td>- Verhalten hängt davon ab, in was für einer Situation sich das System befindet<br>- Je Zustand unterschiedliches Verhalten, u.A. Ausgabe und Zustandswechsel<br>- Keine Schleifen innerhalb der Zustände zulässig</td>
</tr></table>

In vielen technischen Systemen sind je nach Situation nur bestimmte Aktionen sinnvoll (oder möglich). Das Verhalten wird vom aktuellen Systemzustand und aktueller Eingabe abhängig gemacht (Automatenmodell).

>[!example] Beispiel | Zustandsbasierte Programmierung
>Eine Taschenlampe mit zwei Helligkeitsstufen kann in drei Zuständen eingeteilt werden:
>
>- `OFF`:
>	- Die Taschenlampe ist aus.
>- `HALF`
>	- Die Taschenlampe leuchtet mit $50\%$ Helligkeit.
>- `FULL`
>	- Die Taschenlampe leuchtet mit voller Helligkeit.
>
>Der Wechsel der Zustände erfolgt zyklisch über einen einzelnen Knopf:
>`OFF` → `HALF`, `HALF` → `FULL` und `FULL` → `OFF`.
>
>Zustandsdiagramm:
>
>![[zustandbasierte_prog.png]]
>
>>[!code]- Code
>>Ein deutlich gekürzter Code könnte von der Struktur so aussehen:
>>
>>```asm
>>.globl _start
>>_start:
>>_mainLoop:
>>	# do some stuff
>>	# loop while button not pressed
>>	call _switchState     # button pressed: call switchState
>>	
>>_switchState:
>>_off:
>>	li t1, OFF            # load OFF into t1
>>	bne t1, t6, _half     # if current state ist not OFF, go to _half
>>	# turn light off      # else: run some code
>>	
>>_half:
>>	li t1, HALF           # load HALF into t1
>>	bne t1, t6, _half     # if current state ist not HALF, go to _FULL
>>	# turn light to half  # else: run some code
>>
>>_full:
>>	li t1, FULL           # load FULL into t1
>>	bne t1, t6, _half     # if current state ist not FULL, go to _error
>>	# turn light to full  # else: run some code
>>
>> # more stuff ...
>>```

---
## Überblick und Ressourcen

>[!tldr] tl;dr
>#todo
>^tldr

>[!source] Quellen
>- RS Foliensatz 2 - Assemblerprogrammierung des RISC-V
>^sources
