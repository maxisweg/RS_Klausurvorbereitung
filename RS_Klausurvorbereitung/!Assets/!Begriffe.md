Dieses Dokument dient zum zusammenfassen einiger allgemeineren Definitionen in einem Dokument.

---
## 04 - Die RV32I-Architektur

>[!info] Arithmetisch-Logische Einheit (ALU) 
>Die *Arithmetisch-Logische Einheit (ALU)* ist eine Komponente für Berechnungen und logische Operationen. Und je nach Architektur ggf. spezialisierte Recheneinheiten für Adressberechnungen.
>^alu

>[!info] Datenregister
>Das *Datenregister* (auch Registerbank) ist die Quelle und das Ziel für Operationen mit der ALU.
>^datenregister

>[!info] Programm Counter (PC)
>Der *Program Counter (PC)* adressiert den Speicher und enthält die Adresse des aktuellen Befehls.
>^pc

>[!info] Instruktionsregister (IR)
>Der *Instruktionsregister (IR)* dient als Pufferregister und enthält den aktuellen Befehl. Nur bei Mehrzyklen-Architekturen vorhanden.
>^ir

>[!info] Flags
>*Flags* beschreiben den Zustand der CPU, z.B. Informationen über letzte arithmetische Operation (Overflow, Zero, ...).
>^flags

>[!info] Multiplexer (MUX)
>Der *Multiplexer* ist ein Schalter für die Steuerung der Datenpfade.
>
>Die Steuersignale des Multiplexers wählen, welche Eingangssignale an den Ausgang weitergegeben werden. Bei $n$ Steuersignalen hat der Multiplexer $2^n$ Eingänge
>
>---
>[Mehr - Wikipedia](https://de.wikipedia.org/wiki/Multiplexer)
>[Video - simpleclub](https://www.youtube.com/watch?v=JpnVqaSE5_w)
>^multiplexer

>[!info] Adress-Addierer
>Ein *Adress-Addierer* ist ein spezieller Addierer in der CPU, der für Adressberechnungen zuständig ist – also für das Ermitteln der Speicheradresse, auf die zugegriffen werden soll.
>^adressaddierer

>[!info] +4-Addierer
>Ein *+4-Addierer* ist ein Addierer, der darauf ausgelegt ist, den Program Counter (PC) um $4$ zu erhöhen.
>
>Hintergrund ist, dass beim RISC-V, zum Beispiel, jede Instruktion $32$ Bit/$4$ Byte lang ist. Das entlastet die [[#^alu|ALU]], die sich somit um andere Befehle kümmern kann.
>^4addierer

