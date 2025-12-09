## Aufgabe 1: Grundlagen des Cloud Computings verstehen

### 1.1 Das Konzept des Cloud Computings

+ Definiere Cloud Computing in eigenen Worten. Was sind die wesentlichen Merkmale? 

Cloud Computing bedeutet, dass Computerressourcen wie Speicher und Rechenleistung       über das Internet bereitgestellt werden. Unternehmen können schnell zusätzliche Ressourcen hinzufügen und müssen sich nicht um die Infrastruktur kümmern.
Es gibt öffentliche, private und hybride Clouds. Wichtige Faktoren sind Sicherheit und Datenschutz.

+ Nenne und beschreibe die fünf Charakteristika des Cloud Computings.
   
    1. Self-Service auf Abruf
Cloud-Computing-Anbieter stellen APIs bereit, auf die Benutzer zugreifen, um neue Ressourcen anzufordern oder vorhandene Ressourcen bei Bedarf zu skalieren. Teams können ihre Infrastrukturbereitstellung mit Tools für Infrastructure as Code wie Terraform und Ansible auf einfache Weise automatisieren.
   2. Breiter Netzwerkzugang
Der Standort der physischen Hardware ist ein erhebliches Problem bei der Bereitstellung der optimalen Endbenutzererfahrung. Cloud Computing ist hierfür ein Segen, da es global verteilte physische Hardware bietet, die es Unternehmen ermöglicht, standortbezogene Hardware strategisch bereitzustellen.
   3. Ressourcen-Pooling
Rechenressourcen in einer Cloud-Infrastrukturplattform werden dynamisch aufgeteilt und bei Bedarf zugewiesen. Da die physischen Rechner eines Cloud-Hosts dynamisch bereitgestellt und von mehreren Mandanten gemeinsam genutzt werden, ist Cloud-Hardware durch und durch für eine maximale Nutzung optimiert.
   4. Schnelle Elastizität
Cloud-Infrastrukturen können dynamisch wachsen und schrumpfen, sodass die Benutzer eine automatische Skalierung ihrer Rechenressourcen je nach Traffic anfordern können. Die Elastizität kann pro Rechner erfolgen mit einer Erhöhung der Ressourcen zur Maximierung der verfügbaren Rechenressourcen oder auf Basis mehrerer Rechner mit einer automatischen Skalierung einer Anwendung auf mehrere vernetzte Maschinen.
   5. Service nach Maß
Anbieter von Cloud-Infrastrukturen stellen detaillierte Nutzungsmetriken zur Verfügung, die zur Kommunikation der Nutzungskosten verwendet werden. Beispielsweise gibt Amazon Web Services (AWS) die Nutzung pro Servicekategorie in stündlichen oder täglichen Einzelposten an. Cloud-Serviceanbieter verwenden im Allgemeinen ein nutzungsabhängiges Abrechnungsmodell, bei dem Kunden anhand der erhobenen Messdaten die genaue Menge der verwendeten Computerressourcen in Rechnung gestellt wird.

### 1.2 On-Premises vs. Cloud
+ Erläutere den Unterschied zwischen einer On-Premises-Infrastruktur und der Cloud.
Unterschiede zwischen On-Premise-Lösungen und Cloud Lösungen liegen im Lizenzmodell und im Betrieb. Während bei Cloud Anbietern grundsätzlich Mietlizenzen erworben werden, können On-Premises-Lösungen sowohl gekauft als auch gemietet werden.
Cloud Anbieter bieten ihre Software als Service an, das heißt die Installation, die Serverstruktur sowie die Administration liegt in der Verantwortung des Providers. Der Betrieb bei On-Premise hingegen liegt komplett in der Eigenverantwortung der Unternehmen, die diese erwerben.
Die Vorteile der Nutzung einer Cloud Lösung sind:
Kosten können gering gehalten werden durch „Pay-as-you-go“-Modell
Keine AnschaffungskostenOhne voriges Investment steht die Cloud-Lösung direkt nach der Anmeldung zur Verfügung.
Skalierbarkeit: Ressourcen lassen sich einfach dazubuchen, so dass sie immer genügend Speichkapazität haben, auch das hinzufügen neuer Benutzerkonten ist schnell und einfach umgesetzt
Hohe Verfügbarkeit durch Provider garantiert
Geräteunabhängiger Zugang
Wartung und Updates sind als Service inklusive
Vorteile von On-Premises Lösungen:
Datensicherheit – volle Kontrolle über die eigenen Daten
Da es sich bei On-Premise um einen eigenverantwortlich betriebene Server handelt,          die nur einer bestimmten Nutzer-Gruppe zur Verfügung steht, werden Daten nicht mit   einem Drittanbieter geteilt, weshalb dieses Thema weniger kritisch ist.
Zum Thema Datensicherheit und Datenschutz im Falle einer Cloud Software gleich mehr.
Größere Flexibilität durch individuelle AnpassungsmöglichkeitenSowohl die Anpassung der auf dem Server betriebenen Programmen als auch die Anpassung der Datenschutzanforderungen liegen in der Hand des Server-Inhabers und können deshalb nach eigenen Bedürfnissen angepasst und somit besser individualisiert werden.
Eigene IT-InfrastrukturDas Unternehmen kann komplett unabhängig von Server-Anbietern agieren und sich von der eigenen IT-Abteilung die Infrastruktur maßschneidern lassen.
Auch bei Ausfall des Internets Zugriff auf die firmeneigenen DatenDurch den direkten Zugriff auf den hauseigenen Server, ist es Ihnen möglich trotz Internet-Ausfalls auf firmeneigenen Daten zuzugreifen.

