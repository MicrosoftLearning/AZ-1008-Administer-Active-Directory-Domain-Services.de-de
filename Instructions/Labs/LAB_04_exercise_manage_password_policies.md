---
lab:
  title: 'Übung: Verwalten von Kennwortrichtlinien'
  module: Guided Project – Administer Active Directory Domain Services
---
In dieser Übung konfigurieren Sie Gruppenrichtlinienelemente im Zusammenhang mit Kennwortrichtlinien. Dazu gehört das Konfigurieren der Domänenkennwortrichtlinie, das Erstellen einer strengeren Kennwortrichtlinie für die Gruppe „Domänenadministratoren“ und das Aktivieren des Active Directory-Papierkorbs.

## Konfigurieren einer Domänenkennwortrichtlinie

In dieser Aufgabe konfigurieren Sie die Domänenkennwortrichtlinie. Führen Sie die folgenden Schritte aus, um diese Aufgabe auszuführen:

1.  Öffnen Sie in TAILWIND-DC1 über das Menü „Extras“ der Server-Manager-Konsole die Gruppenrichtlinien-Verwaltungskonsole.
2.  Erweitern Sie in der Verwaltungskonsole „Group Policy“ die Gesamtstruktur „tailwindtraders.internal“, den Ordner „Domains“ und die Domäne „tailwindtraders.internal“.
3.  Klicken Sie mit der rechten Maustaste auf **Standarddomänenrichtlinie**, und klicken Sie auf **Bearbeiten**.
4.  Navigieren Sie im Gruppenrichtlinienverwaltungs-Editor zu Computerkonfiguration\\Richtlinien\\Windows-Einstellungen\\Sicherheitseinstellungen\\Kontorichtlinien\\Kennwortrichtlinie.
5.  Doppelklicken Sie auf das Richtlinienelement für die **Mindestkennwortlänge**.
6.  Ändern Sie die Mindestanzahl von Zeichen in `14`.
7.  Klicken Sie auf **OK**, und schließen Sie dann den Gruppenrichtlinienverwaltungs-Editor.
8.  Schließen Sie die Gruppenrichtlinien-Verwaltungskonsole.

## Konfigurieren einer differenzierten Kennwortrichtlinie

In dieser Aufgabe konfigurieren Sie eine differenzierte Kennwortrichtlinie und wenden sie auf die Gruppe „Domänenadmins“ an. Um diese Aufgabe abzuschließen, führen Sie die folgenden Schritte in TAILWIND-DC1 aus:

1.  Öffnen Sie das Active Directory-Verwaltungscenter über das Menü „Tools“ der Server-Manager-Konsole.
2.  Klicken Sie unter Übersicht auf **Tailwindtraders (lokal).**
3.  Öffnen Sie im Bereich „Tailwindtraders (lokal)“ den Systemcontainer.
4.  Öffnen Sie im System-Container den Container „Kennwort-Einstellungen“.
5.  Klicken Sie mit der rechten Maustaste auf den Container „Kennworteinstellungen“, klicken Sie auf **Neu** und dann auf **Kennworteinstellungen**.
6.  Geben Sie im Feld „Name“ `Domain Admin Password Policy` ein.
7.  Legen Sie das Feld „Rangfolge“ auf `1` fest.
8.  Legen Sie die Mindestlänge des Kennworts auf `16` fest.
9.  Klicken Sie auf **OK**.
10. Öffnen Sie die neue Richtlinie **Domänen-Admins-Kennwortrichtlinie**.
11. Klicken Sie im Abschnitt „Direkt anwendbar auf“ auf **Hinzufügen** und geben Sie dann `Domain Admins` ein. Klicken Sie auf **Namen überprüfen**und anschließend auf **OK**.
12. Klicken Sie auf **OK**.

## Aktivieren des Active Directory-Papierkorbs

Bei dieser Aufgabe aktivieren Sie den Active Directory-Papierkorb. Um diese Aufgabe abzuschließen, führen Sie die folgenden Schritte in TAILWIND-DC1 aus:

1.  Öffnen Sie das Active Directory-Verwaltungscenter über das Menü „Tools“ der Server-Manager-Konsole.
2.  Klicken Sie auf **Tailwindtraders (lokal)** im linken Bereich.
3.  Wählen Sie im rechten Bereich **Papierkorb aktivieren**.
4.  Klicken Sie auf **OK**, um die Warnung zu verwerfen.
5.  Klicken Sie auf **OK**, um die Warnung über die Replikationslatenz zu verwerfen.
