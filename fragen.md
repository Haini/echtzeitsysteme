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
Wie unterscheiden sich diese beiden Arten von Systemen in ihren Anforderungen?

+ Fail-Safe hat einen sichern Zustand in der Umwelt den es im Fall eines Systemfehlers erreichen kann
(z.B. Zugsignale)
    + Fail Safeness ist eine Anwendungseigenschaft
    + Hohe Fehlererkennungsabdeckung ist wichtig
    + Verwendung von Watchdog oder Heartbeat Signal
+ Fail-Operational heiszt dass kein sicherer Zustand bei einem Fehler erreicht werden kann
    + Das Computersystem muss also auch nach dem kritischen Fehler ein minimum an Service
    aufrecht erhalten.
    + Aktive Redundanz ist wichtig 
    (Siehe Flugzeug, bei Absturz sollte man nicht alles abschalten und warten)

## Wie funktioniert *Christian's Algorithmus* zur Uhrensynchronisation?
+ Knoten p1 sendet Sync Request an Knoten p2, zum Zeitpunkt t0
+ Knoten p2 empfaengt zum Zeitpunkt t1, sendet T zum Zeitpunkt t2
+ Knoten p1 empfaengt zum Zeitpunkt t3

Berechnung der Round-Trip Time *RTT* = $t_3 - t_0$.  
Knoten p2 setzt seine lokale Zeit auf $T + \frac{d}{2}$.  
Dadurch betraegt der *Clock Sync Error* maximal $\frac{d}{2}$
## Charakterisieren Sie die folgenden Interface Typen (6)

+ *Elementary Interface*
    + Unidirectional control flow (e.g. dual ported ram)
    + Information push to component (e.g. phone call, interrupt)
    + Simpler than composite interface
+ *Composiste Interface*
    + Bidirectional control flow (e.g. queue of event messages)
    + Information pull when required (e.g. checking mail)
+ *Temporal Firewall Interface*
    + Prohibits external control on a component
    + Producer uses information push
    + Consumer uses information pull

## Wie lauten die vier grundlegenden Aussagen zur Zeitmessung (*Fundamentals in Time Measurement*) .. (3)
$\ldots$ fuer ein verteiltes System mit globaler Zeitbasis der Granularitaet g?

+ Wird ein Ereignis von zwei Knoten beobachtet koennen die Zeitstempel des Ereignisses um 
einen Tick verschieden sein.
+ Messung der Dauer: $d_{obs} - 2g^{global} < d^{z}_{true} < d_{obs} + 2g^{global}$
+ Die zeitliche Ordnung von 2 Events e1 und e2 kann aus den Zeitstempeln abgelesen werden wenn gilt
    + $|t^{j}(e1) - t^{k}(e2)| \geq 2$
+ Die zeitliche Reihenfolge von Events kann immer dann abgeleitet werden wenn die Eventmenge
    + 0/$\Delta$ Vorausgehend ist und
    + $\Delta \geq 3g^{global}$ 

## Wie definiert man im Kontext der Echtzeitsysteme eine Komponente? Wodurch ist diese Definition begruendet? (3)
Wahrscheinlich um eine systemweite, konsistente Wahrnehmung von Zeit zu haben?  
Eine Real Time Komponente
+ ist ein komplettes Computer System, z.B. ein Knoten
+ ist time aware
+ besteht aus
    + Hardware
    + Software
    + State

## Was versteht man unter dem *Action Delay*?
+ Wie grosz ist der Action Delay in einem verteilten Echtzeitsysteme
    + (a) ohne globale Zeitbasis?
    + (b) mit globaler Zeitbasis?

## Wie funktioniert die Arbitrierung von Nachrichten in einem Minislotting Protokoll (z.B. ARINC629)?
+ Jeder Node hat eine bestimmte Zeit die er warten muss bevor er senden darf. Wenn in seiner Wartezeit
kein Node mit einer kürzeren Wartezeit (höhere Priorität) sendet (da dieser ja weniger lang warten muss)
kann der Node senden.

## Welche Anforderungen stellt man an eine globale Zeitbasis fuer ein Echtzeitsystem? (2)
+ Chronoskopisches verhalten (Keine Diskontinuitäten, auch während der resynchronisation)
+ Verwendetet die Metrische Sekunde
+ Known Precision
+ High Dependability

