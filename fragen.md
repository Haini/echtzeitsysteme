---
title: Echtzeitsysteme Fragen (N=9, 2012-2016)
---

## Was versteht man unter Resource Adequacy?
Um Zeitgarantien geben zu koennen muss ein System
+ ausreichend Hardware Resourcen zur Verfuegung stellen um 
+ errechnete Lastspitzen und 
+ Katastrophenfaelle abzufangen.

## Wie lautet die Reasonableness Condition fuer eine globale Zeitbasis?
$g^{global} > \pi$
### Was sagt sie aus?
Gibt Sicherhheit darueber dass der Synchronisationsfehler kleiner als ein Makrogranule ist.

Also: $| t^{j}(e) - t^{k}(e) | \leq 1$
### Wofuer wird sie benoetigt?
Um die temporaere Ordnung von zwei Ereignissen wiederherzustellen.

## Beispiel fuer nicht eindeutige Ordnungsrekonstruktion
Zeigen Sie anhand eines Beispiels, dass zwei oder mehrere Cluster, die jeweils eine g/3g-sparse
Zeitbasis verwenden, nicht so kommunizieren koennen, dass die Ordnung aller Events
auf der Empfaengerseite immer eindeutig rekonstruiert werden kann.

+ Sparse Zeitbasis: ($\pi/\delta$)
    + Ereignisse duerfen nur im Intervall $\pi$ (Aktiv) auftreten.
    + Darauf folgt ein Intervall Ruhe $\delta$.
+ Um die temporaere Ordnung zweier Events zu rekonstruieren muessen die globalen Zeitmarken 
 der Events um zumindest 2 Ticks verschieden sein.
    + Eine Differenz von $2*g^{global}$ reicht dafuer nicht aus wenn 
    $t^{j}(a) - t^{k}(b) = 1$
+ Zwei Knoten in Cluster A generieren zum selben Clustweiten Tick zwei Events.
    + Diese beiden Events koennen maximal $\bigpi$ voneinander entfern sein.
    + Es existiert also keine beabsichtigte Ordnung zwischen den beiden Events
    + Cluster B sollte also nie versuchen diese beiden Events zu sortieren.
    + Cluster B sollte aber die Ordnung zwischen Events wiederherstellen wenn
    diese in unterschiedlichen clusterweiten Ticks liegen.
 + Silence for 3 granules is not sufficient.
    + Zwei Events mit der selben clustweiten Granularitaet koennen in Cluster B 
    mit Timestamps die 2 Ticks auseinander liegen versehen werden.
        + Cluster B sollte diese Events nicht sortieren.
    + Events die 3g spaeter erzeugt wurden, also in unterschiedlichen Abschnitten liegen
    sollte aber sortiert werden.
        + Werden aber ebenfalls mit 2 Ticks auseinander liegenden Zeitstempeln versehen.
+ Cluster B hat also 2 Events die er nicht sortieren soll und 2 Events die er sortieren soll
+ Da die Zeitstempel kein eindeutiges Bild liefern (Beide haben 2 Ticks Differenz)
    + Kann keine Entscheidung darueber getroffen werden was sortiert wird und was nicht
+ Bei $1/4g$ hingegen haben Events aus dem selben Zeitfenster $\leq$ 2 Ticks differenz waehrend
unterschiedliche Ticks $\geq$ 3 Ticks differenz haben.

## Durch welche Eigenschaften ergaenzen sich Interne und Externe Uhrensynchronisation? (2)
+ Interne Uhrensynchronisation
    + Hohe Verfuegbarkeit
    + Gute Kurzzeitstabilitaet
+ Externe Uhrensynchronisation
    + Gute Langzeitstabilitaet

## Was versteht man unter einem End-to-End Protocol? (5)
Ein end-to-end Protokoll ist ein Protokoll zwischen den Anwendern (Maschinen oder Menschen) 
die sich an den jeweiligen Endpunkten eines Kommunikationskanals befinden.
D.h. z.B.: Ein Ventil wird geoffnet, ein im Ventil verbauter Sensor liefert Informationen ueber 
die Ventilposition an den Verursacher des Befehls.
Gibt Sicherheit darueber dass ein Subsystem seinen Zweck erfuellt.
### Worin liegt der Vorteil der Verwendung eines solchen Protokolls?
High error-detection coverage.
### Machen die Mechanismen eines solchen Protokolls die Fehlererkennung / Korrektur auf darunterliegenden Protokollschichten hinfaellig?
Jein.
+ Macht Diagnose von Fehlern einfacher.
+ Needed if communication is less reliable than other subsystems 

## Wann spricht man von einem *temporally accurate* RT-Image? (2)
Wir nehmen an dass die RealTime Entititaet zu jedem Zeitpunkt in der nahen Vergangenheit
untersucht wurde, dann ist das RealTime Image *temporally accurate* zum Zeitpunkt $t_{i}$ wenn gilt:

$\exists t_{j} \in RH_{i} : Value(RTImage_{t_{j}}) = Value(RTEntity_{t_{i}})$

