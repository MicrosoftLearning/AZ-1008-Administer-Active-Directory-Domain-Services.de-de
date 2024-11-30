---
lab:
  title: Vorbereiten
  module: Guided Project – Administer Active Directory Domain Services
---
## Projektübersicht

In diesem angeleiteten Projekt durchlaufen Sie die wichtigsten Schritte zum Erstellen, Konfigurieren und Warten eines Domänencontrollers. Sie haben auch die Möglichkeit, einen Domänencontroller höherzustufen.

## Setup

Um die Ressourcenzugriffsanforderungen zu verringern, z. B. den Zugriff auf Windows Server oder ein Microsoft Azure-Abonnement, wird in diesem angeleiteten Projekt ein Windows 10- oder Windows 11-Computer verwendet, um eine virtualisierte Umgebung auszuführen. Sie konfigurieren ein Hyper-V-Subsystem für Windows 10- oder Windows 11-Computer, um die beiden virtuellen Computer der Windows Server 2022 Evaluation Edition zu unterstützen, die Sie für dieses Projekt verwenden. Sie benötigen die Professional- oder Enterprise-Edition von Windows 10 oder Windows 11, um diese Aufgaben auszuführen.

Der Computer, der als Hyper-V-Virtualisierungshost fungiert, sollte über mindestens 16 GB RAM verfügen. Sie können auch eine Evaluierungsversion von Windows Server verwenden, wobei die Hyper-V-Rolle als Host für diese virtuellen Computer installiert wird. Alternativ können Sie eine Virtualisierungsplattform eines Drittanbieters konfigurieren, um beide virtuellen Computer zu hosten. Bei den Übungen und Aufgaben in diesem Lab wird Windows 11 beim Beschreiben des Hyper-V-Hosts verwendet. Die hier dargestellten Optionen erleichtern das Suchen großer Dateien virtueller Computer, wenn Sie die Konfiguration nach Abschluss des Projekts entfernen möchten.

Der Abschnitt „Setup“ besteht aus drei Hauptaufgaben:

 -  Installieren von Hyper-V
 -  Erstellen eines virtuellen Computers für einen Windows Server-Domänencontroller
 -  Erstellen eines Windows Server-Domänenmitgliedsservers

## Installieren von Hyper-V

Bei dieser Aufgabe installieren Sie Hyper-V und konfigurieren einen NAT-Schalter. Sie konfigurieren Hyper-V so, dass ein anderer Satz von Standardverzeichnissen zum Speichern von Dateien und Festplatten virtueller Computer verwendet wird. Sie können die in dieser Anleitung vorgestellten Optionen verwenden oder Ihren eigenen Standort auswählen.

1.  Melden Sie sich mit einem Konto, das über lokale Adminrechte verfügt, bei dem Windows 11-Computer an.
2.  Klicken Sie auf dem Windows 11-Computer auf **Start**, wählen Sie **Settings** und auf der Seite „Settings“ **System** aus.
3.  Scrollen Sie auf der Seite „System“ der Einstellungen nach unten, bis Sie „Optional Features“ finden. Wählen Sie **Optional Features** aus.
4.  Scrollen Sie auf der Seite „Optional Features“ nach unten, bis Sie unter „Related Settings“ die Option **More Windows Features** finden.
5.  Aktivieren Sie auf der Seite „Windows Feature“ das Kontrollkästchen neben „Hyper-V“, und klicken Sie auf **OK**, wie in der Abbildung dargestellt.
    
    ![Screenshot der Seite „Optional Features“, auf der Hyper-V ausgewählt ist](./Media/optional-features.png)
    
