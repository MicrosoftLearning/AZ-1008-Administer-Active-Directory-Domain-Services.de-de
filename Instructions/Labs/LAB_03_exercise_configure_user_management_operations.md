---
lab:
  title: 'Übung: Konfigurieren von Benutzerverwaltungsvorgängen '
  module: Guided Project – Administer Active Directory Domain Services
---
In dieser Übung führen Sie Benutzerverwaltungsvorgänge aus.

## Erstellen von Organisationseinheiten

In dieser Aufgabe erstellen Sie drei OEs: Sydney, Melbourne und Brisbane. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 Active Directory-Benutzer und -Computer über das Menü „Tools“ der Server-Manager-Konsole.
2.  Klicken Sie mit der rechten Maustaste auf die Domain **tailwindtraders.internal**.
3.  Wählen Sie **Neu**, dann **Organisationseinheit** aus.
4.  Legen Sie im Dialogfeld „Neues Objekt – Organisationseinheit“ den Namen `Sydney` fest und klicken Sie auf **OK**.
5.  Wiederholen Sie diesen Vorgang, um die OE `Melbourne` und die OE `Brisbane` zu erstellen.

## Erstellen von Benutzern

In dieser Aufgabe erstellen Sie ein Benutzerkonto und konfigurieren Kontoeigenschaften wie das Ablaufdatum des Kontos. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 Active Directory-Benutzer und -Computer (oder Verwaltungscenter).
2.  Klicken Sie mit der rechten Maustaste auf die Sydney OE.
3.  Wählen Sie **Neu**, dann **Benutzer**.
4.  Geben Sie `SydneyContractor` in die Felder „Vollständiger Name“ und „Benutzername“ etwas ein und klicken Sie auf **Weiter**.
5.  Geben Sie ein Kennwort an, z. B. `Pa55w.rdPa55w.rd`, und bestätigen Sie das Kennwort.
6.  Klicken Sie auf **Weiter** und dann auf **Fertigstellen**.
7.  Wählen Sie die Sydney-OE aus. Doppelklicken Sie in der Sydney-OE auf das Benutzerkonto „SydneyContractor.
8.  Wählen Sie auf der Konto-Registerkarte im Abschnitt **Konto läuft ab** die Option **Ende:** aus, und legen Sie das Datum auf **1. Januar 2030** fest. Klicken Sie auf **OK**.
9.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto „SydneyContractor“ und wählen Sie **Kopieren** aus.
10. Geben Sie `MelbourneContractor` in die Felder „Vollständiger Name“ und „Benutzername“ ein. Klicken Sie auf **Weiter**.
11. Geben Sie ein Kennwort ein, z. B. `Pa55w.rdPa55w.rd`, und bestätigen Sie das Kennwort.
12. Klicken Sie auf **Weiter** und dann auf **Fertigstellen**.
13. Klicken Sie mit der rechten Maustaste auf das Benutzerkonto „SydneyContractor“ und wählen Sie **Kopieren** aus.
14. Geben Sie `BrisbaneContractor` in die Felder „Vollständiger Name“ und „Benutzername“ ein. Klicken Sie auf **Weiter**.
15. Geben Sie ein Kennwort ein, z. B. `Pa55w.rdPa55w.rd`, und bestätigen Sie das Kennwort.
16. Klicken Sie auf **Weiter** und dann auf **Fertigstellen**.
17. Ziehen Sie das Benutzerkonto „MelbourneContractor“ in die Melbourne-OE.
18. Wenn eine Warnung vor sich bewegenden Objekten angezeigt wird, klicken Sie auf **Ja**.
19. Ziehen Sie das BrisbaneContractor-Benutzerkonto in die OE von Brisbane.
20. Wenn eine Warnung vor sich bewegenden Objekten angezeigt wird, klicken Sie auf **Ja**.


## Erstellen der Gruppe „Sydney-Administratoren“

In dieser Aufgabe erstellen Sie eine neue Sicherheitsgruppe namens „Sydney Administrators“. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 Active Directory-Benutzer und -Computer.
2.  Klicken Sie mit der rechten Maustaste auf die Sydney-OE und wählen Sie **Neu**, dann **Gruppe**.
3.  Geben Sie `Sydney Administrators` als Gruppennamen ein und wählen Sie **Universell** als Gruppenbereich aus. Klicken Sie auf **OK**.
4.  Doppelklicken Sie in der Sydney-OE auf das SydneyContractor-Benutzerkonto.
5.  Klicken Sie auf der Registerkarte „Mitglied“ von auf **Hinzufügen**.
6.  Geben Sie `Sydney Administrators`ein.
7.  Klicken Sie auf **Namen überprüfen**.
8.  Klicken Sie auf **OK** und dann erneut auf **OK**.

