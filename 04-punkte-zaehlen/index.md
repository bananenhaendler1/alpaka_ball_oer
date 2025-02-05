---
Title: "Level 3: Tore / Punkte zählen"
Draft: false
Weight: 40

---

# Level 3: Tore / Punkte zählen

So, wir haben Tore, einen Ball - aber aktuell werden die Tore noch nicht gezählt. Das packen wir in diesem Level an!

{{% notice note "Variablen - eine kurze Einführung" %}}

Was ist genau eine Variable? Variable hört sich an wie „variabel“, also veränderbar. Am besten kannst du dir eine Variable wie einen dieser Klebezettel vorstellen. Die sind super, um sich Sachen zu merken!

**Hintergrund: Variablen-Typen**

Es gibt verschiedene Arten von Variablen, je nach dem, was man sagen will:

- Ja / Nein – Boolean
- Text – String
- Einfache Zahlen (1,2,3…) – Integer
- Komma-Zahlen (3,1415) – Float

Und noch ganz viele mehr…

**Achtung: Gute Namen sind gute Helfer**

Variablen-Namen können nur aus einem Buchstaben, aber auch aus ganzen Wörtern bestehen. Wähle also weise: Gib den Variablen Namen, die andere (und auch du nach 2 Wochen) noch verstehen. Dann findest du dich viel leichter im eigenen Programm zurecht. 

{{% /notice %}} 

## Punkte merken

Wir erstellen also eine Variable - In dieser merken wir uns jeweils die Tore / Punkte pro Team

![So erstellst du eine neue Variable](variable-erstellen.png)

Dazu erstellen wir eine Variable für jedes Team:

1. In der seitlichen Leiste *Variablen* auswählen
2. Eine *Neue Variable hinzufügen*
3. *Variablenname* vergeben und Typ *Variablentyp* auf *number* setzen
4. mit *Ok* speichern
5. ...das gleiche nochmal für die andere Farbe

## Tore erkennen

Jetzt müssen wir nur noch erkennen, wenn ein Tor geschossen wurde. Genau - da gab's ja was - die "Auslöser". Wir suchen also einen Auslöser, der erkennt, wenn ein Tor geschossen wurde.

![Auslöser: So erkennt das Tor, was gerade passiert](torblock-ausloeser.png)  

Wir fügen 2 Auslöser hinzu:

- einen *Wenn Block rechts geklickt wird*,  
  um Punkte zurück zu setzen.
- einen *Wenn Entität im Block zusammenstößt*,  
  um Punkte hoch zu zählen und Ball zu entfernen

### Prozedur 1: Punkte zurücksetzen 

![Code, um die Tore zurückzusetzen](code-rechtsklick.png)

In diesem Fall möchten wir, dass die Punkte des Teams auf "0" gesetzt werden und dass die Bossbar auch zurückgesetzt wird. Dafür verwenden wir folgende Befehle:

1. Setzt die globale Variable zum Punkte Zählen auf 0 zurück
2. Führt `/bossbar set blue value 0` in Minecraft aus, um die Bossbar wieder auf 0 zu setzen.

### Prozedur 2: Tore zählen  

Um die Tore zu zählen, haben wir einen Auslöser erstellt, der immer startet, wenn er vom Ball berührt wird.

Die Prozedur für den Zusammenstoß mit einer Entity ist länger und sieht so aus:

![Code, um die Tore zu zählen](code-zusammenstoss-entitaet.png)

1. Tore sollen nur bei Ball-Kontakt gezählt werden: Als erstes prüft das Programm, ob es sich bei der Entität um einen Ball handelt
2. Dazu "holen" wir uns den Anzeige-Namen der "Berührenden Entity" mit `Erhalte den Anzeige-Namen von Event/target entity` und prüfen ob der gleich dem String `Flugball` ist. (Muss übereinstimmen, wie der Objektname bei [Bild und Ton von *Ball erstellen*](../02-ball-erstellen/ball-erstellen.md))
3. Diese beiden Zeilen, die vom Hauptcodeblock abgelöst sind, werden nicht ausgeführt. Sie sind nur ein Hinweis darauf, was wir probiert haben: Bei der (3) wollten wir auf diese beiden Wege testen ob es sich um einen Ball handelt. Das hat leider nicht geklappt.
4. Erhöhe die Punktzahl von Blau: 
    - dazu holt es sich die aktuelle `punktzahl_blau` 
    - und fügt mit *+* 
    - die Zahl *1* hinzu 
    - und speichert das Ergebnis mit `Setze Global: punktzahl` zu wieder in der Punktezahl für blau ab.