6.  Wenn die Installation abgeschlossen ist, klicken Sie auf der Seite „Windows Features“ auf **Restart Now**.
7.  Melden Sie sich nach dem Neustart des Computers erneut mit dem gleichen Konto an, das über lokale Adminrechte verfügt.
8.  Klicken Sie auf **Start**, und suchen Sie nach „Hyper-V Manger“. Heften Sie „Hyper-V Manager“ an die Taskleiste.
9.  Öffnen Sie den „Hyper-V Manager“, klicken Sie mit der rechten Maustaste auf den lokalen Computer und wählen Sie **Hyper-V Settings** aus.
10. Wählen Sie im Dialogfeld **Hyper-V settings** unter „Server“ die Option **Virtual Machines** aus. Legen Sie den Speicherort des Ordners „Virtual Machines“ auf C:\\\VirtualMachines fest.
11. Wählen Sie im Dialogfeld **Hyper-V settings** unter „Server“ die Option **Virtual Machine Hard Disks** aus. Legen Sie den Speicherort der Festplatten des virtuellen Computers auf C:\\\VirtualMachines\\VHDs fest.
12. Klicken Sie auf **OK**, um das Dialogfeld **Hyper-V Settings** zu schließen.
13. Öffnen Sie eine administrative Eingabeaufforderung und führen Sie die folgenden Befehle aus, um ein NAT-Netzwerk zu erstellen.<br>`New-VMSwitch -SwitchName “NATSwitch” -SwitchType Internal`<br>`New-NetIPAddress -IPAddress 10.10.10.1 -PrefixLength 24 -InterfaceAlias “vEthernet (NATSwitch)”`<br>`New-NetNat -Name “NATNetwork” –InternalIPInterfaceAddressPrefix “10.10.10.0/24”`
14. Schließen Sie die administrative Eingabeaufforderung.

## Erstellen eines virtuellen Computers für einen Windows Server-Domänencontroller

In dieser Aufgabe stellen Sie einen Windows Server 2022-Domänencontroller für das Lab bereit, in dem Sie Aufgaben im Zusammenhang mit dem Applied Skill-Leistungsnachweis ausführen. Um diese Aufgabe auszuführen, stellen Sie sicher, dass Sie die ISO-Datei der Windows Server 2022 Evaluation Edition von [https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022) heruntergeladen haben. Legen Sie diese Datei im Ordner c:\\ISOs ab. Mit dieser Evaluierungs-ISO können Sie eine Vollversion von Windows Server 2022 bis zu 180 Tage lang ausführen.

1.  Wählen Sie im Menü **Actions** von Hyper-V Manager **New** und dann **Virtual Machine** aus.
2.  Klicken Sie auf der Seite „Before you Begin“ des Assistenten für neue virtuelle Computer auf **Next**.
3.  Geben Sie auf der Seite „Name und Ort angeben“ des Assistenten für neue virtuelle Computer den Namen **TAILWIND-DC1** ein, und klicken Sie auf **Weiter**.
4.  Wählen Sie auf der Seite „Specify Generation“ die Option **Generation 2** aus, und klicken Sie auf **Next**.
5.  Legen Sie auf der Seite „Assign Memory“ den Startspeicher auf 4096 MB fest, und lassen Sie die Option **Use Dynamic Memory for this virtual machine** ausgewählt. Klicken Sie auf **Weiter**.
6.  Wählen Sie auf der Seite „Configure Networking“ im Dropdownmenü die Verbindung auf „NATSwitch“, und klicken Sie auf **Next**.
7.  Akzeptieren Sie auf der Seite „Connect Virtual Hard Disk“ die Standardeinstellungen, und klicken Sie auf **Next**.
8.  Wählen Sie auf der Seite „Installationsoptionen“ die Option **Installieren eines Betriebssystems aus einer bootfähigen Image-Datei** aus, und klicken Sie dann auf **Durchsuchen**, um die ISO-Datei der Windows Server 2022 Evaluation Edition (mit dem Namen SERVER\_EVAL\_x64FRE\_en-us.iso) auszuwählen. Sie haben diese Datei bereits in den Ordner C:\\\ISOs heruntergeladen. Klicken Sie auf **Weiter**.
9.  Klicken Sie auf der Zusammenfassungsseite auf **Fertig stellen**.
10. Klicken Sie im Hyper-V Manager mit der rechten Maustaste auf TAILWIND-DC1, und wählen Sie **Settings** aus.
11. Wählen Sie auf der Seite „Settings“ von TAILWIND-DC1 unter „Management“ die Option **Checkpoints** aus, und stellen Sie sicher, dass die Option **Use automatic checkpoints** nicht ausgewählt ist, wie im Screenshot dargestellt. Klicken Sie auf **OK**.
    
    ![Screenshot der Auswahl „Checkpoints“ auf der Seite „Settings“](./Media/checkpoints.png)