## Beschreiben Sie die statischen und die dynamischen Attribute einer RT-Entity. (3)
+ Statisch
	+ Name
	+ Type
	+ Value Domain
	+ Max. rate of change
+ Dynamisch
	+ Wert

## Wie funktioniert die Arbitration in einem CAN-Netzwerk? (4)
+ CSMA/CR

## Skizzieren Sie einen *Fail-Silent TTP Node* und beschreiben Sie dessen Komponenten und deren Aufgaben kurz. (2)
+ Besteht aus einem Host, einem TTP Controller (für das Protokoll) und einem Bus-Guardion der weiß wann der TTP Controller
senden darf. Falls dieser außerhalb seines Zeitslotes senden will (Babbling Idiot) dreht der Bus-Guardian einfach den 
Bus Zugriff ab. Wird verwendet um die Fail-Silent Annahme zu verstärken.

## Was versteht man unter einem *H-State* und einem *G-State*? Beschreiben Sie die Bedeutung dieser beiden Konzepte. (2)
+ Der H-State (History State) beschreibt die notwendige Information (State) um einen initialisierten Node an einem bestimmten
Zeitpunkt zu starten.
+ Der G-State ist der minimalste H-State (keine Pending Messages ..)

## Welche Eigenschaften muessen beschrieben werden, um das Echtzeit-Interface.. (2)
(Linking Interface) zwischen Subsystemen und Echtzeitsystemen vollstaendig zu Charakterisieren?
+ (Ich glaube er meint):
+ Temporal Preconditions
	+ wann Inputs available sind
+ Temporal Postconditions:
	+ wann die Outputs available sind
+ Functional Properties

## Wie lautet die *Reasonableness Condition* fuer eine globale Zeitbasis? (2)
+ In einem System mit der gleichen Zeitbasis darf die Precision höchstens ein Macrotick sein.
+ Welche Konsequenzen hat eine Verletzung der Reasonableness Condition?
+ Der Timestamp eines Events gemessen von zwei unterschiedlichen Nodes kann sich um mehr als
1 Tick unterscheiden.

## In welchem Verhaeltnis stehen *kausale* und *temporale* Ordnung? (2)
+ Kausal impliziert Temporal, aber nicht umgekehrt

## Erklaeren Sie die Funktionsweise des *Central Master Algorithm* zur Uhrensynchronisation.
+ Ein Central Master schickt periodisch seine locale Zeit aus.
+ Welche Precision kann mit diesem Algorithmus erreicht werden?
+ Precision = 2*(Drift Rate)*(Resync Intervall) + (Jitter)

## Erklaeren Sie die Funktionsweise eines zeitgesteuerten Kommunikationsprotokolls. (2)
+ Jeder Teilnehmer weiß a priori wann er Buszugriff hat. Daher muss man bei den Nachrichten
auch keine Identifikation mitschicken, da diese Information, Zeitabhängig, jeder Teilnehmer schon hat.

## Was versteht man unter der Idempotenz einer Nachricht?
+ Das mehrmalige empfangen einer Idempotenten Nachricht verändert die Bedeutung der Nachricht nicht.
+ State Messages sind Idempotent, Event Messages nicht.

## Was versteht man unter der *Permanenz* einer Nachricht? Wann ist eine Nachricht permanent? (2)
+ Wenn ein Node die Nachricht und alle davor versendeten empfangen hat.

## Was versteht man unter *Dense Timebase*?
+ Für jedes p, q (p < q) aus {Dense Timebase} gibt es ein r, für das gilt: p < r < q.

+ Welche Eigenschaften einer solchen Dense Timebase kann man aus den fundamentalen Grenzen
der Zeitmessung (*Fundamental Limits of Time Measurement*)?

## Wann spricht man von einem *phasensensitiven*, wann von einem *phaseninsensitiven* Real-Time Image?
+ Ein Phaseninsensitives RT-Image hat eine Temporal Accuracy die länger ist als die Zeit die das nächste
RT-Image braucht um zu dem Controller zu kommen. Das heißt, es gibt Zeitpunkte, wo der Controller 2 valide
RT-Images hat.
+ Ein Phasensensitives RT-Image ist invalid bevor das nächst RT-Image (mit der update Frequenz d_update) ankommt.