5. Wir führen den Minecraft Befehl für die Bossbar aus - den kennst du ja schon aus Level 3.
6. Dazu kombinieren wir den text `/bossbar set blue value ` **(!Achtung! Leerzeichen am Ende wichtig, damit es funktioniert)** mit der `punktzahl_blau` und runden diese, weil es sich sonst um eine Kommazahl handelt. (zwar immer ,0 aber Minecraft kennt hier keine Kommazahl)
7. Wir geben dem/der Spieler*in, der/die am nächsten steht (`@p`) ein neues Spawn-Ei  
    `/give @p alpaka_ball:flugball_spawn_egg`
8. Wenn ein Tor fällt, muss man das natürlich auch hören: Mit diesem Befehl können wir einen Ton abspielen lassen, wenn ein Tor geschossen wurde. Hier z.B. der gleiche Ton, wenn man XP aufsammelt: *entity.experience_orb.pickup*
9. Am Schluss wollen wir den Ball "los werden" - er soll verschwinden und mit einem neuen Ball geht es weiter.  
    - dazu am besten den Befehl `Zerstöre` verwenden
    - Achtung: die Minecraft befehle `kill @e[...]`, `tp @e[...] ~ -500 ~` und MCreator `Lösche` funktionieren nicht.
10. **Speichern nicht vergessen ;)**

{{% notice note "Blau bekommt einen Punkt?"%}}
Vielleicht wunderst du Dich, warum wir jetzt dem blauen Team einen Punkt geben, wenn ein Ball ins blaue Tor geht - müsste ja eigentlich anders rum sein, oder? 
Aber sobald mehr als zwei Teams mitspielen, würde es nicht mehr funktionieren. Mit 12 Punkten hat man also verloren.
{{% /notice %}} 

{{% notice task "Alternative: Punkte abziehen"%}}  
Wenn ihr wollt könnt ihr am Anfang auch 12 Punkte vergeben und mit jedem Tor in den blauen Torblock 1 Punkt von Blau abziehen.
Spielt gerne mit den Zahlen rum ;)  
{{% /notice %}}  

{{% notice success "Geschafft! Tore zählen - ich habe fertig!" %}}  
Jetzt kann's im Spiel getestet werden, und wenn ein Ball in einen blauen Torblock fliegt, dann sollte ein Ton kommen, die Punktzahl in der Bossbar erhöht werden, der Ball verschwinden und man bekommt ein neues Spawn-Ei.  
{{% /notice %}}


### Jetzt nochmal für Orange
Die Variable `punktezahl_orange` für Orange hatten wir bereits erstellt - Jetzt fehlen nur noch die passenden Prozeduren, die wir vom Team Blau kopieren können.

- Gehe zum **Arbeitsplatz**
- Rechts auf die Prozedur klicken - wähle **Mod-Elemnet duplizieren**
- Nenne die neuen Prozeduren ...Orange... statt ...Blau...

![Faulheit siegt, Arbeit sparen: Dupliziere den bestehenden Code](ide-code-kopieren.png)

Jetzt natürlich noch alle Dinge von Blau zu Orange ändern in den beiden Codedateien:

![Neuer Code - Zusammenstoß für Orange...](code-zusammenstoss-entitaet-orange.png)

![... und der Rechts-Click-Code für Orange.](code-rechtsklick-orange.png)



![Und nicht vergessen: Auslöser auch anpassen](torblock-ausloeser-orange.png)

{{% notice task "Funktioniert's?"%}}  
Und nochmal testen ;)

Wenn was nicht klappt, schau oben Schritt für Schritt alles durch, ob du etwas vergessen hast.

{{% /notice %}}
