# Was ist Compute: Die Rechenkraft der Cloud

## Aufgabe 1: Strategische Auswahl von Compute-Services für heterogene Workloads

### Analyse und Empfehlung der Compute-Services:

Die folgende Tabelle fasst die empfohlenen Compute-Services für jede Komponente zusammen, gefolgt von detaillierten Begründungen, Herausforderungen und Synergien.

Komponente    	Anforderungen	Empfohlener Compute-Service

1. Echtzeit-Analyse-Engine	  Extrem geringe Latenz, hohe Verfügbarkeit, unvorhersehbare Spitzenlasten	   Container auf Kubernetes (K8s)
___________________
2. Batch-Verarbeitungsdienst 	Rechenintensiv, flexible Startzeiten, Kosteneffizienz	Serverless Functions
___________________
3. Öffentliche API & Web-Frontend	Vorhersagbarer Traffic, schnelle Skalierbarkeit, reibungslose Bereitstellung	Container auf Kubernetes (K8s)
___________________

1. **Echtzeit-Analyse-Engine (Container auf Kubernetes)**

- Begründung für die Wahl:

Die Echtzeit-Analyse-Engine benötigt maximale Kontrolle über die Laufzeitumgebung, um geringe Latenz zu gewährleisten. Unvorhersehbare Spitzenlasten erfordern eine robuste, schnelle Skalierbarkeit.

* Performance (Latenz): Kubernetes (K8s) bietet dedizierte, langlebige Container-Instanzen, die im Gegensatz zu Serverless-Funktionen keine "Cold Starts" erleben. Die Anwendung ist immer betriebsbereit, was für Echtzeitverarbeitung entscheidend ist.

* Skalierbarkeit: K8s bietet exzellenten horizontalen Pod-Autoscaling (HPA) basierend auf CPU- oder Speicherauslastung, oft ergänzt durch fortschrittlichere Lösungen wie KEDA (Kubernetes Event-driven Autoscaling), die auf Ereignisströme reagieren können. Dies bewältigt unvorhersehbare Spitzenlasten effizient.

* Betriebsaufwand/Isolation: Container bieten eine gute Isolation und ermöglichen die Kapselung komplexer Abhängigkeiten der Analyse-Engine. Der Management-Overhead wird durch Managed K8s-Dienste (wie AWS EKS, Azure AKS, GCP GKE) minimiert.

* Zustandsverwaltung: Obwohl Microservices idealerweise zustandslos sind, können für Echtzeit-Engines manchmal Caching-Ebenen oder lokale Zustände für Performance-Optimierungen erforderlich sein. K8s bietet die Flexibilität, Persistent Volumes anzubinden oder Sidecar-Container für dedizierte Caching-Lösungen zu nutzen.

- Herausforderungen und Abwägungen:
* Herausforderung 1 (Komplexität): K8s bringt eine Lernkurve und operativen Overhead mit sich, selbst bei Managed Services. Das Team benötigt Know-how in der Cluster-Verwaltung, Monitoring und CI/CD-Pipelines für Container. Lösung: Investition in Schulungen und Nutzung von DevOps-Automatisierungstools.

* Herausforderung 2 (Kosten bei Grundlast): Im Gegensatz zu Serverless fallen für die K8s-Worker-Nodes (VMs) fixe Kosten an, auch wenn die Auslastung minimal ist. Lösung: Nutzung von Cluster-Autoscaling, das die Anzahl der zugrundeliegenden VMs bei geringer Nachfrage reduziert, um Kosten zu optimieren, während die Mindestkapazität für die Latenzanforderungen beibehalten wird.

* Kompromiss: Die Wahl von K8s bietet maximale Performance und Kontrolle auf Kosten eines höheren Management-Overheads und potenziell höherer Grundkosten im Vergleich zu Serverless.
________________________

2. **Batch-Verarbeitungsdienst (Serverless Functions)**

- Begründung für die Wahl:

Die Anforderungen dieses Dienstes – rechenintensiv, flexible Startzeiten und hohe Kosteneffizienz – passen perfekt zum Serverless-Modell (z.B. AWS Lambda, Azure Functions, GCP Cloud Functions).

* Kostenmodell: Serverless ist ideal für unregelmäßige, langlaufende Aufgaben. Sie zahlen nur für die tatsächliche Ausführungszeit der Funktion (Pay-per-Execution). Da die Jobs nur einmal täglich laufen, ist dies extrem kosteneffizient im Vergleich zur dauerhaften Bereitstellung von VMs oder K8s-Pods.

* Betriebsaufwand (Management-Overhead): Der Dienst ist vollständig verwaltet. Das Start-up muss sich nicht um Server-Wartung, Skalierung der Infrastruktur oder Patching kümmern. Der Fokus liegt rein auf dem Code der Batch-Logik.

* Skalierbarkeit: Wenn mehrere Berichte gleichzeitig ausgelöst werden müssen, skaliert der Cloud-Anbieter die Funktionen automatisch und parallel.

* Entwicklerproduktivität: Die Bereitstellung ist einfach; Entwickler pushen Code, und die Cloud-Plattform übernimmt den Rest.

- Herausforderungen und Abwägungen:

