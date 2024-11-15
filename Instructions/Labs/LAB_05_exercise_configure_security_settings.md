---
lab:
  title: Übung – Konfigurieren von Sicherheitseinstellungen
  module: Guided Project – Administer Active Directory Domain Services
---
In dieser Übung konfigurieren Sie Einstellungen im Zusammenhang mit der Sicherheit, einschließlich der Deaktivierung der NTLM-Authentifizierung für Domänenkonten, der Überwachung der Kontoverwaltungsaktivität und dem Verweigern der Anmeldung als Dienst für Mitglieder einer Sicherheitsgruppe.

## Einschränken der NTLM-Authentifizierung

Bei dieser Aufgabe schränken Sie die NTLM-Authentifizierung ein. Um diese Aufgabe abzuschließen, führen Sie die folgenden Schritte in TAILWIND-DC1 aus:

1.  Öffnen Sie im Menü „Tools“ der Server-Manager-Konsole die Verwaltungskonsole „Group Policy“.
2.  Erweitern Sie in der Verwaltungskonsole „Group Policy“ die Gesamtstruktur „tailwindtraders.internal“, den Ordner „Domains“ und die Domäne „tailwindtraders.internal“. Erweitern Sie dann Gruppenrichtlinienobjekte.
3.  Klicken Sie mit der rechten Maustaste auf **Default Domain Controller Policy**, und klicken Sie auf **Edit**.
4.  Navigieren Sie zu Computer Configuration\\Policies\\Windows Settings\\Security Settings\\Local Policies\\Security Options.
5.  Wählen Sie dies aus, und doppelklicken Sie auf **Network security: Restrict NTLM: NTLM authentication in this domain**.
6.  Klicken Sie auf das Kontrollkästchen **Define this policy setting**.
7.  Wählen Sie den Wert **Deny all** aus, und klicken Sie auf **OK**.
8.  Klicken Sie im Dialogfeld „Confirm Setting Change“ auf **Ja**.
9.  Schließen Sie den Gruppenrichtlinienverwaltungs-Editor.

## Überwachen der Benutzerkontenverwaltung in Sydney

In dieser Aufgabe ermöglichen Sie die Prüfung der Benutzerkontenverwaltung in der Organisationseinheit Sydney. Um diese Aufgabe abzuschließen, führen Sie die folgenden Schritte in TAILWIND-DC1 aus:

1.  Wählen Sie im Menü „Tools“ der Server-Manager-Konsole die Gruppenrichtlinien-Verwaltungskonsole aus.
2.  Erweitern Sie in der Gruppenrichtlinien-Verwaltungskonsole die Domäne „Tailwindtraders.internal“.
3.  Navigieren Sie zur Organisationseinheit Sydney, klicken Sie mit der rechten Maustaste, und wählen Sie **Create a GPO in this domain, and link it here...** aus.
4.  Geben sie der neuen GPO den Namen `SydneyOUPolicy`.
5.  Klicken Sie auf **OK**.
6.  Klicken Sie mit der rechten Maustaste auf „SydneyOUPolicy“, und wählen Sie **Edit** aus.
7.  Navigieren Sie zu Computer Configuration\\Policies\\Windows Settings\\Security Settings\\Advanced Audit Policy Configuration\\Audit Policies\\Account Management.
8.  Wählen Sie die Option aus, und doppelklicken Sie auf **Kontoverwaltung für Audit-Benutzer**.
9.  Klicken Sie auf das Kontrollkästchen **Configure the following audit events**.
10.  Wählen Sie die Werte für **Success** und **Failure** aus, und klicken Sie auf **OK**.
11.  Den Editor zur Gruppenrichtlinienverwaltung schließen

## Deny Log On As a Service

In dieser Aufgabe konfigurieren Sie die Sicherheitsoption „Deny Log on as a service“. Um diese Aufgabe abzuschließen, führen Sie die folgenden Schritte in TAILWIND-DC1 aus:

1.  Öffnen Sie im Menü „Tools“ der Server-Manager-Konsole die Verwaltungskonsole „Group Policy“.
2.  Erweitern Sie die Domäne Tailwindtraders.internal.
3.  Navigieren Sie zur Organisationseinheit Sydney, und klicken Sie mit der rechten Maustaste auf „SydneyOUPolicy“. Wählen Sie **Bearbeiten** aus.
4.  Navigieren Sie zu Computer Configuration\\Policies\\Windows Settings\\Security Settings\\Local Policies\\User Rights Assignment.
5.  Wählen Sie die Richtlinie **Anmelden als Dienst verweigern** aus, und doppelklicken Sie darauf.
6.  Wählen Sie die Einstellung **Define this policy** aus.
7.  Klicken Sie auf **Benutzer oder Gruppe hinzufügen**.
8.  Klicken Sie auf **Browse**, dann auf **Advanced** und anschließend auf **Find now**.
9.  Wählen Sie die Gruppe **Sydney Administrators** aus.
10. Klicken Sie auf **OK**, bis Dialogfelder geschlossen sind (es kann vier oder fünf Bestätigungen erfordern).
