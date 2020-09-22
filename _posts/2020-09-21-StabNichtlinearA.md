---
toc: true
layout: post
description: geometrisch exakte 1d finite elemente methode teil i
categories: [markdown]
title: Geometrisch exakte eindimensionale (1d) Finite-Elemente-Methode: Teil I - Kinematik, Kinetik und Konstitution
---

# Einleitung

In dieser Beitragsserie werden wir die Grundlagen der geometrisch exakten eindimensionalen Finite-Elemente-Methode mit beliebiger elastischer Materialnichtlinearität zur Berechnung statischer, strukturmechanischer Aufgabenstellungen erarbeiten. Im Zuge dessen werden wir versuchen, eine lineare Verkoppelung der Normalkraft mit einem generalisierten Verzerrungsmaß für ein hyperelastisches Material einzubauen. Das ist dann doch nicht ganz so trivial, wie man zunächst meinen möchte. Manche Dinge sind außerdem nicht direkt vom eindimensionalen Stab auf ein Stabelement im dreidimensionalen Raum übertragbar, darauf wird im Beitrag an den nötigen Stellen immer wieder eingegangen. Und die Beitragsreihe soll vor allem eines zeigen: Erklärt man die Dinge der Reihe nach, dann ist die Thematik ohne großes Vorwissen für Interessierte recht einfach verständlich.

# Kinematik eines Stabelements

In der undeformierten Konfiguration eines Festkörpers - also eines Stabes - wird das differentielle Stabelement an der Position $X$ und mit der Länge $dX$ identifiziert.

Die Deformation wird durch eine eins-zu-eins Abbildung der Punktkoordinaten der undeformierten Konfiguration in die deformierte Konfiguration beschrieben.

![]({{ site.baseurl }}/images/DeformationStab.png "Deformation eines differentiellen Stabelements")

$x = \chi(X)$

Dies führt auf die Koordinate der deformierten Konfiguration. Der eindimensionale Deformationsgradient mit Bezug auf die unverformte Konfiguration beinhaltet die differentielle Längenänderung in einem Bereich rund um einen in der undeformierten Konfiguration identifizierten Punkt $X$.

$F=\frac{d\chi(X)}{dX} = \frac{dx}{dX}$

$dx = F dX$

Das deformierte Positionsfeld wird durch Addition eines Verschiebungsfeldes zum undeformierten Positionsfeld bestimmt. Daraus ergibt sich der Zusammenhang, dass der Deformationsgradient gleich dem Verschiebungsgradient plus eins ist.

$F=\frac{d(X+U)}{dX}=1+\frac{dU}{dX}$

Das Verhältnis aus deformierter zu undeformierter Länge des differentiellen Stabelements bezeichnen wir als Streckung $\lambda$, unabhängig davon ob eine Längenzu- oder abnahme vorliegt. Mit anderen Worten: Wir sparen uns also den Begriff der *Stauchung* und bringen diese in einer Art generalisierter Streckung unter.

$\lambda=\frac{dx}{dX}=\frac{dl}{dL}$

Damit ist die Deformation eines differentiellen Stabelements eindeutig charakterisiert.

**Hinweis**: Die direkte Berechnung der Streckung entlang eines im Raum liegenden Stabes ist auf diese Art nicht möglich! Hier muss über das Skalarprodukt $dl^2 = d\boldsymbol{x}^T d\boldsymbol{x}$ die quadratische Streckung berechnet werden (Satz von Pythagoras). Danach wird durch Ziehen der Wurzel die Stabstreckung ermittelt. Die Wurzel darf man aber nur *entlang des Stabes* ziehen, wenn man das so sagen will. Die Skalarprodukte der Stabvektoren sind die einzige Möglichkeit, um im Raum überhaupt eine Längenmessung etablieren zu können. Dafür ist auch kein Wurzelziehen nötig.

# Verzerrung

