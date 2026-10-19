---
layout: post
title: "Masterarbeit: Vergleichende Analyse von Agentic-Process-Automation-Tools"
date: 2026-05-01
tags: [Masterarbeit, Agentic Process Automation]
---

Ich habe mit meiner Masterarbeit begonnen. Sie beschäftigt sich mit **Agentic Process Automation (APA)**: Ich vergleiche ausgewählte APA-Tools anhand eines eigenen Kriterienkatalogs und praktischer Hands-on-Tests. Hier ist die Einleitung.

---

## Motivation

Die Automatisierung von Geschäftsprozessen gilt als zentraler Treiber der digitalen Transformation von Unternehmen. Sie soll die Effizienz steigern, Kosten senken und zugleich die Qualität von Prozessen verbessern (Reijers & Mansar, 2005, S. 302 f.). Bisher dominierten regelbasierte Ansätze wie Robotic Process Automation (RPA). Diese führen strukturierte Routineaufgaben zuverlässig aus, stoßen bei unstrukturierten Eingaben und Ausnahmefällen jedoch an ihre Grenzen (Syed et al., 2020, S. 9).

Derzeit zeichnet sich ein grundlegender Wandel hin zu integrierten, intelligenten Automatisierungsplattformen ab. Gartner erwartet, dass bis 2030 rund 70 % der Unternehmen auf konsolidierte Automatisierungsplattformen umstellen werden. Solche Plattformen orchestrieren Geschäftsprozesse, KI-Agenten, Bots, APIs und menschliche Interaktionen gemeinsam (Gartner, 2025).