## Konfigurieren eines Benutzers als geschützter Benutzer

In dieser Aufgabe konfigurieren Sie das SydneyContractor-Benutzerkonto als „geschützten Benutzer“. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 Active Directory-Benutzer und -Computer (oder Verwaltungscenter).
2.  Navigieren Sie zur Sydney-OE und doppelklicken Sie auf das SydneyContractor-Benutzerkonto.
3.  Klicken Sie auf der Registerkarte „Mitglied“ von auf **Hinzufügen**.
4.  Geben Sie `Protected Users`ein.
5.  Klicken Sie auf **Namen überprüfen**.
6.  Klicken Sie auf **OK** und dann erneut auf **OK**.

## Delegieren von Sicherheitsberechtigungen an eine Organisationseinheit an eine Sicherheitsgruppe

In dieser Aufgabe delegieren Sie die Fähigkeit, Kennwörter zurückzusetzen und die Änderung von Kennwörtern zu erzwingen, an die Gruppe der Administrierenden von Sydney über Konten in der Sydney-OE. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 Active Directory-Benutzer und -Computer.
2.  Klicken Sie mit der rechten Maustaste auf die OE Sydney und klicken Sie auf **Steuerung delegieren**.
3.  Klicken Sie auf der Startseite des Assistenten für die Delegierung der Kontrolle auf **Weiter**.
4.  Klicken Sie auf **Hinzufügen** und geben Sie `Sydney Administrators` ein.
5.  Klicken Sie auf **Namen überprüfen**.
6.  Klicken Sie auf **OK** und dann auf **Weiter**.
7.  Wählen Sie auf der Seite „Zu delegierende Aufgaben“ die Option **Benutzerkennwörter zurücksetzen und die Kennwortänderung bei der nächsten Anmeldung erzwingen** aus. Klicken Sie auf **Weiter**.
8.  Klicken Sie auf **Fertig stellen**.

## Konfigurieren des City-Attributs für einen Benutzer

Bei dieser Aufgabe konfigurieren Sie ein Stadtattribut für ein Benutzerkonto und verwenden dann das Attribut „Suchen“, um zu überprüfen, ob der/die Benutzende vorhanden ist. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 Active Directory-Benutzer und -Computer.
2.  Wählen Sie die Sydney-OE aus, klicken Sie mit der rechten Maustaste auf das Benutzerkonto „SydneyContractor“ und klicken Sie auf **Eigenschaften**.
3.  Legen Sie auf der Registerkarte „Adresse“ der Eigenschaften von Sydney Contractor im Feld „Stadt“ den Wert `Sydney` fest und klicken Sie auf **OK**.
4.  Klicken Sie in Active Directory-Benutzer und -Computer mit der rechten Maustaste auf „Tailwindtrader.internal“ und klicken Sie auf **Suchen**.
5.  Wählen Sie auf der Registerkarte „Erweitert“ des Dialogfelds „Benutzer, Kontakte und Gruppen suchen“ die Option **Feld**, dann **Benutzer**, dann **Stadt**. Legen Sie Bedingung auf **Ist (genau)** fest. Legen Sie den Wert auf **Sydney** fest. Klicken Sie auf **Jetzt suchen**.
6.  Klicken Sie auf **Ja** im Popup-Fenster „Im Verzeichnis finden“.
7.  Überprüfen Sie, ob das Benutzerkonto SydneyContractor in den **Suchergebnissen** aufgeführt ist.
8.  Schließen Sie das Dialogfeld „Benutzer, Kontakte und Gruppen suchen“.

## Deaktivieren des Melbourne-Auftragnehmerbenutzers

In dieser Aufgabe deaktivieren Sie das Benutzerkonto „Melbourne Contractor“. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 Active Directory-Benutzer und -Computer, und öffnen Sie dann die Melbourne-OE.
2.  Klicken Sie in der Melbourne-OE mit der rechten Maustaste auf **MelbourneContractor** und klicken Sie auf **Konto deaktivieren**.
3.  Klicken Sie auf **OK**.

## Zurücksetzen des Kennworts des Auftragnehmers von Brisbane

In dieser Aufgabe setzen Sie das Kennwort des BrisbaneContractor-Benutzerkontos zurück. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 Active Directory-Benutzer und -Computer, und öffnen Sie dann die Brisbane-OE.
2.  Klicken Sie mit der rechten Maustaste auf das Benutzerkonto „BrisbaneContractor“ und wählen Sie **Kennwort zurücksetzen**.
3.  Geben Sie im Dialogfeld „Kennwort zurücksetzen“ das Kennwort `Pa66w.rdPa66w.rd` zweimal ein und wählen Sie **OK**. Klicken Sie erneut auf **OK** in dem Dialog, der Sie darüber informiert, dass das Kennwort geändert wurde.