Die Verzerrung ist eine (nichtlineare) Funktion der Deformation, die im eindimensionalen Sinne monoton steigend im Sinne der Streckung sein soll. Für den Grenzfall unendlich großer und kleiner Streckungen soll sie idealerweise gegen $\pm \infty$ gehen. 

**An dieser Steller fragt man sich vielleicht**: Warum *soll* und nicht *muss*? Nun, *unser* Ziel einer strukturmechanischen Berechnung ist es ja, ein physikalisch stabiles Materialverhalten abzubilden. Aber was heißt denn konkret *physikalisch stabil*? Darunter versteht man eine monoton steigende Normalkraft bei zunehmender Streckung. Erfüllt nun bereits die Verzerrung bis hin zu den Limits unendlicher Streckung diese Anforderungen, so hat man bereits eine gute Basis für die konstitutive Materialmodellierung. Aber keine Garantie - dazu später mehr.

Um den undeformierten Zustand soll zudem die Steigung eins gelten, um im Falle infinitesimaler Streckungen die Ingenieurverzerrungen zu erhalten. 

Seth und Hill haben für eine generalisierte Verzerrung folgenden Vorschlag gemacht:

$e^{(k)} = \frac{1}{k} (\lambda^k-1)$

Wenn wir im weiteren Verlauf den Begriff Verzerrung verwenden, meinen wir immer diese generalisierten Verzerrungen. Erwähnenswert ist noch, dass für den Sonderfall $k=0$ die Seth-Hill-Verzerrungen auf die log. Verzerrung führt:

$e^{(0)} = ln(\lambda)$

Die Änderung der Verzerrung im Sinne der Streckung, mit anderen Worten die erste Variation der Verzerrung, berechnet sich zu:

$\delta e^{(k)} = \frac{\lambda^k}{\lambda}~\delta \lambda$ .

**Hinweis**: Auch hier gilt wieder: Die Streckung muss für Stäbe im dreidimensionalen Raum zunächst aus der Wurzel des Streckungsquadrats berechnet werden. Erst dann darf in Stabrichtung die (k)-Modifikation erfolgen. Einzig für den Sonderfall $k=2$ ist kein Wurzelziehen nötig, da die quadratische Länge des differentiellen Stabelements direkt aus dem Inprodukt der Stabvektoren resultiert. 



# Kinetik (Kräftegleichgewicht am deformierten System)

Wir betrachten ein differentielles Stabelement eines eindimensionalen Festkörpers (eines Stabs) in seiner deformierten Konfiguration und schneiden dieses frei. Im allgemeinen Belastungsfall treten am negativen und positiven Schnittufer voneinander verschiedene Normalkräfte auf. Die Normalkraft am negativen Schnittufer stellt den konstanten Grundanteil der Normalkraft dar und das positive Schnittufer beinhaltet zusätzlich differentielle Normalkraftänderungen entlang der deformierten Längskoordinate. Desweiteren wird eine Volumslast entlang der Längskoordinate mit vorerst beliebiger Abhängigkeit zur Längskoordinate angenommen. Das Kräftegleichgewicht am freigeschnittenen differentiellen Linienlement lautet:

$\sum N = 0 = -\sigma(x)~a(x) + \sigma(x)~a(x) + \frac{d\sigma(x)}{dx}~a(x) + b(x)~a(x)$

Nach Division durch die deformierte Querschnittsfläche bleibt

$\frac{d\sigma}{dx} + b = 0$

**Hinweis:** Das differentielle Kräftegleichgewicht wird im Mehrdimensionalen zur Vektorgleichung $\boldsymbol{div}(\boldsymbol{\sigma})+\boldsymbol{b} = \boldsymbol{0}$.

# Konstitution

Im letzten Schritt müssen wir noch eine Verbindung zwischen der Verzerrung und dem Kräftegleichgewicht herstellen, indem wir das Materialverhalten miteinbeziehen: Wir verheiraten die Verzerrung mit der Normalkraft über das konstitutive Materialgesetz, dem Ehevertrag wenn man so will. Wir fordern außerdem, dass dieses Materialgesetz im Sinne eines Potentials als Verzerrungsenergiefunktion vorliegen soll, was uns zum Begriff der Hyperelastizität führt.