In diesem Kontext entsteht mit Agentic Process Automation (APA) eine neue Generation von Automatisierungstechnologien. Dabei verfolgen KI-basierte Agenten eigenständig Ziele, treffen Entscheidungen und orchestrieren Aktionen über verschiedene Systeme hinweg ([UiPath, Agentic Automation](https://www.uipath.com/automation/agentic-automation)). Der Schwerpunkt verschiebt sich damit von der starren Ausführung vorab modellierter Abläufe hin zu einer zielorientierten Prozessausführung, in der deterministische Workflow-Logik und agentische Autonomie miteinander verbunden werden.

Für Unternehmen eröffnet sich daraus ein erhebliches Potenzial. Zugleich entsteht ein konkreter Entscheidungsbedarf: Welche der am Markt verfügbaren Plattformen eignet sich für den produktiven Einsatz, und anhand welcher Kriterien lässt sich dies belastbar beurteilen? An dieser Stelle setzt die Arbeit an.

## Problemstellung

Der Markt für APA-Tools ist gegenwärtig durch mehrere Herausforderungen geprägt:

- **Begriffsunschärfe:** APA ist bislang kein normierter Begriff. Anbieter verwenden unterschiedliche Definitionen und Marketingbezeichnungen wie *AI Agents*, *Autonomous Workflows*, *Agentic Orchestration* oder *AI Automation*. Dadurch werden sowohl eine einheitliche wissenschaftliche Einordnung als auch die Vergleichbarkeit von Produktversprechen erschwert.
- **Heterogene Architekturen und Funktionsumfänge:** Die verfügbaren Tools unterscheiden sich erheblich, unter anderem in ihren Agentenfähigkeiten, im zugrunde liegenden Orchestrierungsparadigma und in der Integrationsfähigkeit in bestehende Systemlandschaften.
- **Unklare Leistungsfähigkeit und Robustheit:** Viele Anbieter versprechen eine autonome, zielorientierte Prozessausführung durch KI-Agenten. Ob diese Systeme unter realistischen Bedingungen zuverlässig und konsistent arbeiten, bleibt jedoch häufig offen, etwa bei variierenden Eingaben, bei Fehlern oder bei der wiederholten Ausführung desselben Vorgangs.
- **Vertrauenswürdigkeit agentischer Systeme:** Erhalten Agenten Zugriff auf kritische Systeme, Daten oder Geschäftsprozesse, gewinnen Governance-, Sicherheits- und Kontrollmechanismen erheblich an Bedeutung. Häufig ist unklar, wie ausgereift diese Mechanismen tatsächlich sind, etwa die Transparenz und Nachvollziehbarkeit von Agentenentscheidungen oder die Widerstandsfähigkeit gegenüber manipulativen Eingaben. Damit bleibt auch offen, inwieweit ein Einsatz in produktiven Umgebungen verantwortbar ist.

Es fehlt somit ein systematischer, am Stand der Technik ausgerichteter Bewertungsansatz, der APA-Tools nicht allein auf Basis von Herstellerangaben, sondern anhand praktischer Erprobung vergleichbar macht.

## Zielsetzung

Ziel der Arbeit ist eine vergleichende Analyse ausgewählter, repräsentativer APA-Tools. Im Mittelpunkt stehen die Identifikation und Ableitung geeigneter Bewertungskriterien auf Basis des Standes der Technik. Dazu werden zunächst die zentralen technologischen Komponenten und Architekturmerkmale von APA-Systemen herausgearbeitet und begrifflich eingeordnet.

Auf dieser Grundlage entsteht ein strukturierter Kriterienkatalog, mit dem die ausgewählten Tools im Rahmen einer Nutzwertanalyse systematisch gegenübergestellt werden. Die Bewertung stützt sich hauptsächlich auf Hands-on-Tests, in denen ein standardisierter Testfall in allen betrachteten Tools implementiert und mehrfach ausgeführt wird.

Das Ergebnis ist eine methodisch fundierte Nutzwertanalyse sowie ein praxisnaher Bewertungsansatz, der bei der Einordnung von APA-Technologien unterstützen kann.

## Forschungsfragen

1. **RQ1:** Welche technologischen Architekturmerkmale kennzeichnen Agentic-Process-Automation-Systeme?
2. **RQ2:** Welche Kriterien lassen sich aus Literatur, Standards und Anbieterunterlagen zur Bewertung von APA-Tools ableiten?
3. **RQ3:** Wie unterscheiden sich ausgewählte APA-Tools hinsichtlich technischer Fähigkeiten?
4. **RQ4:** Wie unterscheiden sich ausgewählte APA-Tools hinsichtlich operativer Leistungsfähigkeit?
5. **RQ5:** Wie unterscheiden sich ausgewählte APA-Tools hinsichtlich Governance und Sicherheit?

## Aufbau der Arbeit

Die Arbeit gliedert sich in sechs Kapitel.

- **Kapitel 2** erläutert die Grundlagen von AI Agents, Multi-Agent-Systemen und Agentic AI und ordnet APA ein. Anschließend werden Orchestrierungsparadigmen und Architekturmerkmale von APA-Systemen behandelt (RQ1).
- **Kapitel 3** analysiert den Stand der Technik und entwickelt einen Kriterienkatalog (RQ2) mit fünf Bereichen: Agentenfähigkeiten, Workflow-Orchestrierung, Integrationsfähigkeit, Governance und Observability sowie operative Leistungsfähigkeit. Er bildet die Grundlage der anschließenden Nutzwertanalyse.
- **Kapitel 4** begründet die Plattformauswahl und beschreibt Testfall, Testumgebungen sowie Testdurchführung. Anschließend werden die Kriterien operationalisiert, skaliert und gewichtet sowie Auswertungsmethodik und Limitationen erläutert.
- **Kapitel 5** präsentiert die Bewertungsergebnisse (RQ3–RQ5), aggregiert sie zu Gesamtnutzwerten und überprüft deren Stabilität mittels Sensitivitätsanalyse.
- **Kapitel 6** diskutiert die Ergebnisse im Hinblick auf die Forschungsfragen, reflektiert Beitrag und Limitationen der Arbeit und gibt einen Forschungsausblick.

Die Nutzwertanalyse ermöglicht den systematischen Vergleich mehrerer Alternativen anhand gewichteter Kriterien, deren Bewertungen zu Gesamtnutzwerten aggregiert werden. Die resultierende Rangfolge hängt von den festgelegten Gewichtungen und Bewertungen ab und stellt daher keine objektiv beste Lösung dar (Zangemeister, 1976, S. 45; Belton & Stewart, 2002, S. 2 f.).

---

Ich werde hier über den Fortschritt der Arbeit berichten.