12. Doppelklicken Sie auf TAILWIND-DC1. Dadurch wird das Fenster „Virtual Machine Connection“ geöffnet. Wählen Sie **Starten** aus. Wenn die Meldung „Press any key to boot from CD or DVD“ angezeigt wird, wählen Sie mit der Maus im Fenster des virtuellen Computers aus, und drücken Sie die Leertaste. Dadurch wird festgelegt, dass der virtuelle Computer aus der angefügten ISO-Datei gestartet wird.
13. Akzeptieren Sie auf der Seite „Microsoft Server Operating System Setup“ die Standardwerte, und klicken Sie auf **Next**.
14. Wählen Sie auf der Seite „Install now“ die Option **Install now** aus.
15. Wählen Sie auf der Seite „Microsoft Server Operating System Setup“ **Windows Server 2022 Standard Evaluation (Desktop Experience)** aus, wie im Screenshot gezeigt, und klicken Sie auf **Next**.
    
    ![Screenshot des Bildschirms „Microsoft Server Operating System Setup“ mit ausgewählter Option „Windows Server 2022 Standard Evaluation“](./Media/server-install.png)
    
17. Lesen Sie auf der Seite „Applicable notices and license terms“ die Lizenz durch, und aktivieren Sie dann das Kontrollkästchen **I Accept**. Klicken Sie auf **Weiter**.
18. Wählen Sie auf der Seite „Which type of installation do you want?“ die Option **Custom** aus.
19. Wählen Sie auf der Seite „Where do you want to install the operating system?“ die Option „Drive 0“ aus, und klicken Sie auf **Next**. Das Betriebssystem wird installiert. Dies dauert abhängig von der Geschwindigkeit des von Ihnen verwendeten Computers einige Minuten. Der virtuelle Computer wird neu gestartet.
20. Auf der Seite „Einstellungen anpassen“ werden Sie aufgefordert, ein Kennwort für das integrierte Administratorkonto einzugeben. Geben Sie zwei Mal das Kennwort **Pa55w.rdPa55w.rd** ein. Das Kennwort ist ein Demo-Kennwort und sollte nicht für Produktionssysteme verwendet werden. Sie können hier auch Ihr eigenes Kennwort auswählen. Nachdem Sie das Adminkennwort zweimal eingegeben haben, klicken Sie auf **Finish**. Sie werden nicht mit dem ausgeführten virtuellen Computer verbunden.
21. Geben Sie auf dem Sperrbildschirm des virtuellen Computers das Adminkennwort **Pa55w.rdPa55w.rd** ein, um sich anzumelden.
22. Klicken Sie nach der Anmeldung mit der rechten Maustaste auf das Netzwerksymbol, dargestellt durch einen Globus auf der Taskleiste, und wählen Sie die Option **Open Network & Internet Settings** aus.
23. Wählen Sie auf der Seite „Network Status“ die Option **Adapteroptionen ändern** aus.
24. Klicken Sie auf der Seite „Network Connections“ mit der rechten Maustaste auf **Ethernet**, und wählen Sie **Properties** aus.
25. Wählen Sie auf der Seite „Ethernet Properties“ das Element „Internet Protocol Version 4 (TCP/IPv4)“ aus, und klicken Sie auf **Properties**.
26. Legen Sie auf der Registerkarte „General“ der Seite „Internet Protocol Version 4 (TCP/IPv4) Properties“ die IP-Adresskonfiguration wie folgt fest, und klicken Sie auf **OK**:
    
    
    1.  Folgende IP-Adresse verwenden:
        
        
        1.  IP-Adresse: 10.10.10.10
        2.  Subnetzmaske: 255.255.255.0
        3.  Standardgateway: 10.10.10.1
    2.  Folgende DNS-Serveradressen verwenden:
        
        
        1.  Bevorzugter DNS-Server: 1.1.1.1
        2.  Alternativer DNS-Server: 8.8.8.8
