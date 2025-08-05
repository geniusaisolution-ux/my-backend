# Check24 Partner Program Integration

## Übersicht

Die Check24 Tracking-ID wurde erfolgreich in alle relevanten Stellen der GENIUS.AI-Plattform implementiert. Die Integration ermöglicht es, Provisionen durch Weiterleitung von Nutzern zu Check24-Vergleichsportalen zu generieren.

## Implementierte Funktionen

### 1. Backend Tracking Service (`server/services/tracking.ts`)
- **Check24 URL-Generierung**: Dynamische Erstellung von Affiliate-URLs mit Partner-ID
- **Kategorien-Support**: Energie (Strom, Gas, Ökostrom), Telekommunikation (Internet, Mobilfunk), Versicherungen (KFZ, Haftpflicht, Hausrat)
- **Click-Tracking**: Nachverfolgung von Nutzerklicks für Analytics
- **Postleitzahlen-Integration**: PLZ-basierte Lokalisierung der Angebote

### 2. API Endpoints (`server/routes.ts`)
- `GET /api/tracking/comparison-url`: Generiert Check24 Tracking-URLs
- `POST /api/tracking/click`: Verfolgt Klick-Events für Analytics

### 3. Frontend Tracking Utilities (`client/src/lib/tracking.ts`)
- **URL-Generierung**: Client-seitige Funktionen zur Tracking-URL-Erstellung
- **Click-Tracking**: Automatische Erfassung von Nutzerinteraktionen
- **Helper-Funktionen**: Vereinfachte APIs für verschiedene Vertragskategorien

### 4. AI Integration (`server/services/ai.ts`)
- **Automatische URL-Injection**: Check24 Links werden automatisch in Optimierungsvorschläge eingefügt
- **Kontext-abhängige Weiterleitung**: URLs basieren auf Vertragstyp und Anbieter

## Konfiguration

### Umgebungsvariable
```bash
CHECK24_PARTNER_ID=YOUR_CHECK24_PARTNER_ID_HIER_EINFUEGEN
```

**Wichtig**: Ersetzen Sie `YOUR_CHECK24_PARTNER_ID_HIER_EINFUEGEN` durch Ihre tatsächliche Check24 Partner-ID.

## Verwendung im Frontend

### Direkte Vergleiche öffnen
```typescript
import { trackingHelpers } from '@/lib/tracking';

// Energie-Vergleich
await trackingHelpers.openEnergyComparison('strom', '10115');

// Telekom-Vergleich
await trackingHelpers.openTelecomComparison('internet', '10115');

// Versicherung-Vergleich
await trackingHelpers.openInsuranceComparison('kfz', '10115');
```

### Optimierungsvorschläge
Alle AI-generierten Optimierungsvorschläge enthalten automatisch Check24 Tracking-URLs im `comparisonUrl` Feld.

## Integration Points

### 1. Contract Analysis
- **Automatisch**: Bei der Vertragsanalyse werden Check24 URLs in Optimierungsvorschläge eingefügt
- **Kontext-sensitiv**: URLs basieren auf Vertragstyp (Energie, Telekom, Versicherung)

### 2. Dashboard
- **Optimierung-Buttons**: Direkte Weiterleitung zu passenden Check24 Vergleichen
- **Vertragsmanagement**: Tracking bei Optimierungsaktionen

### 3. Landing Page
- **Newsletter-Integration**: Check24 Disclaimer im Footer implementiert
- **Direktvergleiche**: Tracking-URLs für Schnellvergleiche

## Analytics & Tracking

### Click Events
Alle Klicks auf Check24 Links werden nachverfolgt:
- **User ID**: Eindeutige Nutzeridentifikation
- **URL**: Vollständige Tracking-URL
- **Kategorie**: Vertragstyp (energy, telecom, insurance)
- **Unterkategorie**: Spezifischer Vertragstyp (strom, internet, kfz, etc.)

### Conversion Tracking
Das System protokolliert:
- Anzahl generierter Tracking-URLs
- Klickrate pro Vertragskategorie
- User Journey von Analyse bis Check24-Weiterleitung

## Rechtliche Hinweise

### Footer Disclosure
Im Footer wurde der required Check24 Partnerprogramm-Hinweis implementiert:

> "Wir nehmen am CHECK24.net Partnerprogramm teil. Auf unseren Seiten werden iFrame-Buchungsmasken und andere Werbemittel eingebunden, an denen wir über Transaktionen, zum Beispiel durch Leads und Sales, eine Werbekostenerstattung erhalten können."

## URL-Struktur

### Energie
- **Strom**: `https://www.check24.de/strom/?pid=[PARTNER_ID]&plz=[PLZ]`
- **Gas**: `https://www.check24.de/gas/?pid=[PARTNER_ID]&plz=[PLZ]`
- **Ökostrom**: `https://www.check24.de/strom/?oekostrom=1&pid=[PARTNER_ID]&plz=[PLZ]`

### Telekommunikation
- **Internet/DSL**: `https://www.check24.de/dsl/?pid=[PARTNER_ID]&plz=[PLZ]`
- **Mobilfunk**: `https://www.check24.de/handytarife/?pid=[PARTNER_ID]&plz=[PLZ]`

### Versicherungen
- **KFZ**: `https://www.check24.de/kfz-versicherung/?pid=[PARTNER_ID]&plz=[PLZ]`
- **Haftpflicht**: `https://www.check24.de/privathaftpflicht/?pid=[PARTNER_ID]&plz=[PLZ]`
- **Hausrat**: `https://www.check24.de/hausratversicherung/?pid=[PARTNER_ID]&plz=[PLZ]`

## Nächste Schritte

1. **Partner-ID konfigurieren**: Check24 Partner-ID in Umgebungsvariable eintragen
2. **Testing**: Tracking-URLs auf korrekte Partner-ID-Übertragung prüfen
3. **Analytics-Dashboard**: Erweiterte Tracking-Metriken implementieren
4. **A/B Testing**: Optimierung der Conversion-Rate durch verschiedene CTA-Varianten