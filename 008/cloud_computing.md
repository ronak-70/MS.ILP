# Aufgabe 1: Cloud Services – Architektur und Strategie

### 1.1 Dienstleistungsmodelle im kritischen Vergleich

Die Wahl zwischen IaaS (Infrastructure as a Service), PaaS (Platform as a Service) und SaaS (Software as a Service) ist eine strategische Entscheidung, die direkt von Reife, Größe und den Zielen eines Unternehmens abhängt. Die Modelle unterscheiden sich primär im Grad der Kontrolle und Verantwortung, die vom Unternehmen zum Cloud-Anbieter verlagert wird. 
Kriterium          	IaaS     	PaaS    	SaaS
________________
Verantwortung  	Hoch (OS, Runtime, Daten, Applikation)        	Mittel (Applikation, Daten)	      Gering (Nur Konfiguration & Nutzung)
________________
Flexibilität	        Maximal      	Hoch    	Gering
________________
Geschwindigkeit	Mittel    	Hoch (Entwicklung)     	Sehr hoch (Nutzung)
________________

Strategische Bedeutung für Start-ups vs. Enterprise-Konzerne
**Start-ups:** Fokus auf Innovationsgeschwindigkeit und Time-to-Market
* Dominantes Modell: PaaS und SaaS.

* Time-to-Market: Start-ups müssen schnell validieren. SaaS (für CRM, E-Mail, Projektmanagement) ermöglicht sofortige Produktivität ohne Infrastruktur-Setup. PaaS (mit Serverless Functions, verwalteten Datenbanken) erlaubt es Entwicklern, sich ausschließlich auf die Kernlogik zu konzentrieren, was die Entwicklungszeit drastisch verkürzt.

* TCO: Die anfänglichen Investitionen (CapEx) sind minimal. Das Pay-as-you-go-Modell schont das Budget. IaaS wird oft nur gewählt, wenn eine spezifische, proprietäre Software betrieben werden muss, die keine PaaS-Anforderungen erfüllt.

* Innovationsgeschwindigkeit: Durch die Nutzung von PaaS-Diensten (z.B. KI-APIs, IoT-Plattformen) können Start-ups schnell innovative Funktionen integrieren, ohne tiefes Expertenwissen vorhalten zu müssen.

* Vendor Lock-in Risiko: Das Risiko wird bewusst in Kauf genommen, da die Geschwindigkeit wichtiger ist als langfristige Portabilität. 


**Etablierte Enterprise-Konzerne: Fokus auf Skalierbarkeit, Compliance und TCO-Optimierung**
* Dominantes Modell: IaaS und Hybrid-IaaS.

* TCO: Enterprise-Konzerne migrieren oft bestehende, virtualisierte Rechenzentren (Lift-and-Shift). IaaS bietet hier die größte Kompatibilität und ermöglicht es, bestehende Lizenzen (z.B. Windows Server, SQL Server) in die Cloud zu überführen (Hybrid Use Benefit), was die TCO kurzfristig optimiert.

* Governance & Compliance: Große Unternehmen benötigen oft die volle Kontrolle über das Betriebssystem und die zugrunde liegende Infrastruktur (IaaS), um strenge interne Audit- und Compliance-Vorgaben erfüllen zu können.

* Innovationsgeschwindigkeit: Innovationen finden oft in isolierten "Digital Labs" statt, die PaaS nutzen. Die breite Masse der Altsysteme verbleibt jedoch auf IaaS oder On-Premise.

* Vendor Lock-in Risiko: Dies ist ein hohes Risiko für Konzerne. Die Strategie zielt oft auf Multi-Cloud oder Hybrid-Cloud ab, um Abhängigkeiten zu minimieren und Verhandlungsmasse zu behalten. 


**Fazit der Phasen**

* Gründungs- und Wachstumsphase (Start-up): Klare Dominanz von SaaS (Effizienz) und PaaS (Entwicklung), um schnell Ergebnisse zu erzielen und Kapital zu schonen.