27. Klicken Sie auf **Schließen**. Wenn Sie gefragt werden, ob der Computer auffindbar sein soll, wählen Sie **Yes** aus.
28. Öffnen Sie im Startmenü den Server-Manager, und wählen Sie Local Server und dann den Computernamen aus. Anschließend wird das Dialogfeld „System Properties“ geöffnet. Wählen Sie im Dialogfeld „System Properties“ auf der Seite „Computer Name“ die Option **Change** aus.
29. Ändern Sie im Dialogfeld „Computer Name/Domain Changes“ den Computernamen in **TAILWIND-DC1**, und klicken Sie dann auf **OK**.<br>
30. Klicken Sie im Dialogfeld dafür, dass Sie den Computer neu starten müssen, auf **OK**.
31. Wählen Sie im Dialogfeld „System Properties“ die Option **Close** aus.
32. Klicken Sie im Dialogfeld **You must restart your computer to apply these changes** auf **Restart Now**. Der Computer wird neu gestartet.
33. Melden Sie sich nach dem Neustart des Computers mit dem Kennwort, das Sie während der Installation konfiguriert haben, als Admin an.
34. Wählen Sie im Server-Manager das Menü „Manage“ und dann **Add Roles and Features** aus.
35. Wählen Sie auf der Seite „Before you begin“ des Assistenten zum Hinzufügen von Rollen und Features die Option **Next** aus.
36. Wählen Sie auf der Seite „Select installation type“ die Option **Role-based or feature-based installation** aus, und klicken Sie auf **Next**.
37. Klicken Sie auf der Seite „Select destination server“ auf **Select a server from the server pool**. Stellen Sie sicher, dass **TAILWIND-DC1** ausgewählt ist, und klicken Sie auf **Weiter**.
38. Aktivieren Sie auf der Seite „Select server roles“ das Kontrollkästchen **Active Directory Domain Services**. Dadurch wird die Seite „Add features“ geöffnet. Wählen Sie **Features hinzufügen** aus. Klicken Sie auf der Seite „Select server roles“ auf **Weiter**.
39. Klicken Sie auf der Seite "Features auswählen" auf **Weiter**.
40. Klicken Sie auf der Seite „Active Directory Domain Services“ auf **Next**.
41. Wählen Sie auf der Seite „Confirm installation selections“ die Option **Install** aus. Je nach Geschwindigkeit des Computers kann die Installation einige Minuten dauern. Klicken Sie nach Abschluss der Installation auf **Schließen**.
42. Wählen Sie im Server-Manager-Menü das Benachrichtigungssymbol neben der Flagge in der oberen rechten Ecke aus, wie im Screenshot zu sehen.

    ![Screenshot des Server-Manager-Menüs mit angezeigtem Warnsymbol.](./Media/server-manager-menu.png)
43. Wählen Sie im Menü, das sich öffnet, wenn Sie das Benachrichtigungssymbol auswählen, die Option **Promote this server to a domain controller** aus. Dies startet den Konfigurations-Assistent für die Active Directory Domain Services
44. Wählen Sie auf der Seite „Deployment Configuration“ die Option **Add a new forest** aus, und legen Sie den Namen der Stammdomäne auf **tailwindtraders.internal** fest. Klicken Sie auf **Weiter**.
45. Akzeptieren Sie auf der Seite „Domain Controller options“ die Standardeinstellungen, und geben Sie das Kennwort für den Wiederherstellungsmodus der Verzeichnisdienste (DSRM) ein. Geben Sie dazu zweimal das folgende Kennwort ein: Pa55w.rdPa55w.rd. Klicken Sie auf **Weiter**.
46. Klicken Sie auf der Seite „DNS Options“ auf **Next**.
47. Klicken Sie auf der Seite „Additional Options“ auf **Next**.
48. Klicken Sie auf der Seite „Pfade“ auf **Next**.
49. Klicken Sie auf der Seite „Review Options“ auf **Next**.
50. Klicken Sie auf der Seite „Prerequisites Check“ auf **Install**. Die Installation dauert je nach Geschwindigkeit des virtuellen Computers mehrere Minuten. Der virtuelle Computer wird neu gestartet.
51. Melden Sie sich beim Neustart des virtuellen Computers als **tailwindtraders\\administrator** mit dem Kennwort an, das Sie für das Standard-Administratorkonto (Pa55w.rdPa55w.rd) konfiguriert haben.

## Erstellen eines Windows Server-Domänenmitgliedsservers

In dieser Aufgabe stellen Sie einen Windows Server 2022-Domänenmitgliedsserver für das Lab bereit und konfigurieren ihn, in dem Sie Aufgaben im Zusammenhang mit dem Applied Skill-Leistungsnachweis ausführen. Diese Aufgabe verwendet auch die iso-Datei der Auswertungsedition.

