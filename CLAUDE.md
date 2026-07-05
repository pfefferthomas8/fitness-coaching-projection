# Thomas Pfeffer - Projection Tool

## Projekt
Interaktives Körper-Projektions-Tool (kostenlos). Nutzer berechnen ihre realistische Körper-Transformation. Danach führt das Tool in den Funnel: kostenlose Projektion → 19 € persönliche Analyse → 2.497 € Coaching. Kein Lead-Formular mehr, keine Telefonnummer-Abfrage. Der CTA leitet auf die Analyse-Seite weiter und reicht alle Tracking-Parameter mit.

## Design System
- Background: #0a0a0a
- Cards: #141414 mit Border #1f1f1f
- Accent (CTAs, Highlights): #ee4f00
- Text primär: #e8e8e8
- Text sekundär: #888888
- Text dezent: #555555
- Font: DM Sans via Google Fonts (Weights 400/500/600/700)
- Max-Width: 480px zentriert, Mobile-first
- Border-Radius: Karten 18px, Buttons 12-14px, Badges 20px
- Buttons: #ee4f00 Background, weiß Text, box-shadow: 0 4px 20px rgba(238,79,0,0.25)
- CTA-Boxen: background linear-gradient(135deg, rgba(238,79,0,0.09), rgba(238,79,0,0.03)) mit border 1px solid rgba(238,79,0,0.19)
- Labels/Badges: Uppercase, 11px, letter-spacing 0.1em

## Stack
- Single HTML file (index.html), kein Framework, kein Build-Step
- Gehostet auf Cloudflare Pages via GitHub
- Auto-deploy bei jedem Push auf main

## Services & Keys
- Meta Pixel ID: 2039462596786177
- Pushover: API Token a5b6aohsr31wf1c523r9bqa7r5bdsc / User Key usfd8f7r5md97mdycq1mjcug8swqeh (Priority 0, Sound cashregister)
- (EmailJS wurde mit dem Lead-Formular entfernt – nicht mehr im Einsatz)

## Funnel & Weiterleitung
- Kostenlose Projektion → CTA "Mehr zur persönlichen Analyse" → https://www.form-training.at/analyse/ → dort läuft der eigentliche Verkauf (19 € Analyse → 2.497 € Coaching)
- Abschluss-Block (`#ctaBox`) ist bewusst hochwertig gehalten: Eyebrow "Dein nächster Schritt" + feine Akzentlinie oben, Headline "Du weißt jetzt, was möglich ist.", Frage "Warum stehst du heute noch nicht dort?", Überleitung zur Analyse, dezente Preis-Pille "Persönliche Analyse · 19 €", Full-Width-Button. Keine Bullets, keine Coaching-/Telefon-Texte.
- Mobile-Umbrüche: `text-wrap:balance` (Headline/Subline/Button) + `text-wrap:pretty` (Fließtext) + gezielte `&nbsp;` gegen Orphan-Words. Auf 390px und im 480px-Container geprüft.
- CTA ist ein normaler `<a>`-Link. Beim Laden und nach jeder Berechnung wird die href via `refreshAnalyseUrl()` neu gebaut (`buildAnalyseUrl()`), inkl. aller Tracking-Parameter und der Projektionsdaten (`pj=`), damit ein Kauf auf form-training.at dem IG-Kontakt zugeordnet werden kann.

## Tracking
- Herkunft aus der DM-Link-URL: `?ref=<ig_handle>&utm_source=instagram&utm_medium=dm&utm_campaign=projektion`. `ref` = pro Empfänger anpassen (IG-Handle), so sieht Thomas, wer geklickt/gekauft hat.
- `TRACK`-Modul (Top des Scripts) liest ref/utm, vergibt persistente Visitor-ID (`pj_vid` in localStorage), persistiert Werte und reicht alle eingehenden Query-Params an die Analyse-URL weiter.
- Meta Pixel Funnel:
  1. PageView → Seite geladen
  2. ProjektionOpen (Custom) → Öffnen aus einer DM (nur wenn `ref` gesetzt)
  3. ViewContent → Projektion berechnet
  4. AnalyseClick (Custom) → CTA "Persönliche Analyse holen" geklickt (Überleitung zur Analyse-Seite)
  - Hier wird BEWUSST KEIN InitiateCheckout gefeuert. Der Überleitungs-Klick ist noch kein Checkout-Intent.
  - InitiateCheckout (value 19, EUR) entsteht erst auf form-training.at/analyse beim Klick auf den Stripe-19-€-Button.
  - Alle Events tragen Custom Data: ref, utm_source/medium/campaign, visitor_id.
  - Der eigentliche Purchase (19 €) wird auf form-training.at/analyse gefeuert (separates Projekt).
- Echtzeit-Push: Beim ersten CTA-Klick pro Visitor geht eine Pushover-Benachrichtigung an Thomas (ref, Quelle, Projektion, Visitor-ID) via `navigator.sendBeacon` (übersteht die Navigation). Guard `pj_clicked` in localStorage verhindert Mehrfach-Pushes.

## Projektions-Engine
- Zielauswahl: Fettabbau oder Muskelaufbau
- Eingaben: Gewicht, KFA, Trainingserfahrung, Trainingshäufigkeit, Zeitraum
- 82% Adherence eingerechnet (nicht sichtbar für User, Text sagt "Realistische Projektion")
- KFA-Floors: Beginner 17%, Intermediate 16%, Advanced 15% (bewusst hoch – kein Bodybuilding-Coaching, Zielgruppe Männer 30+)
- Deceleration nahe am Floor (exponentiell)
- Trainingsfrequenz-Multiplikatoren: 2x=0.75, 3x=1.0, 4x=1.15, 5x=1.22
- Ergebnisse: 4 Karten (Gewicht, KFA, Muskelmasse, Fettmasse) mit Sparkline-Charts
- Meilensteine: Monat 3, 6, 9, 12, 18, 24
- Lifestyle-Impact-Balken: Energielevel, Selbstwahrnehmung, Belastbarkeit (mit dynamischer %-Anzeige und Beschreibungen)

## Tonalität & Regeln
- Zielgruppe: Männer 30+, Unternehmer, Selbstständige, Führungskräfte
- Ton: Ruhig, direkt, faktisch. Kein Hype, keine Motivationssprüche
- Kernbotschaft: "Du bist nicht kaputt. Dein Problem ist normal und hat eine klare Ursache."
- Keine Emojis im Content (außer Ziel-Buttons 🔥💪)
- Deutsch, natürlich formuliert, keine AI-typischen Formulierungen
- Keine Bindestriche im Copy
- "Männer in Topform" oder "fitte Männer", nie "schlanke Männer"
- Keine verwaisten Wörter am Zeilenende (Orphan Words vermeiden)
- Footer: Thomas Pfeffer · Online Fitness Coach für Männer 30+

## Coaching Details
- Premium 1:1 Online Coaching
- Erster Monat 597€, danach 397€/Monat, Mindestlaufzeit 3 Monate
- App: Traindoo (Trainingspläne, Tracking, Kommunikation)
- Individueller Trainingsplan, Ernährungsfahrplan, 400+ Rezepte
- KI-Makrotracking (Foto/Sprachnachricht), täglicher WhatsApp-Support
- Wöchentliches Feedback mit Analyse und Anpassungen

## Wichtig bei Änderungen
- Immer git add, commit und push nach Änderungen
- Keine externen CSS/JS Dateien, alles bleibt in einer HTML-Datei
- Bei Textänderungen auf Orphan Words achten (kein einzelnes Wort in letzter Zeile)
- Pushover Priority muss auf 0 bleiben (respektiert Lautlos-Modus)
