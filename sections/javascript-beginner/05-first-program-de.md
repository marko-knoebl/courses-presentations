# Unser erstes JavaScript-Programm

## Unser erstes JavaScript-Programm

Wir schreiben ein JavaScript-Programm für die Verwendung im Browser.

Unser Programm soll den Benutzer nach seinem Namen fragen und ihn dann begrüßen.

## Eingabe und Ausgabe

Ausgabe in Popup-Fenster:

```js
alert('hello!');
```

Alert ist eine sogenannte _Funktion_.

## Eingabe und Ausgabe

Eingabe: Mit Hilfe von `prompt`:

```js
let name = prompt('What is your name?');
```

## Eingabe und Ausgabe

Ausgabe der Begrüßung

```js
alert(`Nice to meet you, ${name}!`);
```

## Typen umwandeln

Die Funktion `prompt` liefert immer Text (einen String) zurück.

Um den String in eine Zahl zu verwandeln:

```js
let birthYearString = prompt('When were you born?');
let birthYear = Number(birthYearString);
```

Analog für andere Datentypen: `String(...)`, `Boolean(...)`

Alternativen: `.toString()`, `parseInt()`, `parseFloat()`

## Übung: Alter anhand Geburtsjahr

Der Benutzer soll nach seinem Geburtsjahr gefragt werden. Dann soll angegeben werden, wie alt diese Person im Jahr 2019 wird.

## Kommentare

Kommentare dienen Entwicklern, um ihren Code zu beschreiben und zu erklären. Sie werden bei der Ausführung von JavaScript ignoriert.

Es gibt zwei Möglichkeiten, Kommentare zu erstellen:

```js
// dies ist ein Kommentar über 1 Zeile

/*
dies ist
ein mehrzeiliger
Kommentar
*/
```

## Variablen

Wie wir schon gesehen haben: Variablen werden üblicherweise mit `let` deklariert

Alternativen:

- Deklaration mit `const` (nicht mehr neu zuweisbar)
- Deklaration mit `var` ("veraltete" Version von `let`)

Mit `let` oder `const` deklarierte Variablen sind nur innerhalb des enstprechenden Codeblocks (innerhalb der umgebenden geschweiften Klammern) gültig. (Mehr dazu später)

## Das Semikolon in JavaScript

In JavaScript sind Semikolons in den meisten Fällen optional; sie werden bei der Ausführung automatisch nach bestimmten Regeln eingesetzt. (_automatic semicolon insertion_)

## Das Semikolon in JavaScript

Das automatische Hinzufügen von Semikolons kann zu Problemen führen:

<!-- prettier-ignore -->
```js
function foo() {
  return
    "hello";
}
```

wird interpretiert als:

<!-- prettier-ignore -->
```js
function foo() {
  return;
  "hello";
}
```