## Was versteht man unter *implizieter* und *expliziter* Flusskontrolle? (2)
+ Explizite Flusskontrolle erfolgt durch den Empfänger via spezieller Leitungen (cts) oder über eigene Acknowledge
Telegramme.
+ Implizite Flusskontrolle wird z.B. in Zeitgesteuerten Protokollen umgesetzt. Die Datenrate ist auf jeden Fall
a priori bekannt.

+ Beschreiben Sie kurz die Eigenschaften jedes dieser Flusskontrollparadigmen.

+ Explizit
	+ Error detection beim Sender
	+ Thrashing unter hoher Last möglich
+ Implizit
	+ Error detection beim Receiver

##  24.06.2013 Frage 2

## Was versteht manunter TAI und UTC. Charakterisieren Sie diese Standards kurz.
+ (TAI) International Atomic Time
	+ Definiert die Sekunde als vielfaches des Zerfalls eines speziellen Atoms
	+ Physical Time Standard
	+ Chronoscopic
+ (UTC) Universal Time Coordinated
	+ Astronomical Time Standard
	+ Die Sekunde entspricht dem TAI Standard

## Was versteht man unter *G-State*? Wofuer benoetigt man diesen?
+ Siehe oben

## Welche Interfaces einer Echtzeitkomponente unterschieden wir?
+ Beschreiben Sie kurz die Aufgabe und Charakteristik jedes dieser Interfaces.
+ LIF - Linking Interface
	+ Real time Interface
	+ Time aware
	+ Contains RT observations
+ CP - Configuration Planning Interface
	+ Used to install a new node
+ DM - Diagnostic and Maintainance Interface
	+ Used to debug Hardware
	+ Knowledge about internal required
+ Local Interface
	+ Communication with other nodes

## Was versteht man unter einem Information Push Interface bzw. einem Information Pull Interface?
+ Ein Information Push Interface sagt dir wann Daten da sind.
+ Ein Information Pull Interface musst du fragen ob es date hat.

## Charakterisieren Sie die Funktionsweise und Eigenschaften eines ereignisgesteuerten Kommunukationsprotokolls.
+ Messages zu jedem Zeitpunkt möglich
+ Maximum Execution Time und Reading error sind groß
+ Benötigt expliziten Flow Control
+ Error Detection beim Sender

## Beschreiben Sie zwei Strategien, wie zeitgesteuerte und ereignisgesteuerte Kommunikation kombiniert / integriert werden koennen.
+ TT und ET wechseln sich periodisch ab
+ ET 'on top of' TT

## Was versteht man unter *Sparse Timebase*? Wofuer wird diese benoetigt?
+ (delta)/(pi) precedent. In einer Sparse Timebase darf nur in der (delta) Phase gesendet werden.
	+ Sie wird benötigt um in der Kommunikation von 2 Clustern, ohne Synchronisierten Timebases, die
	Temporale Ordnung der Events zu ermöglichen.

## Wie lautet die *Synchronisationsbedingung*? Erklaeren Sie diese. (2)
+ (Synchronisations Funktion) + (Drift Rate) < (Precision)
+ Die Synchronisations Funktion hängt von dem Jitter und dem Synchronisationsalgortihmus ab.
+ Die Drift Rate beschreibt die maximale Abweichung der clocks der Nodes.

## Erklaeren Sie die Funktionsweise eines zeitgesteuerten Kommunikationsprotokolls.
+ Jeder Node bekommt a priori einen Zeitslot in dem er Senden Darf.

+ Welche Vorteile bietet die zeitgesteuerte gegenueber der ereignisgesteuerten Kommunikation?
+ Es ist keine identifikations Information notwending, da jede Nachricht aufgrund der Empfangszeit
eindeutig einem Sender zugeordnet werden kann.
+ Es kann eine Worst Case Latency angegeben werden.

## Was versteht man unter einem *Simple Task*?
+ Ein Task der keine Synchronisation benötigt und keine Blocking Statements beinhaltet.
+ Zu Beginn sind alle Inputs vorhanden und wenn der Task beendet ist sind alle Outputs vorhanden.