## Erklaeren Sie den Begriff *Accuracy* und *Precision*. Geben Sie jeweils ein Beispiel an. (5)
+ Accuracy bezeichnet den maximalen Offset einer Uhr von der Referenzuhr in einem Zeitintervall
    + Offset between clock k and the reference clock z at tick i
    + $offset^{k, z(k)}_{i} = |z(microtick^{k}_{i}) - z(microtick^{z(k)}_{i}|$
    + GPS, $1 \mu s$ mmoeglich.
+ Precision bezeichnet den maximalen Offset zwischen zwei Uhren in einem Ensemble von Uhren
+ an einem Macrotick i
    + $\Pi_{i} = max_{j,k} \{offset^{jk}_{i}\}$

## Was ist eine *Observation*? (2)
Eine Observation enthaelt Information ueber den State einer beobachteten RT Entity.
Sie besteht aus <Name, Time, Value> und wird als Nachricht verschickt.

## Charakterisieren Sie das Ressourcenmanagment in einem zeitgesteuerten Echtzeitbetriebssystem.
????

## Beschreiben Sie Aufgabe, Funktionsweise und Eigenschaften eines Bus Guardians.
+ Aufgabe
    + Schaltet Knoten nur zu wenn sie senden duerfen.
    + Kann Knoten die permanent senden vom BUS schalten
    + Quasi ein Tuersteher
+ Funktionsweise
    + Kennt den Zeitslot in dem der Knoten sprechen darf und aktiviert die BUS Kommunikation nur dann.
+ Eigenschaften
    + ???

## Erklaeren Sie die Begriffe *Fail-Safe System* und *Fail-Operational System*. 
Wie unterscheiden scih diese beiden Arten von Systemen in ihren Anforderungen?

## Wie funktioniert *Christian's Algorithmus* zur Uhrensynchronisation?

## Charakterisieren Sie die folgenden Interface Typen (6)

+ *Elementary Interface*
+ *Composiste Interface*
+ *Temporal Firewall Interface*

## Wie lauten die vier grundlegenden Aussagen zur Zeitmessung (*Fundamentals in Time Measurement*) .. (3)
fuer ein verteiltes System mit globaler Zeitbasis der Granularitaet g?

## Wie definiert man im Kontext der Echtzeitsysteme eine Komponente? Wodurch ist diese Definition begruendet? (3)

## Was versteht man unter dem *Action Delay*?
+ Wie grosz ist der Action Delay in einem verteilten Echtzeitsysteme
    + (a) ohne globale Zeitbasis?
    + (b) mit globaler Zeitbasis?

## Wie funktioniert die Arbitrierung von Nachrichten in einem Minislotting Protokoll (z.B. ARINC629)?

## Welche Anforderungen stellt man an eine globale Zeitbasis fuer ein Echtzeitsystem? (2)

## Beschreiben Sie die statischen und die dynamischen Attribute einer RT-Entity. (3)

## Wie funktioniert die Arbitration in einem CAN-Netzwerk? (4)

## Skizzieren Sie einen *Fail-Silent TTP Node* und beschreiben Sie dessen Komponenten und deren Aufgaben kurz. (2)

## Was versteht man unter einem *H-State* und einem *G-State*? Beschreiben Sie die Bedeutung dieser beiden Konzepte. (2)

## Welche Eigenschaften muessen beschrieben werden, um das Echtzeit-Interface.. (2)
(Linking Interface) zwischen Subsystemen und Echtzeitsystemen vollstaendig zu Charakterisieren?

## Wie lautet die *Reasonableness Condition* fuer eine globale Zeitbasis? (2)

+ Welche Konsequenzen hat eine Verletzung der Reasonableness Condition

## In welchem Verhaeltnis stehen *kausale* und *temporale* Ordnung? (2)

## Erklaeren Sie die Funktionsweise des *Central Master Algorithm* zur Uhrensynchronisation.

+ Welche Precision kann mit diesem Algorithmus erreicht werden?

## Erklaeren Sie die Funktionsweise eines zeitgesteuerten Kommunikationsprotokolls. (2)

## Was versteht man unter der Idempotenz einer Nachricht?

## Was versteht man unter der *Permanenz* einer Nachricht? Wann ist eine Nachricht permanent? (2)

## Was versteht man unter *Dense Timebase*?

+ Welche Eigenschaften einer solchen Dense Timebase kann man aus den fundamentalen Grenzen
der Zeitmessung (*Fundamental Limits of Time Measurement*)?

## Wann spricht man von einem *phasensensitiven*, wann von einem *phaseninsensitiven* Real-Time Image?

## Was versteht man unter *implizieter* und *expliziter* Flusskontrolle? (2)

+ Beschreiben Sie kurz die Eigenschaften jedes dieser Flusskontrollparadigmen.

##  24.06.2013 Frage 2

## Was versteht manunter TAI und UTC. Charakterisieren Sie diese Standards kurz.

## Was versteht man unter *G-State*? Wofuer benoetigt man diesen?

## Welche Interfaces einer Echtzeitkomponente unterschieden wir?

+ Beschreiben Sie kurz die Aufgabe und Charakteristik jedes dieser Interfaces.

## Was versteht man unter einem Information Push Interface bzw. einem Information Pull Interface?

## Charakterisieren Sie die Funktionsweise und Eigenschaften eines ereignisgesteuerten Kommunukationsprotokolls.

## Beschreiben Sie zwei Strategien, wie zeitgesteuerte und ereignisgesteuerte Kommunikation kombiniert / integriert werden koennen.

## Was versteht man unter *Sparse Timebase*? Wofuer wird diese benoetigt?

## Wie lautet die *Synchronisationsbedingung*? Erklaeren Sie diese. (2)

## Erklaeren Sie die Funktionsweise eines zeitgesteuerten Kommunikationsprotokolls.

+ Welche Vorteile bietet die zeitgesteuerte gegenueber der ereignisgesteuerten Kommunikation?

## Was versteht man unter einem *Simple Task*?