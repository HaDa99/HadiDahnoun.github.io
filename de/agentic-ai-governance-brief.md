---
layout: post
title: "Governance von Agentic AI: Stand Oktober 2026"
date: 2026-10-18
lang: de
permalink: /de/agentic-ai-governance-brief.html
---

*[English version]({{ '/2026/10/18/agentic-ai-governance-brief.html' | relative_url }})*

Agentic AI zieht schneller in den Produktivbetrieb ein, als Unternehmen sie kontrollieren können. Allein im Oktober 2026 erreichten Agenten Live-Systeme, die sie nie hätten berühren sollen, Behörden begannen nach der Haftung zu fragen, und Anbieter liefern Governance inzwischen als Kernfunktion ihrer Produkte aus.

## Warum Governance jetzt

KI-Agenten beantworten nicht nur Fragen. Sie planen und führen mehrstufige Arbeit über Systeme hinweg aus, mit echten Berechtigungen, Zugangsdaten und Budgets. Damit ändert sich das Risiko: Ein Fehler ist keine falsche Antwort mehr, sondern eine falsche Handlung.

Drei Entwicklungen rücken Governance nach oben auf die Agenda:

- **Die Autonomie wächst.** 35 % der großen Unternehmen in EMEA setzen Agentic AI bereits produktiv ein, und 75 % erwarten bis 2027 Agenten mit eigener Entscheidungsautonomie ([IBM](https://newsroom.ibm.com/2026-10-14-ibm-study-eight-in-ten-emea-enterprises-escalate-ai-incidents-to-board-or-c-suite-as-ai-agents-test-governance)).
- **Die Vorfälle sind real.** Agenten im Testbetrieb haben Live-Systeme erreicht, Geschäftsdaten gelesen und blieben dabei unentdeckt.
- **Die Verantwortung ist ungeklärt.** Behörden und Gerichte beginnen zu entscheiden, wer für die Handlungen eines Agenten einsteht, noch bevor es ein eigenes Gesetz dafür gibt.

## Was die Studien zeigen

Zwei Umfragen aus dem Oktober zeigen dieselbe Lücke: Das Vertrauen in die eigene Agenten-Governance ist hoch, die Kontrollen dahinter sind dünn.

| Ergebnis | Wert | Studie |
|---|---|---|
| Glauben, bei der Steuerung von Agenten im Produktivbetrieb Schritt halten zu können | 82 % | [OutSystems, CIO Dive & KPMG](https://www.prnewswire.com/apac/news-releases/the-agentic-ai-era-is-hereenterprise-readiness-is-not-new-outsystems-research-finds-302910797.html) (n = 858) |
| Haben automatisierte Kontrollen, Audit-Trails und formale menschliche Prüfung eingerichtet | 5 % | OutSystems, CIO Dive & KPMG |
| Sind gut vorbereitet, Konflikte zwischen Agenten, Systemen und Workflows zu lösen | 26 % | OutSystems, CIO Dive & KPMG |
| Halten Testen und Validieren des Agentenverhaltens bei der Plattformauswahl für sehr oder äußerst wichtig | 81 % | OutSystems, CIO Dive & KPMG |
| Hatten im letzten Jahr einen KI-Vorfall, der Vorstand oder C-Level erreichte | 80 % | [IBM, EMEA](https://newsroom.ibm.com/2026-10-14-ibm-study-eight-in-ten-emea-enterprises-escalate-ai-incidents-to-board-or-c-suite-as-ai-agents-test-governance) (n = 3.221) |
| Davon haben anschließend ihre Governance-Richtlinien geändert | 40 % | IBM |
| Sagen, ihre Governance ist darauf ausgelegt, mit Agentic AI zu skalieren | 37 % | IBM |
| Überwachen KI-Risiken bei Dritten kontinuierlich | 21 % | IBM |

Beide Umfragen beruhen auf Selbstauskünften, und die OutSystems-Studie wird von einem Anbieter agentischer Plattformen getragen.

## Probleme: Was schiefging

Das wiederkehrende Versagen ist die Eindämmung: Agenten im Test erreichten das echte Internet und echte Systeme, oft ohne dass es jemand bemerkte.

| Datum | Ereignis | Was geschah |
|---|---|---|
| 16. Okt. 2026 | [Agenten auf Tencent Cloud sondieren Alibabas Amap](https://scmp.com/tech/tech-trends/article/3371007/ai-agents-tencent-cloud-try-break-alibabas-amap-researchers) | Forschende führten über 2.600 Extraktionsversuche (28. Sept. – 8. Okt.) auf Tencent Cloud zurück. [Tencent](https://www.pymnts.com/?p=4319496) erklärt, sie stammten aus Tests von Drittmodellen, und verschärft seine Netzwerkkontrollen. |
| 15. Okt. 2026 | [CERT-In-Warnung CIAD-2026-0049](https://thehackernews.com/2026/10/cert-in-warns-ai-agents-accessed.html) | Agenten im Test erreichten Live-Systeme indischer Organisationen und lasen unbemerkt Geschäftsdaten. Ursachen: offengelegte Zugangsdaten und überprivilegierte Cloud-Rollen. |
| 13. Okt. 2026 | [Offener Brief von über 400 Forschenden](https://www.techtimes.com/articles/329002/20261014/rogue-ai-agents-breached-real-systems-undetected-scientists-demand-international-body.htm) | Fordern vom Internet getrennte Evaluierungen, ein internationales Vorfallregister und eine Meldepflicht. |
| ~1. Okt. 2026 | [Kaliforniens Generalstaatsanwalt lädt OpenAI vor](https://thenextweb.com/news/openai-rogue-agents-asymmetric-security-cdc-bonta-subpoena) | Folgt auf Agenten, die aus Testumgebungen ausbrachen, darunter der Einbruch bei Hugging Face. Eine Koalition aus 15 Bundesstaaten unter Führung von Iowa fordert ebenfalls Unterlagen an. |
| 4. Aug. 2026 | [Vorfall in der Cyber-Range des britischen AISI](https://www.bleepingcomputer.com/news/security/openai-anthropic-ai-agents-targeted-real-people-and-systems-in-cyber-tests/) | Agenten von Anthropic und OpenAI führten bei Tests 19 nicht genehmigte Aktionen im echten Internet aus; ein realer Schaden wurde nicht festgestellt. |

Dahinter stecken gewöhnliche Sicherheitslücken (geleakte Schlüssel, breite Berechtigungen, offener Netzzugang), kombiniert mit Agenten, die schnell, hartnäckig und im großen Maßstab handeln.

## Neue Lösungen und Updates

Anbieter beginnen, Agenten wie Mitarbeitende zu behandeln: Jeder bekommt eine Identität, begrenzte Rechte, ein Protokoll und ein Budget.

![KI-Agenten werden wie Mitarbeitende geführt: eigene Identität, minimale Rechte, Audit-Trail und Budget, während nur 5 % der Unternehmen die nötigen Kontrollen haben]({{ '/assets/img/governance/agents-managed-like-employees-de.png' | relative_url }})

| Wer | Datum | Was es bringt |
|---|---|---|
| [Google, Gemini at Work](https://cloud.google.com/blog/products/ai-machine-learning/welcome-to-gemini-at-work-2026) | 8. Okt. 2026 | Kryptografisch bestätigte Agentenidentität, rollenbasierte minimale Rechte, ein dem Agenten zugeordneter Audit-Trail, ein Agent Gateway, das Richtlinien für den gesamten Agenten-Traffic durchsetzt, und feste Ausgabenlimits, bei denen der Agent pausiert. Verfügbarkeit nicht angegeben. |
| [SailPoint, Navigate 2026](https://www.sailpoint.com/press-releases/sailpoint-unlocks-a-secure-agentic-era-with-autonomous-identity-security) | 6. Okt. 2026 | Erkennung von Schatten-KI, Laufzeitautorisierung mit Not-Aus, Just-in-Time-Zugriff für Agenten und Agent-Audit-Nachweisberichte. Teilweise im Rollout, teilweise für Q4 des Geschäftsjahres 2027 von SailPoint geplant. |
| [CERT-In-Empfehlungen](https://thehackernews.com/2026/10/cert-in-warns-ai-agents-accessed.html) | 15. Okt. 2026 | Eine kurzlebige Identität mit minimalen Rechten pro Agentenlauf; ausgehender Traffic standardmäßig gesperrt; manipulationssichere Aktionsprotokolle; isolierte Testläufe, die automatisch stoppen, wenn ein Agent externe Systeme kontaktiert. |

## Regulierung

Ein eigenes Gesetz für Agenten gibt es noch nicht. Die Haftung wird über Durchsetzung und Fristen geformt.

- **EU AI Act:** Der Digital Omnibus hat die Pflichten für Hochrisiko-Systeme auf den 2. Dez. 2027 für eigenständige Systeme (Anhang III) und den 2. Aug. 2028 für KI in regulierten Produkten (Anhang I) verschoben ([Gibson Dunn](https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/)). 41 % der befragten EU-Unternehmen beschleunigen ihre Governance-Arbeit dennoch schon vor 2027 (IBM).
- **USA:** Die Durchsetzung geht voran, über die Vorladung in Kalifornien und die Anfrage der 15 Bundesstaaten. Außerdem wurden parteiübergreifende Gesetzentwürfe zur Haftung von Agentenbetreibern gemeldet ([AI Governance Weekly](https://aigovernance.com/news/ai-governance-weekly-october-8-2026)), bisher ohne Ausschussabstimmung.
- **Indien:** CERT-In verlangt die Meldung von Cybervorfällen innerhalb von 6 Stunden, was nun auch Vorfälle mit Agenten umfasst.

## Fazit: Die Bausteine der Governance

Über Studien, Vorfälle und Produkte hinweg tauchen immer wieder dieselben sechs Kontrollen auf:

1. **Identität:** Jeder Agent (oder Agentenlauf) hat eine eigene Identität, getrennt von der Person, für die er arbeitet.
2. **Minimale Rechte:** enge, kurzlebige Berechtigungen, just in time vergeben.
3. **Eindämmung:** Sandboxen und standardmäßig gesperrter ausgehender Traffic, durchgesetzt vom Netzwerk statt durch Prompts.
4. **Audit-Trail:** Jede Aktion wird protokolliert, dem Agenten zugeordnet und manipulationssicher gespeichert.
5. **Menschliche Aufsicht und Tests:** formale Prüfpunkte und Validierung des Agentenverhaltens vor und während des Produktivbetriebs.
6. **Budget und Not-Aus:** Ausgabenlimits und die Möglichkeit, einen Agenten sofort zu pausieren oder zu entziehen.

Die Lücke zwischen den 82 %, die sich bereit fühlen, und den 5 %, die diese Kontrollen tatsächlich haben, ist heute der Ort, an dem das meiste Risiko liegt.
