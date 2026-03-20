# Thomas Pfeffer - Projection Tool

## Projekt
Interaktives Körper-Projektions-Tool für Premium 1:1 Online Fitness Coaching. Leads berechnen ihre realistische Körper-Transformation und bewerben sich direkt über ein integriertes 3-Fragen-Formular.

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
- EmailJS: Service service_vm4yypj / Template template_v8acq6m / Public Key ozP5yS651iffhazkF
- Pushover: API Token a5b6aohsr31wf1c523r9bqa7r5bdsc / User Key usfd8f7r5md97mdycq1mjcug8swqeh (Priority 0, Sound cashregister)

## Pixel Funnel
1. PageView → Seite geladen
2. ViewContent → Projektion berechnet
3. InitiateCheckout → "Für 1:1 Coaching bewerben" geklickt
4. Lead → Formular abgeschickt

## Lead-Formular (3 Fragen)
1. Name (Textfeld)
2. Situation (Multiple Choice: Voller Kalender / Keine Veränderung / Komme nicht wieder rein / Weiß nicht wo anfangen)
3. WhatsApp-Nummer (Textfeld)

Bei Absenden: EmailJS E-Mail + Pushover Push-Notification gleichzeitig. Beide enthalten Name, Situation, Telefonnummer, Projektionsdaten und Zeitstempel.

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
