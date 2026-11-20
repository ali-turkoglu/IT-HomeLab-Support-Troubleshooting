# Fall 001 – Anmeldung am Windows-PC nicht möglich

| Punkt | Details |
|---|---|
| GLPI-Ticket | #3 |
| Typ | Störung / Incident |
| Kategorie | User Accounts & Access |
| Priorität | Mittel |
| Status | Geschlossen |
| Umgebung | Windows-Domäne im HomeLab, Active Directory, GLPI |

## Ziel und Umfang

In diesem Fall übe ich den Ablauf eines Support-Tickets: Informationen sammeln, Einstellungen prüfen, Ergebnisse dokumentieren und das Ticket schließen. Ich übernehme dabei die Rolle des Benutzers und des Technikers.

Die Störung ist simuliert. Das Konto wurde nicht wirklich gesperrt oder entsperrt. Ein Anmeldetest wurde nicht durchgeführt.

## 1. Meldung des Benutzers

Der Benutzer kann sich nicht mit seinem Firmenkonto am Windows-PC anmelden. Am Vortag hat die Anmeldung noch funktioniert.

Ich frage nach der genauen Fehlermeldung und bitte um einen Screenshot ohne persönliche Daten.

In der simulierten Antwort bestätigt der Benutzer, dass er das Tastaturlayout und die Feststelltaste geprüft hat. Er meldet: „Das Benutzerkonto ist gesperrt.“

## 2. Benutzerkonto prüfen

Ich öffne **Active Directory Users and Computers** und prüfe das Testkonto `finance.user01` unter **Properties → Account**.

Hier befindet sich die Funktion **Unlock account**. Damit kann ein gesperrtes Konto entsperrt werden. In diesem Fall führe ich keine Entsperrung durch.

![Kontoeinstellungen und die Funktion Unlock account](../assets/case-001/01-ad-account-settings.png)

## 3. Kennwortrichtlinien prüfen

### Default Domain Policy

In **Group Policy Management** prüfe ich die **Account Lockout Policy**. Der Wert **Account lockout threshold** ist auf **0** gesetzt. Diese Richtlinie sperrt Konten bei falschen Passworteingaben nicht automatisch.

### Richtlinie für den Benutzer

Die allgemeine Domain-Richtlinie allein reicht für die Prüfung nicht aus. Für einzelne Benutzer oder Gruppen kann eine besondere Kennwortrichtlinie gelten.

Im **Active Directory Administrative Center** wähle ich beim Testbenutzer **View resultant password settings**.

Für `finance.user01` gilt die **Finance department Password Policy**. Dort ist **Enforce account lockout policy** nicht aktiviert. Die grau angezeigten Zeitwerte sind deshalb nicht aktiv.

## 4. Ergebnis dokumentieren

Die geprüften Einstellungen bestätigen keine automatische Kontosperrung durch falsche Passworteingaben. Ich ändere keine Einstellungen.

Ich dokumentiere die Prüfungen und Ergebnisse als private Notiz in GLPI.

![Private technische Notiz in GLPI](../assets/case-001/02-glpi-investigation-note.png)

Bei einer echten Kontosperrung würde ich das Konto entsperren und den Benutzer um einen erneuten Anmeldetest bitten. Wenn sich das Konto wieder sperrt, würde ich die Ursache weiter prüfen, zum Beispiel alte gespeicherte Passwörter und passende Ereignisprotokolle.

## 5. Ticket abschließen

Ich trage das Ergebnis der Simulation als Lösung ein. Danach akzeptiere ich die Lösung mit dem Benutzerkonto in GLPI. Das Ticket erhält den Status **Closed**.

Der Abschluss bestätigt das Ende der Übung. Er bestätigt keine tatsächlich behobene Anmeldestörung.

![Geschlossenes GLPI-Ticket Nummer 3](../assets/case-001/03-glpi-ticket-closed.png)

## Was ich gelernt habe

- Zuerst nach der genauen Fehlermeldung fragen.
- Benutzerkonto und geltende Kennwortrichtlinie getrennt prüfen.
- Eine besondere Kennwortrichtlinie kann für den Benutzer gelten.
- Nur notwendige Informationen im Ticket dokumentieren.
- Zwischen einer Simulation und tatsächlich durchgeführten Änderungen unterscheiden.

---

[Zurück zu IT Support & Troubleshooting](../README.md)

