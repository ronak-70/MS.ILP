## 1. Das Shared Responsibility Model: Grenzen der Verantwortung in der Cloud

### Aufgabenstellung:

1. * Wähle einen spezifischen Cloud-Service-Typ
   *  Beschreibe ein hypothetisches Szenario, in
      demeine Sicherheitslücke aufgetreten ist.

      Angenommen Firma X betreibt eine Kundenwebanwendung auf IaaS-VMs in einer Cloud-Region. Eine VM ist aufgrund fehlender OS-Patches für eine bekannte RCE-Schwachstelle angreifbar. Ein Angreifer nutzt diese Lücke, führt Code aus, liest sensible Nutzerdaten und API-Schlüssel aus dem Dateisystem aus und exfiltriert sie

  * Identifiziere klar, welche Aspekte der   Sicherheitslücke in die Verantwortung des Cloud-Anbieters fallen und welche in die des Kunden. Berücksichtige dabei auch potenzielle Grauzonen oder Bereiche, in denen eine Abgrenzung schwierig sein könnte.

      klare Abgrenzung:
      CSP verantwortlich für physische Infrastruktur, Hypervisor-Isolation, physische Sicherheit, Netz-Backbone sowie Bereitstellung von Sicherheitsservices (z. B. VPC, Security Groups, KMS, DDoS-Schutz).

      Kunde verantwortlich für das Guest-OS, Applikations-Patches, Konfiguration, Geheimnisverwaltung, Host-basierte Firewall, Intrusion Detection auf VM-Ebene, Logging/Alerting der Anwendung. 

  * Diskutiere, welche technischen Kontrollen der Cloud-Anbieter bereitstellt und welche der Kunde implementieren *muss*, um seine Verantwortung zu erfüllen und das Risiko zu minimieren.

      Provider Controls (Beispiele):

      Hypervisor-Isolation, Host-Patching, VPC/NSG, DDoS-Protection, KMS, zentrale Logging-/Monitoring-Services, optionale WAF/Managed IDS.

      Customer Controls:

      OS-Patching, Härtung, Secret-/Key-Management (z. B. Vault/KMS), EDR/Agenten, Logging/Alerting, Incident Response Playbooks, regelmäßige Pen-Tests.  

2. * Erkläre, wie das Shared Responsibilit Model
     die Durchführung von Compliance-Audits in einer Cloud-Umgebung beeinflusst.

     Incident Response Steps:

     VM isolieren, forensische Images erstellen, Logs sichern.
     Geheimnisse rotieren und entwerten.
     Root cause analysieren, Patches ausrollen, Ersatz-VMs aus geprüften Images starten.
     Compliance-Notifications (z. B. Datenschutzbeauftragter, Aufsichtsbehörden).
     Lessons Learned + Hardenings + regelmäßige Tests.

    * Beschreibe, welche Dokumente oder Nachweise der 
      Cloud-Kunde typischerweise vom Cloud-Anbieter anfordern würde, um seine eigene Compliance zu belegen, und welche Rolle der Kunde selbst bei der Bereitstellung von Nachweisen spielt. 

    - Auditoren verlangen von CSP Audit-Reports (SOC2, 
      ISO27001, PCI) und Angaben zur Data Residency.

    - Kunde liefert Nachweise zu Own Controls:        
      Patch-Records, IAM-Policies, Log-Aufbewahrung, Backup/DR-Tests.

    - Shared Responsibility erleichtert die     
      Audit-Scope-Definition: CSP controls vs. customer controls.

## 2. Infrastructure as a Service (IaaS): Die flexible Basis

### Aufgabenstellung:
1. *  Analysiere kritisch die Total Cost of Ownership  
      (TCO)

     typische Erkenntnis:
     Kurzfristig, also in einem Zeitraum von etwa 1–3 Jahren, kann ein On-Premises-Betrieb bei sehr großen oder bereits vollständig etablierten Workloads tatsächlich günstiger wirken. Der Grund ist, dass die Organisation bereits viel in eigene Hardware, Lizenzen, Rechenzentrumsfläche und Personal investiert hat. Da diese Investitionen abgeschrieben werden oder ohnehin vorhanden sind, entstehen relativ geringe zusätzliche Kosten, wenn die bestehende Infrastruktur weitergenutzt wird.
     Man spricht hier von Economies of Scale: Große, stark ausgelastete Rechenzentren können ihre Hardware, Energie und Personalressourcen sehr effizient nutzen und dadurch niedrige Stückkosten pro Workload erreichen.


     Mittelfristig bis langfristig: IaaS reduziert CAPEX, erhöht Agilität, verkürzt Time-to-Market; TCO positiv, wenn man Betriebskosten, Personalkosten, Downtime-Risiken und Skalierbarkeit berücksichtigt.

  *  Diskutiere die signifikanten Unterschiede im   
     Betriebsmodell und in den benötigten Skillsets der IT-Abteilung zwischen einer IaaS- und einer On-Premise-Strategie.

     On-Prem: Hardware lifecycle management, cabling, rack ops, physical security.

     IaaS: IaC (Terraform/ARM), Cloud-Security, Cost-Optimization (FinOps), SRE/DevOps Practices.
   

      