### 1.3 Übersicht der Service-Modelle 

+ Beschreibe die drei Haupt-Service-Modelle

1.Infrastructure as a Service
Infrastructure as a Service (IaaS) ist eine grundlegende Cloud-Serviceschicht, die es Unternehmen ermöglicht, IT-Infrastruktur – Server, Speicher, Netzwerke, Betriebssysteme – von einem Cloud-Anbieter zu mieten. IaaS ermöglicht es Benutzern, die benötigten Ressourcen aus physischen Raw-Server-Lagern zu reservieren und bereitzustellen. Darüber hinaus ermöglicht IaaS Benutzern die Reservierung vorkonfigurierter Computer für spezielle Tasks, beispielsweise Load Balancer, Datenbanken, E-Mail-Server und verteilte Warteschlangen.
DevOps-Teams können IaaS als zugrunde liegende Plattform verwenden, aus der sich eine DevOps-Toolkette erstellen lässt, die die Verwendung verschiedener Tools von Drittanbietern umfassen kann.

2.Platform as a Service
Platform as a Service (PaaS) ist eine auf IaaS basierende Cloud-Infrastruktur, die Ressourcen zum Erstellen von Tools und Anwendungen auf Benutzerebene bereitstellt. Sie umfasst die zugrunde liegende Infrastruktur, einschließlich Rechen-, Netzwerk- und Speicherressourcen, sowie Entwicklungstools, Datenbankverwaltungssysteme und Middleware.
PaaS nutzt IaaS, um automatisch die Ressourcen zuzuweisen, die für den Betrieb eines sprachbasierten Technologie-Stack erforderlich sind. Beliebte Sprach-Tech-Stacks sind Ruby On Rails, Java Spring MVC, MEAN und JAM Stacks. PaaS-Kunden können dann einfach ein Artefakt ihres Anwendungscodes hochladen, das automatisch in der Infrastruktur des PaaS bereitgestellt wird. Dies ist ein neuartiger und leistungsstarker Workflow, der es Teams ermöglicht, sich vollständig auf ihren spezifischen Geschäftsanwendungscode zu konzentrieren und sich nicht um Hosting- und Infrastrukturprobleme zu kümmern. PaaS übernimmt automatisch die Skalierung und Überwachung der Infrastruktur, um Ressourcen je nach beobachteter Traffic-Last zu vergrößern oder zu verringern.

3.Software as a Service
Software as a Service (SaaS) liefert Softwareanwendungen über das Internet auf Abruf und in der Regel im Abonnement. Die Cloud-Anbieter hosten und verwalten die Anwendung und kümmern sich bei Bedarf um Software-Upgrades und Sicherheitspatches. Beispiele für SaaS sind CRM-Systeme, Webmail-Anwendungen, Produktivitätstools wie Jira und Confluence, Analysetools, Überwachungstools, Chatanwendungen und mehr.

4.Function as a Service
Function as a Service (FaaS) ist ein Cloud-Computing-Service, der eine Plattform bietet, auf der Kunden Anwendungen entwickeln, ausführen und verwalten können. Entwickler müssen somit nicht mehr selbst die erforderliche Infrastruktur für die Entwicklung und Einführung einer App aufbauen und warten. Cloud-Anbieter bieten Cloud-Ressourcen an, führen einen Codeblock aus, geben das Ergebnis zurück und zerstören dann die verwendeten Ressourcen.


### 1.4 Vorteile und Herausforderungen der Cloud-Einführung

