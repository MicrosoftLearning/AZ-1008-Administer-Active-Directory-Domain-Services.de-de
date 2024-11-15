---
lab:
  title: Übung – Konfigurieren von Domänencontrollervorgängen
  module: Guided Project – Administer Active Directory Domain Services
---
In dieser Übung stufen Sie einen Server zum Domänencontroller hoch, übertragen eine FSMO-Rolle auf den neuen Domänencontroller, erstellen einen Standort und fügen dem Standort ein Subnetz hinzu.

## Installieren von Active Directory Domain Services (AD DS) und Höherstufen auf Domänencontroller

In dieser Aufgabe fördern Sie den Mitgliedsserver TAILWIND-MBR1, um ein Domänencontroller in der TAILWINDTRADERS-Domäne zu werden. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Melden Sie sich mit dem Kennwort bei TAILWIND-MBR1 als TAILWINDTRADERS\\Administrator an: `Pa55w.rdPa55w.rd`.
2.  Wählen Sie im Server-Manager das Menü „Manage“ und dann **Add Roles and Features** aus.
3.  Klicken Sie auf der Seite „Before you begin“ des Assistenten „Add Roles and Features“ auf **Next**.
4.  Wählen Sie auf der Seite „Select installation type“ die Option **Role-based or feature-based installation** aus, und klicken Sie auf **Next**.
5.  Wählen Sie auf der Seite „Select destination server“ die Option **Select a server from the server pool** aus, stellen Sie sicher, dass TAILWIND-MBR1 ausgewählt ist, und klicken Sie auf **Next**.
6.  Aktivieren Sie auf der Seite „Select server roles“ das Kontrollkästchen **Active Directory Domain Services**. Dadurch wird die Seite „Add features“ geöffnet. Wählen Sie **Features hinzufügen** aus. Klicken Sie auf **Weiter**.
7.  Klicken Sie auf der Seite "Features auswählen" auf **Weiter**.
8.  Klicken Sie auf der Seite „Active Directory Domain Services“ auf **Next**.
9.  Klicken Sie auf der Seite "Installationsauswahl bestätigen" auf **Installieren**. Je nach Geschwindigkeit des Computers kann die Installation einige Minuten dauern. Klicken Sie nach Abschluss der Installation auf **Schließen**.
10. Wählen Sie im Menü „Server-Manager“ das Benachrichtigungssymbol neben der Flagge oben rechts aus (wie im Screenshot gezeigt).

    ![Screenshot des Server-Manager-Menüs mit angezeigtem Warnsymbol.](./Media/server-manager-menu.png)
13. Wählen Sie im Menü, das sich öffnet, wenn Sie das Benachrichtigungssymbol auswählen, die Option **Promote this server to a domain controller** aus. Dies startet den Konfigurations-Assistenten für Active Directory Domain Services.
14. Wählen Sie auf der Seite „Deployment Configuration“ die Option **Add a domain controller to an existing domain** aus, und stellen Sie sicher, dass der Domänenname auf **tailwindtraders.internal** eingerichtet ist.
15. Sie müssen das Adminkonto erneut authentifizieren. Wählen Sie **Ändern** aus. Geben Sie `Administrator` als Benutzername und `Pa55w.rdPa55w.rd` als Kennwort ein. Klicken Sie auf **OK**. Klicken Sie auf **Weiter**.
16. Akzeptieren Sie auf der Seite „Domain Controller options“ die Standardeinstellungen, und geben Sie das Kennwort für den Wiederherstellungsmodus der Verzeichnisdienste (DSRM) ein. Geben Sie dazu zweimal das folgende Kennwort ein: `Pa55w.rdPa55w.rd`. Klicken Sie auf **Weiter**.
17. Klicken Sie auf der Seite „DNS Options“ auf **Next**.
18. Klicken Sie auf der Seite „Additional Options“ auf **Next**.
19. Klicken Sie auf der Seite „Pfade“ auf **Next**.
20. Klicken Sie auf der Seite „Review Options“ auf **Next**.
21. Klicken Sie auf der Seite „Prerequisites Check“ auf **Install**. Die Installation dauert je nach Geschwindigkeit des virtuellen Computers mehrere Minuten. Der virtuelle Computer wird neu gestartet.
22. Melden Sie sich beim Neustart des virtuellen Computers als `tailwindtraders\administrator` mit dem Kennwort an, das Sie für das Standard-Administratorkonto konfiguriert haben (`Pa55w.rdPa55w.rd`).

## Flexible Übertragung einzelner Master-Betriebsrollen

In dieser Aufgabe übertragen Sie die Rolle RID Master von TAILWIND-DC1 zu TAILWIND-MBR1. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie auf TAILWIND-MBR1 unter **Tools** „Active Directory Users and Computers“.<br>
2.  Klicken Sie im Navigationsbereich mit der rechten Maustaste auf „Active Directory Users and Computers“, zeigen Sie auf **All Tasks**, und wählen Sie dann **Operations Masters** aus.
3.  Wählen Sie auf der Registerkarte „RID“ die Option **Change** aus, und klicken Sie dann auf **Yes** und auf **OK**.
4.  Klicken Sie auf **Schließen**, um das Dialogfeld „Operations Masters“ zu schließen.

## Erstellen eines Active Directory-Standorts und Konfigurieren eines Subnetzes für diesen Standort

In dieser Aufgabe erstellen Sie eine Active Directory-Site, und konfigurieren ein Subnetz, das mit dieser Site verbunden ist. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Melden Sie sich bei TAILWIND-DC1 als `tailwindtraders\administrator` mit dem Kennwort an, das Sie für das standardmäßige Administratorkonto (`Pa55w.rdPa55w.rd`) konfiguriert haben.
2.  Öffnen Sie „Active Directory-Standorte und -Dienste“ über das Menü „Extras“.
3.  Klicken Sie mit der rechten Maustaste auf „Sites“, wählen Sie **Neue Site** aus und geben Sie `Sydney` als Site-Namen ein.
4.  Wählen Sie als Linknamen „DEFAULTIPSITELINK“ aus und klicken Sie zweimal auf **OK**.
5.  Erweitern Sie den Ordner **Sites**.
6.  Klicken Sie mit der rechten Maustaste auf **Subnetze**, und wählen Sie **Neues Subnetz** aus.
7.  Geben Sie als Präfix `172.16.1.0/24` ein, wählen Sie **Sydney** als Standortnamen aus und klicken Sie auf **OK**.
8.  Schließen Sie Active Directory-Standorte und -Dienste.