* Skalierungs- und Reifephase (Enterprise): IaaS dominiert für die Migration bestehender Workloads, während gezielt PaaS-Dienste für neue, innovative Projekte genutzt werden. Die Hybridität wird zur Norm.

### 1.2 Architekturentscheidungen für hybride Szenarien

Das Ziel ist eine Modernisierung bei gleichzeitiger Sicherung sensibler Altdaten On-Premise. Das folgende hypothetische Architekturkonzept nutzt eine Hybridstrategie, um die Vorteile beider Welten zu maximieren.

Szenario: Eine bestehende HR-Anwendung verwaltet hochsensible Mitarbeiterdaten (Gehälter, Gesundheitsakten), die lokal in einer SQL-Datenbank verbleiben müssen. Die Anwendung soll modernisiert werden, um neue Cloud-native Features (z.B. ein neues, skalierbares Mitarbeiterportal) bereitzustellen.

**Architekturkonzept**
Wir verwenden Services aus Microsoft Azure:

1. On-Premise: Bestehende SQL-Datenbank mit sensiblen Daten.

2. Cloud-Service 1 (PaaS - Datenbank): Azure SQL Database Managed Instance (oder Azure Private Link): Dient als Cloud-Datenbank für unkritische Daten (z.B. Mitarbeiterfotos, allgemeine Unternehmensnews) und als sicherer Kommunikationskanal zur On-Premise-DB.

3. Cloud-Service 2 (PaaS - Compute): Azure App Services: Skalierbare, verwaltete Plattform für das neue Mitarbeiterportal (Frontend/Backend API).

4. Cloud-Service 3 (IaaS/Netzwerk): Azure Site-to-Site VPN Gateway: Die technische Brücke, die eine sichere Verbindung zwischen dem lokalen Rechenzentrum und der Azure Cloud herstellt.

**Zusammenspiel der Services**

1-Sichere Konnektivität: Das Azure VPN Gateway stellt einen verschlüsselten Tunnel (Site-to-Site VPN) zwischen der lokalen Firewall und dem Azure Virtual Network (VNet) her. Die Cloud-Anwendungen agieren, als wären sie Teil des lokalen Netzwerks.

2-Anwendungslogik (Azure App Services): Das neue Mitarbeiterportal wird in den App Services gehostet. Diese können je nach Bedarf automatisch skalieren.

3-Datenzugriff (Hybrid):
* Wenn das Portal unkritische Daten benötigt, greift es direkt auf die Azure SQL Database zu (schneller Cloud-Zugriff).
* Wenn sensible Daten benötigt werden (z.B. Gehaltsabrechnungen), stellt der App Service eine Anfrage über den gesicherten VPN-Tunnel an die lokale SQL-Datenbank.

4-Datenresidenz: Die Architektur stellt sicher, dass die sensibelsten Daten niemals das lokale Rechenzentrum physisch verlassen und dennoch über die neue Cloud-Anwendung zugänglich sind.

**Begründung der Wahl**

Vorteile der hybriden Strategie: Maximale Datensouveränität (Compliance erfüllt), gleichzeitige Nutzung moderner, skalierbarer Cloud-Dienste (Innovationsvorteil).

Wahl der Services: PaaS-Dienste (App Services, Azure SQL DB) wurden gewählt, um den Wartungsaufwand für die neue Anwendung zu minimieren und Skalierbarkeit zu gewährleisten. Das VPN Gateway ist der technische Standard für sichere Hybridverbindungen.

**Technische Herausforderungen bei der Integration**

1-Netzwerkkomplexität: Sicherstellung des korrekten Routings, DNS-Auflösung und Firewall-Konfigurationen auf beiden Seiten der VPN-Verbindung.

