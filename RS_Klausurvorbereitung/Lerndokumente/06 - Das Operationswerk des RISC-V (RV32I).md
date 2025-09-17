[[#Überblick und Ressourcen|Zum Überblick]]

>[!target]- Prüfungsrelevante Inhalte
>- Halbaddierer
>- Volladdierer
>- Aufbau der ALU
>	- 1-Bit ALUs
>	- Struktur der kompletten ALU
>- Ripple-Carry Adder: Aufbau und Funktionsweise
>
>---
>(Siehe Foliensatz 14 - Zusammenfassung)

Wie sieht eine RISC-V CPU aus?

---
## Halbaddierer

Ein Halbaddierer addiert zwei 1-Bit-Operanden ohne Berücksichtigung eines Übertrags.

*Eingang*: Niederwertigste Stelle der Summanden: $a_0,b_0$

*Ausgang*:

- $y_0$ - Summe der beiden Eingänge (ohne Carry-In)
- $c_0$ - Übertrag zur nächsten Stelle

## Halb- und Volladdierer

- Ein *Halbaddierer* addiert zwei Eingänge.
	- Summe: $y=a\oplus b$
	- Carry: $c=a\wedge b$
- Ein *Volladdierer* addiert drei Eingänge.
	- Summe: $y=a\oplus b\oplus c_{\text{ein}}$
	- Carry: $c_{\text{aus}}=(a\wedge b)\vee(a\wedge c_{\text{ein}})$

Addierer können zu mehrstelligen Addierwerken (z.B. [[06 - Das Operationswerk des RISC-V (RV32I)#Ripple-Carry Adder|Ripple-Carry-Addierer]]) kombiniert werden.

#todo obiges besser

---

#todo alles dazwischen

---
## Ripple-Carry Adder

Der *Ripple-Carry Adder* dient der Addition mehrstelliger Binärzahlen.

>[!info] Ripple-Carry Adder
>Ein $n$-Bit-Carry-Addierer kann zwei $n$-stellige Binärzahlen addieren. Das Ergebnis hat $n+1$ Stellen.
>
>Er setzt sich aus $n$ Volladdierern zusammen. Dabei wird der Übertrags-Ausgang der Addierer jeweils an einen Eingang des nächsten Volladdierers angeschlossen. Der letzte Volladdierer bildet den $(n+1)$-ten Ausgang des Schaltnetzes.
>
>#todo image

---
## Überblick und Ressourcen

>[!tldr] tl;dr
>#todo
>^tldr

>[!link] Hilfreiche Links
>#todo

>[!source] Quellen
>- RS Foliensatz 6 - Operationswerk - hierarchischer Entwurf einer ALU für RV32i-Befehle
>^sources
