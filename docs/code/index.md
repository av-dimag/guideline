# Wie schreiben wir Code?

Die meisten Spielregeln betreffend Schreibweisen im Code sind bereits im `.editorconfig` und im `.eslintrc.js` im jeweiligen Repository definiert. Dennoch tragen wir hier die paar Regeln zusammen, um einen einheitlich aussehenden Code zu erhalten.

> :warning: &nbsp; Das Dokument ist im Aufbau und daher noch nicht vollständig!

## Format

### Einrücken

Generell arbeiten wir mit Leerschlag anstelle von Tabs. Zwei Leerschläge bei allen Dokumenten mit Ausnahme von Typescript; hier helfen 4 Leerschläge zur besseren Lesbarkeit.

## Kommentare

Jede Funktion muss mit einem Kommentar im Stil von [TSDoc](https://tsdoc.org/) versehen werden. Später können wir aus diesen Kommentaren die Dokumentation generieren. Es hilft aber auch den Code zu verstehen und ist hilfreich beim Wiederverwenden einer Funktion.

```typescript
/**
 * Adds two numbers together.  
 * @example { add two positive numbers }
 * add(1,1) // prints "2"
 * 
 * @example { add two negative numbers }
 * add(-1,-1) // prints "-2"
 */ 
export const add = (x: number, y: number): number => x + y;
```

<!-- ## File-Struktur -->