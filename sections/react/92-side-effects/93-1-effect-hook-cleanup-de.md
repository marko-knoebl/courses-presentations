# Effect Hook: Cleanup

## Effect Hook: Cleanup

manche Side Effects müssen später "aufgeräumt" werden:

- Abbrechen von API-Anfragen, wenn sie nicht mehr benötigt werden (z.B. wenn sich ein Suchbegriff geändert hat)
- Stoppen von Timern

## Cleanup-Funktionen

Eine Effect-Funktion kann eine "Cleanup-Funktion" zurückgeben

Diese Funktion wird ausgeführt, bevor der Effect zum nächsten Mal läuft oder bevor die Komponente entfernt wird

## Cleanup-Funktionen

Beispiel: Struktur für eine Suchanfrage mit unmittelbarem Feedback / Laden, wenn der Benutzer tippt:

```js
function App() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);

  useEffect(() => {
    const initiateQuery = async () => {
      // ...
    };
    const cancelPreviousQuery = () => {
      // ...
    };
    initiateQuery();
    return cancelPreviousQuery;
  }, [query]);

  // ...
}
```

## Cleanup-Funktionen

vollständiges Beispiel: Hacker News - Suche

```js
function App() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);
  useEffect(() => {
    let isCancelled = false;
    const initiateQuery = async () => {
      const res = await fetch(
        `https://hn.algolia.com/api/v1/search?query=${query}`
      );
      const data = await res.json();
      if (!isCancelled) {
        setResults(data.hits);
      }
    };
    const cancelPreviousQuery = () => {
      isCancelled = true;
    };
    initiateQuery();
    return cancelPreviousQuery;
  }, [query]);
  return (
    <div className="App">
      <input
        value={query}
        onChange={(event) => {
          setQuery(event.target.value);
        }}
      />
      <ul>
        {results.map((article) => (
          <li key={article.objectId}>{article.title}</li>
        ))}
      </ul>
    </div>
  );
}
```

## Cleanup-Funktionen

Beispiel: Benutzer wird nach 10 Sekunden Inaktivität automatisch ausgeloggt

```jsx
const App = () => {
  const [loggedIn, setLoggedIn] = useState(true);
  const [lastInteraction, setLastInteraction] = useState(
    new Date()
  );
  // restart the logout timer on user interaction
  useEffect(() => {
    const logout = () => setLoggedIn(false);
    const timeoutId = setTimeout(logout, 10000);
    return () => clearTimeout(timeoutId);
  }, [lastInteraction]);
  return (
    <button onClick={() => setLastInteraction(new Date())}>
      {loggedIn
        ? 'click to stay logged in'
        : 'logged out automatically'}
    </button>
  );
};
```

## Asynchrone Effects und Cleanup-Funktionen

Eine Effect-Funktion **darf keine asynchrone Funktion sein**

Hintergrund:

ein eventueller Rückgabewert einer Effect-Funktion wird immer als Cleanup-Funktion interpretiert

asynchrone Funktionen geben immer Promises zurück

## Asynchrone Effects und Cleanup-Funktionen

ungültig:

```js
useEffect(loadSearchResultsAsync, [query]);
```

gültig:

```js
useEffect(() => {
  loadSearchResultsAsync();
}, [query]);
```