### Hyperelastizität

Hyperelastizität bedeutet, dass eine Verzerrungsenergiefunktion je Einheit Masse existiert. Diese Verzerrungsenergiefunktion charakterisiert das Materialverhalten im Sinne der Deformation. Warum bezieht man sie je Einheit Masse? Weil die Masse die einzige Konstante eines Festkörpers während der Deformation darstellt. 

Masse? Wir sind eindimensional unterwegs, wie soll das klappen? Da ein eindimensionaler Stab nur durch eine Querschnittsfläche und einer Dichte eine Masse bekommt, muss die eindimensionale Betrachtungsweise an dieser Stelle zwangsläufig um eine Querschnittsfläche erweitert werden!

Das differentielle Potential der inneren Kräfte ist folglich das Produkt aus Verzerrungsenergiefunktion je Einheit Masse und differentieller Masse. Um die Potentialbeiträge der externen Kräfte kümmern wir uns derzeit nicht.

$d\Pi_{int} = \psi_m(e^{(k)})~dm$

Wie bereits erwähnt: Die Masse eines differentiellen Stabelements ist in einem geschlossenen System über den gesamten Deformationsvorgang hinweg konstant.

$dm = \rho~a~dx = \rho_0~A~dX$

## Verzerrungsenergiefunktion je Einheit unverformtes Volumen

Multipliziert man die Dichte der unverformten Konfiguration mit der Verzerrungsenergiefunktion je Einheit Masse, so führt das auf die Verzerrungsenergiefunktion je Einheit unverformtes Volumen. Für ein differentielles Stabelement ist das differentielle Volumen durch das Produkt aus unverformter Querschnittsfläche und differentieller Länge gegeben.

$d\Pi_{int} = \psi(e^{(k)})~A~dX$

Die Variation dieser Verzerrungsenergiefunktion nach der Deformation führt auf arbeitskonjugierte Paare aus Spannung und inkrementeller Verzerrung. Die Ableitung der Verzerrungsenergiefunktion nach der Verzerrung wird als Spannung identifiziert, weil das Paar einen inkrementellen Arbeitsausdruck der inneren Kräfte ergibt.

$\delta d\Pi_{int} = \delta\psi(e^{(k)})~A~dX$

$\delta d\Pi_{int} = \frac{d\psi(e^{(k)})}{de^{(k)}} \delta e^{(k)} ~A~dX$

Daraus erhält man die zur inkrementellen Verzerrungsgröße $\delta e^{(k)}$ zugehörige Spannung 

$s^{(k)}=\frac{d\psi(e^{(k)})}{de^{(k)}}$

## Lineare Spannungs-Verzerrungs-Relation

Um eine lineare Spannungs-Verzerrungs-Verkoppelung zu erhalten, muss die Verzerrungsenergiefunktion eine quadratische Funktion der Verzerrung sein. Der E-Modul dient hierbei als Materialparameter.

$\psi(e^{(k)}) = \frac{E}{2}~{e^{(k)}}^2$

$s^{(k)}=E~e^{(k)}$

# Wie kommt man mit all dem Wissen schlussendlich zur Stab-Normalkraft?

Soweit, so gut. Wir haben eine fiktive (k)-Spannung berechnet. Wie schaffen wir es jetzt, einen Zusammenhang zur Normalkraft herzustellen? Alles der Reihe nach. Die Normalkraft ist für ein differentielles Stabelement als Produkt aus Cauchy-Spannung und deformierter Querschnittsfläche gegeben (auch bekannt als Cauchysches Fundamentaltheorem).

$N = \sigma~a$