2-Latenz: Der Zugriff auf die lokale Datenbank aus der Cloud ist immer langsamer als der Zugriff innerhalb eines Rechenzentrums. Die Architektur muss Latenz-tolerante Abfragen entwerfen (z.B. Caching verwenden).

3-Datenkonsistenz und Synchronisation: Es kann zu Herausforderungen kommen, wenn Daten redundant (teils lokal, teils Cloud-DB) gehalten werden müssen und synchronisiert werden müssen, um die Performance zu gewährleisten.


### 1.3 Governance und Compliance in Multi-Cloud-Umgebungen

Die Nutzung mehrerer Cloud-Anbieter (Multi-Cloud) bietet Vorteile wie die Vermeidung von Vendor Lock-in und die Nutzung von Best-of-Breed-Services, führt jedoch zu erheblichen Herausforderungen in Bezug auf Governance und Compliance, da jeder Anbieter eigene Tools, APIs und Sicherheitsmodelle hat. 

**Herausforderungen**
1-Inkonsistente Sicherheitslage: Richtlinien, die in AWS funktionieren (z.B. IAM-Rollen), lassen sich nicht direkt auf Azure (Azure AD, RBAC) oder Google Cloud (IAM) übertragen. Dies schafft Sicherheitslücken.

2-Mangelnde Transparenz (Shadow IT): Es ist schwierig, den Überblick über alle genutzten Dienste über verschiedene Clouds hinweg zu behalten.

3-Datenresidenz und DSGVO: Die Einhaltung der DSGVO erfordert strikte Kontrolle darüber, wo (in welchem Land/Region) Daten gespeichert und verarbeitet werden. In Multi-Cloud-Umgebungen kann die Datenbewegung über verschiedene Jurisdiktionen hinweg schnell unkontrollierbar werden.

4-Auditierbarkeit: Auditoren benötigen Zugriff auf konsolidierte Protokolle und Berichte aus allen Umgebungen, was bei fragmentierten Systemen mühsam ist.

**Schlüsselbereiche für spezielle Anforderungen**

+ Datenresidenz: Cloud Services müssen präzise Konfigurationsmöglichkeiten bieten (z.B. "speichere Daten nur in der EU West Region"). Dies muss zentral überwacht werden.

+ Zugriffsmanagement (IAM): Die größte Herausforderung. Zugriffsrechte müssen über alle Clouds hinweg konsistent sein.

+ Auditierbarkeit: Logging- und Monitoring-Dienste müssen einheitlich Daten sammeln und zentral speichern.

**Strategische Empfehlungen für das Management**

1-Zentrale Cloud Governance Platform (CSPM):

Einführung eines Cloud Security Posture Management (CSPM) Tools eines Drittanbieters (z.B. Microsoft Defender for Cloud, Prisma Cloud, Wiz). Diese Tools bieten eine einzige Glasscheibe, um Compliance-Verstöße und Fehlkonfigurationen aller Cloud-Anbieter zu erkennen und zu beheben.

2-Identity Federation und Zero Trust:

Verwendung eines zentralen Identitätsanbieters (z.B. Azure AD oder Okta), der als Single Source of Truth dient. Alle Zugriffe auf AWS-, Azure- oder GCP-Ressourcen werden über diesen zentralen Dienst authentifiziert. Implementierung des Zero-Trust-Prinzips ("Never trust, always verify").

3-Automatisierung durch Infrastructure-as-Code (IaC):

Anstatt Ressourcen manuell im Portal jedes Anbieters bereitzustellen, sollte IaC (z.B. Terraform) verwendet werden. Terraform kann konsistente Richtlinien und Konfigurationen (z.B. "Datenbanken müssen immer Verschlüsselung aktivieren") über AWS, Azure und GCP hinweg erzwingen.

4-Einführung eines "Cloud Center of Excellence" (CCoE):

Ein dediziertes, interdisziplinäres Team, das die Standards, Richtlinien und Best Practices für die Nutzung aller Cloud-Plattformen definiert, kommuniziert und durchsetzt.