1.  Wählen Sie im Hyper-V-Manager im Menü „Actions“ die Option **New** und dann **Virtual Machine** aus.
2.  Klicken Sie auf der Seite „Before you Begin“ des Assistenten für neue virtuelle Computer auf **Next**.
3.  Geben Sie auf der Seite „Name und Ort angeben“ des Assistenten für neue virtuelle Computer den Namen **TAILWIND-MBR1** ein, und klicken Sie auf **Weiter**.
4.  Wählen Sie auf der Seite „Specify Generation“ die Option **Generation 2** aus, und klicken Sie auf **Next**.
5.  Legen Sie auf der Seite „Assign Memory“ den Startspeicher auf 4096 MB fest, und lassen Sie die Option **Use Dynamic Memory for this virtual machine** ausgewählt. Klicken Sie auf **Weiter**.
6.  Wählen Sie auf der Seite „Configure Networking“ im Dropdownmenü die Verbindung **NATSwitch** aus, und klicken Sie auf **Next**.
7.  Akzeptieren Sie auf der Seite „Connect Virtual Hard Disk“ die Standardeinstellungen, und klicken Sie auf **Next**.
8.  Wählen Sie auf der Seite „Installationsoptionen“ die Option **Installieren eines Betriebssystems aus einer bootfähigen Image-Datei** aus, und klicken Sie dann auf **Durchsuchen**, um die iso-Datei der Windows Server 2022 Evaluation Edition (mit dem Namen SERVER\_EVAL\_x64FRE\_en-us.iso) auszuwählen, die Sie in den Ordner C:\\ISOs heruntergeladen haben. Klicken Sie auf **Weiter**.
9.  Klicken Sie auf der Zusammenfassungsseite auf **Fertig stellen**.
10. Klicken Sie im Hyper-V-Manager mit der rechten Maustaste auf **TAILWIND-MBR1**, und wählen Sie **Settings** aus.
11. Wählen Sie auf der Seite „Settings“ von TAILWIND-MBR1 unter „Management“ die Option „**Checkpoints**“ aus, stellen Sie sicher, dass die Option **Use automatic checkpoints** nicht ausgewählt ist. Klicken Sie dann auf **OK**.
12. Doppelklicken Sie auf TAILWIND-MBR1. Dadurch wird das Fenster für die Verbindung mit virtuellen Computern geöffnet. Klicken Sie auf **Start**. Wenn die Nachricht „Press any key to boot from CD or DVD“ angezeigt wird, klicken Sie mit der Maus in das Fenster des virtuellen Computers, und drücken Sie die Leertaste. Dadurch wird festgelegt, dass der virtuelle Computer aus der angefügten ISO-Datei gestartet wird.
13. Akzeptieren Sie auf der Seite „Microsoft Server Operating System Setup“ die Standardwerte, und klicken Sie auf **Next**.
14. Klicken Sie auf der Seite „Install now“ auf die Option **Install now**.
15. Wählen Sie auf der Seite „Microsoft Server Operating System Setup“ die Option **Windows Server 2022 Standard Evaluation (Desktop Experience)** aus, und klicken Sie auf **Next**.
16. Lesen Sie auf der Seite „Applicable notices and license terms“ die Lizenz durch, und aktivieren Sie dann das Kontrollkästchen **I Accept**. Klicken Sie auf **Weiter**.
17. Wählen Sie auf der Seite „Which type of installation do you want?“ die Option **Custom** aus.
18. Wählen Sie auf der Seite „Where do you want to install the operating system?“ **Drive 0** aus, und klicken Sie auf **Next**. Das Betriebssystem wird installiert. Dies dauert abhängig von der Geschwindigkeit des von Ihnen verwendeten Computers einige Minuten. Der virtuelle Computer wird neu gestartet.
19. Auf der Seite „Einstellungen anpassen“ werden Sie aufgefordert, ein Kennwort für das integrierte Administratorkonto einzugeben. Geben Sie zwei Mal das Kennwort **Pa55w.rdPa55w.rd** ein. Das Kennwort ist ein Demo-Kennwort und sollte nicht für Produktionssysteme verwendet werden. Sie können hier auch Ihr eigenes Kennwort auswählen. Nachdem Sie das Adminkennwort zweimal eingegeben haben, wählen Sie **Finish** aus. Sie werden nicht mit dem ausgeführten virtuellen Computer verbunden.
20. Geben Sie auf dem Sperrbildschirm des virtuellen Computers das Adminkennwort **Pa55w.rdPa55w.rd** ein, um sich anzumelden.
21. Nachdem Sie sich angemeldet haben, klicken Sie mit der rechten Maustaste auf das Netzwerksymbol, das durch einen Globus in der Taskleiste dargestellt wird, und wählen Sie **Open Network & Internet Settings** aus.
22. Wählen Sie auf der Seite „Network Status“ die Option **Adapteroptionen ändern** aus.
23. Klicken Sie auf der Seite „Network Connections“ mit der rechten Maustaste auf **Ethernet**, und wählen Sie **Properties** aus.
24. Wählen Sie auf der Seite „Ethernet Properties“ das Element **Internet Protocol Version 4 (TCP/IPv4)** aus, und klicken Sie auf **Properties**.
25. Legen Sie auf der Registerkarte „General“ der Seite „Internet Protocol Version 4 (TCP/IPv4) Properties“ die IP-Adresskonfiguration wie folgt fest, und klicken Sie auf **OK**:
    
    
    1.  Folgende IP-Adresse verwenden:
        
        
        1.  IP-Adresse: 10.10.10.20
        2.  Subnetzmaske: 255.255.255.0
        3.  Standardgateway: 10.10.10.1
    2.  Folgende DNS-Serveradressen verwenden:
        
        
        1.  Bevorzugter DNS-Server: 10.10.10.10
        2.  Alternativer DNS-Server: 8.8.8.8
