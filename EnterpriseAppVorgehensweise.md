Um eine App mithilfe von Xcode für Enterprise oder AdHoc Distribution zu builden benötigt man ein DistributionCodesigningCertificate, ein Provisioning Profile und eine App Id.

Die App Id kann man im Enterprise Portal unter Certificates IDs & Profiles>App IDs anlegen.

Ein DistributionCodeSigningCertificate kann in Xcode erstellt werden. Wenn bereits ein DistributionCodeSigningCertificate vorhanden ist sollte es aber verwendet werden.
Um ein vorhandenes DistributionCodeSigningCertificate von Xcode zu exportieren kann man in Xcode unter Xcode >Preferences>Accounts den Account auswählen, der mit dem Enterprise Programm verbunden ist.
Im Anschluss kann man unter Manage Certificates mit der rechten Maustaste auf das Certificate klicken und es mit Passwort exportieren. Xcode erstellt darauf hin eine neue Datei, die das Certificate enthält.
Um das Certificate auf einem neuen Rechner zu installieren kann man die Datei einfach doppelt anklicken.

Das ProvisioningProfile kann ebenfalls im Enterprise Portal erstellt werden.
Dazu unter Certificates IDs & Profiles>All>+
Es ist auch möglich, ein ProvisioningProfile für mehrere Apps zu verwenden.

Wenn ProvisioningProfile, CodeSigningCertificate und App ID bereit sind kann die App in Xcode für Enterprise oder AdHoc Distribution gebuilded werden.
Dazu zunächst das Xcode Projekt öffnen. Und das Projekt archivieren: Product> Archive.

Im Anschluss können die Archivierten Projekte unter Window>Organizer angezeigt werden.

Um ein Projekt zu builden klickt man nun im Organizer auf „Distribute App“ oder „Export“ (je nach Xcode Version).

Die App kann für AdHoc oder Enterprise Distribution gebuildet werden.
Der Unterschied besteht darin, dass AdHoc Apps nur auf bestimmten Geräten installiert werden dürfen, die man vorher im ProvisioningProfile festlegt.

Im nächsten Schritt wählt man den Punkt „Include Manifest for over-the-air installation“ aus und und klickt auf Next.

Nun muss man drei URLs angeben: Eine für die APP und zwei für Icons.
Hier ist es sinnvoll, zunächst Platzhalter URLs anzugeben.

Im nächsten schritt wählt man den Punkt „Manually manage signing an“ und wählt dann sein CodeSigningCertificate und Provisionning Profile aus.

Nun wird die App für IOS gebuilded .
Als Resultat erhält man einen Ordner, der unter anderem eine Projektname.ipa Datei und eine manifest.plist Datei enthält.
Die Projektname.ipa Datei enthält die kompilierte App, während die manifest.plist Datei Informationen über die App inklusive eines Downloadlinks enthält.

Der Inhalt der .plist Datei sollte folgendermaßen strukturiert sein:

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>items</key>
	<array>
		<dict>
			<key>assets</key>
			<array>
				<dict>
					<key>kind</key>
					<string>software-package</string>
					<key>url</key>
					<string>https://downloadurl</string>
				</dict>
			</array>
			<key>metadata</key>
			<dict>
				<key>bundle-identifier</key>
				<string>com.psiori.appname</string>
				<key>bundle-version</key>
				<string>1.0</string>
				<key>kind</key>
				<string>software</string>
				<key>title</key>
				<string>AppName</string>
			</dict>
		</dict>
	</array>
</dict>
</plist>


Hier hat man die Auswahl zwischen AdHoc und Enterprise Distribution.

Für die Installation kann man nun beide Dateien auf Dropbox platzieren.
Zum download 

Alle Geräte, auf denen Apps über AdHoc Distribution installiert werden müssen im Enterprise Portal über ihre UDID registriert sein.
Dazu im Apple Enterprise Portal unter Certificates IDs & Profiles > Devices > +