Durch partielle Integration des differentiellen Kräftegleichgewichts (wird eventuell in einem weiteren Beitrag genauer erläutert...) erhält man, dass die virtuelle Arbeit der inneren Kräfte je Einheit deformiertes Volumen als Produkt von Cauchy-Spannung und räumlichen Verschiebungsgradienten definiert ist. Das negative Vorzeichen kommt durch die partielle Integration zustande: Die Summe aller Randterme minus der Änderung im Inneren ist gleich Null. Diese Änderung im Inneren ist, naja, etwas salopp gesagt, die virtuelle Arbeit der inneren Kräfte.

$\delta dW_{int} = - \sigma~\frac{d\delta U}{dx}~dv$

$\delta dW_{int} = - \sigma~\delta\lambda \lambda^{-1}~a~dx$

Durch einen Vergleich

$s^{(k)}\lambda^k \delta\lambda\lambda^{-1}~A~dX = \sigma~\delta\lambda \lambda^{-1}~a~dx$

erhält man die Cauchy-Spannung in Abhängigkeit der Verzerrungsenergiefunktion

$\sigma = \frac{1}{J} s^{(k)}\lambda^k$.

## Normalkraft als Funktion der Verzerrung

...und in weiterer Folge der Streckung:

$N = s^{(k)}\lambda^{k-1} A$

$N = EA~e^{(k)}\lambda^{k-1}$

Man sieht also, dass die Normalkraft trotz aller Bemühungen **nicht**-linear mit der Verzerrung interagiert! Die Umrechnung des Verzerrungsinkrements auf das Inkrement der Streckung macht uns hier einen Strich durch die Rechnung. Das ist im Grunde aber nicht weiter schlimm, es ist eben so.

Da wir jetzt hinsichtlich der Kinematik, der Kinetik und der Konstitution alle Vorbereitungen getroffen haben, geht es im nächsten Beitrag weiter mit der Diskretisierung. Aber zuvor noch ein letztes Gedankenspiel: Wie müsste eine Verzerrungsenergiefunktion aussehen, die eine lineare Verkoppelung der Normalkraft mit der Verzerrung ermöglicht?

## Normalkraft als lineare Funktion der Verzerrung

Bei dieser Fragestellung gehen wir nicht vom Formelbau einer gegebenen Verzerrungsenergiefunktion aus, sondern von der gewünschten Formelarchitektur der Normalkraft:

$N = \frac{d\psi}{d\lambda} A = EA~e^{(k)}$.

Damit können wir die Verzerrungsfunktion durch einmaliges Integrieren nach der Streckung erzeugen. Die Integrationskonstante bestimmen wir im Anschluss mit der Forderung, dass im undeformierten Zustand keine Verzerrungsenergie auftreten soll.

$\psi = \int \frac{d\psi}{d\lambda} d\lambda = \int \frac{E}{k}(\lambda^k-1)~d\lambda$

Versucht man obige Gleichung zu integrieren, so erhält man eine Verzerrungsenergiefunktion, die nicht für alle beliebigen (k)-Exponenten konvex ist. Eine strikt konvexe Verzerrungsenergiefunktion erhalten wir nur dann, wenn wir zunächst den Sonderfall der log. Verzerrungen (k=0) annehmen, dann integrieren und erst zum Schluss die log. Verzerrung durch die allgemeine (k)-Verzerrung ersetzen. Schlussendlich muss man noch einen auftretenden Vorfaktor eliminieren und wir erhalten die Verzerrungsenergiefunktion, die eine lineare Verkoppelung der Normalkraft mit der Verzerrung erzeugt:

$\psi = \frac{E}{1+k}[\lambda (e^{(k)}-1)] + \psi_0$ 	mit 	$\psi_0 = \frac{1}{1+k}$.

Als Fleißaufgabe kann man jetzt wieder die fiktive (k)-Spannung berechnen. Hierzu muss man in der Verzerrungsenergiefunktion die Streckung durch die Verzerrung ausdrücken und einmal nach der Verzerrung ableiten.

$\lambda = (1+k~e^{(k)})^{1/k}$

$s^{(k)} = \frac{d\psi}{de^{(k)}} = \frac{E}{1+k}\left[\frac{\lambda}{\lambda^k} (e^{(k)}-1)+\lambda\right]$