* Herausforderung 1 (Ausführungsdauer und Speicherlimits): Serverless-Funktionen haben oft maximale Laufzeitlimits (z.B. 15 Minuten bei AWS Lambda) und Speicherbegrenzungen. Komplexe, stundenlange Jobs könnten diese Limits sprengen. Lösung: Zerlegung des Batch-Jobs in kleinere, sequentielle Schritte, die über einen Orchestrierungsservice (z.B. AWS Step Functions) koordiniert werden. Dies ermöglicht es, jeden Schritt innerhalb der Limits auszuführen.

* Herausforderung 2 (Cold Starts bei seltener Nutzung): Wenn der Dienst nur einmal am Tag genutzt wird, kann der erste Aufruf einen "Cold Start" erleiden (die Plattform muss den Container laden). Lösung: Da die Startzeit flexibel ist, stellt dies kein kritisches Problem dar. Alternativ können "Provisioned Concurrency" oder "Warming"-Techniken angewendet werden, um die Latenz des Starts zu minimieren, was jedoch zusätzliche Kosten verursacht.

* Kompromiss: Maximale Kosteneffizienz und minimaler Betriebsaufwand werden eingetauscht gegen Einschränkungen bei der Ausführungsdauer und potenziellen Kaltstarts.
_________________

3. **Öffentliche API und Web-Frontend (Container auf Kubernetes)**

- Begründung für die Wahl:

Ähnlich wie die Analyse-Engine profitiert dieser Dienst von der robusten Orchestrierung und den langlebigen Instanzen von Kubernetes.

* Skalierbarkeit und Vorhersagbarkeit: K8s skaliert schnell und effizient, um den vorhersagbaren Tages- und Wochenzyklen des Traffics gerecht zu werden.

* Reibungslose Bereitstellung (DevOps): K8s ermöglicht fortschrittliche Deployment-Strategien wie Blue/Green Deployments, Canary Releases und Rollbacks. Dies minimiert Ausfallzeiten und Risiken bei der häufigen Bereitstellung neuer Features, was für ein schnell wachsendes Start-up entscheidend ist.

* Entwicklerproduktivität: Die Nutzung derselben Technologieplattform (K8s) für API/Frontend und die Analyse-Engine (Komponente 1) ermöglicht es den Entwicklerteams, Tools, Praktiken und interne Bibliotheken zu teilen.

* Performance: Langlebige Container vermeiden Latenz durch Cold Starts bei jedem API-Request.

- Herausforderungen und Abwägungen:

* Herausforderung 1 (Observability): Eine Microservices-Architektur mit K8s erfordert robuste Monitoring-, Logging- und Tracing-Lösungen (Observability Stack, z.B. Prometheus, Grafana, Jaeger), um den Zustand der verteilten Dienste zu verstehen. Lösung: Einführung standardisierter Observability-Tools frühzeitig im Entwicklungsprozess.

* Herausforderung 2 (API Gateway Management): Die Verwaltung des eingehenden Traffics, Load Balancing, Authentifizierung und Drosselung erfordert ein API Gateway oder einen Ingress Controller. Lösung: Einsatz eines dedizierten Cloud-API-Gateway-Dienstes oder eines K8s-spezifischen Ingress Controllers wie NGINX, Traefik oder Istio (Service Mesh). 

* Kompromiss: Die Nutzung von K8s bietet hohe Flexibilität und Kontrolle, erfordert jedoch mehr Konfigurations- und Wartungsaufwand als eine einfachere, vollständig verwaltete Web-App-Plattform.

**Synergien der Heterogenen Compute-Strategie**

Die Entscheidung für eine Kombination aus Kubernetes (für langlebige, latenzsensitive Dienste) und Serverless Functions (für ereignisgesteuerte, kosteneffiziente Batch-Jobs) bietet signifikante Vorteile gegenüber einer monolithischen Compute-Wahl:

1. "Right Tool for the Right Job": Jede Komponente nutzt die Stärken der jeweiligen Plattform optimal aus (Kostenfokus beim Batch, Performancefokus bei Echtzeit).

2. Kostenoptimierung: Durch die Nutzung von Serverless für den Batch-Dienst werden erhebliche Kosten gespart, die bei einer 24/7 laufenden K8s-Lösung anfallen würden.

3. Resilienz und Isolation: Das Ausfallen der Batch-Verarbeitung beeinträchtigt nicht die Echtzeit-Engine oder die API, da sie auf unterschiedlichen, isolierten Infrastrukturmodellen laufen.

4. Skalierbarkeit: Die Architekturen können unabhängig voneinander skaliert werden. Die K8s-Cluster skalieren mit dem User-Traffic, während die Serverless-Plattform Hunderte parallele Batch-Jobs ohne Zutun des Start-ups abwickeln kann.

5. Interaktion:
* Die Echtzeit-Analyse-Engine (K8s) schreibt analysierte Daten in eine zentrale Datenbank oder einen Data Lake.
* Der Batch-Verarbeitungsdienst (Serverless) liest diese Daten aus der Datenbank/dem Data Lake, aggregiert sie und speichert die Ergebnisse.
* Die Öffentliche API (K8s) liest die aggregierten Ergebnisse aus der Datenbank und stellt sie dem Web-Frontend bereit.
Diese flexible, heterogene Strategie ermöglicht es dem Start-up, agil zu bleiben, Kosten zu kontrollieren und gleichzeitig die spezifischen, anspruchsvollen Performance-Anforderungen jeder Microservice-Komponente zu erfüllen.