+Sammle die wichtigsten Vorteile, die Unternehmen durch die Einführung von Cloud Computing erzielen können
Kürzere Produkteinführungszeit
Sie können neue Instanzen in Sekundenschnelle einrichten oder auslaufen lassen. Entwickler können so die Entwicklung durch schnelle Bereitstellungen beschleunigen. Cloud-Computing unterstützt Innovationen durch die einfache Erprobung neuer Ideen und die Entwicklung neuer Anwendungen ohne Hardwareeinschränkungen oder langsame Beschaffungsprozesse.
Skalierbarkeit und Flexibilität
Cloud-Computing bietet Ihrem Unternehmen mehr Flexibilität. Sie können Ressourcen und Speicher schnell skalieren, um den Geschäftsanforderungen gerecht zu werden, ohne in physische Infrastruktur investieren zu müssen.
Unternehmen müssen nicht für die Infrastruktur bezahlen, die für ihre höchsten Anforderungen erforderlich ist, und auch keine Kosten dafür tragen. Ebenso können sie schnell herunterskaliert werden, wenn Ressourcen nicht verwendet werden.  
Kosteneinsparungen
Für welches Cloud-Dienstmodell Sie sich entscheiden, Sie zahlen nur für die Ressourcen, die Sie tatsächlich nutzen. So vermeiden Sie das Überladen und die Überdimensionierung von Rechenzentren und Ihre IT-Teams haben mehr Zeit, sich auf strategische Aufgaben zu konzentrieren. 
Bessere Zusammenarbeit
Mit Cloud Storage können Sie jederzeit und von überall aus Daten verfügbar machen. Anstatt an einen Standort oder ein bestimmtes Gerät gebunden zu sein, können Nutzer von jedem Gerät aus auf Daten aus der ganzen Welt zugreifen – sofern sie eine Internetverbindung haben.
Erweiterte Sicherheit
Trotz der weitverbreiteten Wahrnehmung kann Cloud Computing Ihren Sicherheitsstatus aufgrund der Tiefe und Breite der Sicherheitsfeatures, der automatischen Wartung und der zentralen Verwaltung verbessern.
Renommierte Cloud-Anbieter beschäftigen außerdem führende Sicherheitsexperten und setzen modernste Lösungen ein, um für einen robusten Schutz zu sorgen. 
Schutz vor Datenverlust
Cloud-Anbieter bieten Features zur Sicherung und Notfallwiederherstellung an. Das Speichern von Daten in der Cloud statt lokal kann dabei helfen, Datenverluste im Notfall zu vermeiden, z. B. Hardwarefehler, schädliche Bedrohungen oder sogar einfache Nutzerfehler. 

+Identifiziere und beschreibe die größten Herausforderungen oder Bedenken, die Unternehmen bei der Migration in die Cloud haben könnten
Die größten Herausforderungen bei der Cloud-Migration sind Sicherheit und Compliance (Datenschutz, DSGVO-Konformität), Abhängigkeit vom Anbieter, Kostenkontrolle (unerwartete Gebühren), Datenmigration (Komplexität, Bestandsaufnahme, Bandbreite), Leistungsprobleme (Latenz, Geschwindigkeit), Kompatibilität der Infrastruktur sowie die mangelnde interne Expertise für Planung, Ausführung und Verwaltung, was oft zu unklaren Strategien und Ausfallzeiten führt. 
## Aufgabe 2: Globale Infrastruktur der Cloud erkunden

### 2.1 Was globale Infrastruktur im Cloud Computing bedeutet

Globale Cloud-Infrastruktur bedeutet, dass große Cloud-Anbieter (wie AWS, Azure, Google Cloud) physische Rechenzentren mit Servern, Speichern und Netzwerken weltweit unterhalten und diese Ressourcen über das Internet als skalierbare Dienste (IaaS, PaaS, SaaS) bereitstellen, was Unternehmen ermöglicht, Anwendungen weltweit mit geringer Latenz und hoher Verfügbarkeit zu betreiben, ohne eigene Hardware zu besitzen. Es geht um die weltweite Verteilung von Rechenleistung, Speicher und Netzwerk, um Benutzern eine nahtlose, leistungsstarke und kosteneffiziente Nutzung über geografische Grenzen hinweg zu ermöglichen. 
### 2.2 Regionen, Availability Zones (Verfügbarkeitszeiten) und Rechenzentren

Im Konzept der Cloud-Infrastruktur gibt es den Begriff der „Region“, d. h. einen physischen Ort auf der Welt, an dem wir Rechenzentren zusammenfassen. Wir bezeichnen jede Gruppe von logischen Rechenzentren als Verfügbarkeitszone (Availibility Zone, abgekürzt AZ). Normalerweise besteht jede Region aus mehreren, isolierten und physisch getrennten AZs innerhalb eines geografischen Gebiets.
Eine Cloud-Region ist eine Gruppe von Geräten, die sich in einem separaten Rechenzentrum befinden. Jede Region verfügt über einen von anderen Regionen getrennten Anschluss an Stromleitungen, eine autonome Stromversorgung und Kühlung sowie über dedizierte Kommunikationskanäle. Jede Region ist von Hardware- und Softwarefehlern in anderen Regionen der Cloud isoliert.
Jede AZ verfügt über eine unabhängige Stromversorgung, Kühlung und physische Sicherheit und ist über redundante Netzwerke mit niedriger Latenz verbunden. Cloud-Kunden, die Wert auf hohe Verfügbarkeit legen, können ihre Anwendungen so konzipieren, dass sie in mehreren AZs laufen, um eine noch größere Fehlertoleranz zu erreichen. Die Regionen der SIM-Cloud-Infrastruktur erfüllen die höchsten Anforderungen an Sicherheit, Compliance und Datenschutz.