26. Klicken Sie auf **Schließen**. Wenn Sie gefragt werden, ob der Computer auffindbar sein soll, wählen Sie **Yes** aus.
27. Öffnen Sie im Startmenü den Server-Manager, und wählen Sie **Local Server** und dann den Computernamen aus. Anschließend wird das Dialogfeld „System Properties“ geöffnet. Wählen Sie im Dialogfeld „System Properties“ auf der Seite „Computer Name“ die Option **Change** aus.
28. Ändern Sie im Dialogfeld „Computer Name/Domain Changes“ den Computernamen in **TAILWIND-MBR1**, und klicken Sie dann auf **OK**.<br>
29. Klicken Sie im Dialogfeld, das Sie darüber informiert, dass Sie Ihren Computer neu starten müssen, auf **OK**.
30. Klicken Sie im Dialogfeld **Systemeigenschaften** auf „Schließen“.
31. Klicken Sie im Dialogfeld „You must restart your computer to apply these changes“ auf **Restart Now**. Der Computer wird neu gestartet.
32. Melden Sie sich nach dem Neustart des Computers mit dem Kennwort, das Sie während der Installation konfiguriert haben, als Admin an.
33. Wählen Sie in der Server-Manager-Konsole den Abschnitt „Local Server“ aus. Wählen Sie im Abschnitt „Local Server“ „TAILWIND-MBR1“ neben „Computer Name“ aus. Anschließend wird das Dialogfeld „System Properties“ geöffnet.
34. Klicken Sie im Dialogfeld „System Properties“ auf **Change**.
35. Wählen Sie im Dialogfeld „Computer Name/Domain Changes“ die Option **Domain under Member of** aus, geben Sie den Domänennamen **TAILWINDTRADERS,** ein, und klicken Sie auf **OK**.
36. Geben Sie im Dialogfeld „Computer Name/Domain Changes“ den folgenden Benutzernamen und das folgende Kennwort ein, und klicken Sie auf **OK**:
    
    
    1.  Benutzername: TAILWINDTRADERS\\Administrator
    2.  Kennwort: Pa55w.rdPa55w.rd
37. Im Moment wird das Dialogfeld „Welcome to the Tailwintraders domain“ angezeigt. Klicken Sie auf **OK**.
38. Klicken Sie im Dialogfeld **Systemeigenschaften** auf „Schließen“.
39. Klicken Sie im Dialogfeld, in dem Sie aufgefordert werden, den Computer neu zu starten, auf **Restart Now**.
