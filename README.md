# Informacje
Najnowsza wersja: `clickerCore-0.7.js`<br>
Funkcje:<br>
1. Zarządzanie monetami (zapis i odczyt)
2. Ulepszenia
3. Osiągnięcia **(W.I.P)**

# Tworzenie gry Clicker

Wykonuj kroki po kolei.

## Implementacja rdzenia w twojej grze.
W pliku HTML dodaj rdzeń. Rdzeń musi być załadowany przed wszystkimi skryptami odnoszącymi się do niego.<br><br>
Kod
`latest.js` oznacza automatyczne pobieranie najnowszej wersji rdzenia.<br>
Alternatywa: zamiast `latest.js` -> *wersjaRdzenia*.js np. `clickerCore-0.7.js`
```html
<script src="https://tw-software.eu/bencclicker/core/latest.js"></script>
<!-- Reszta skryptów np. <script src="js/game.js"></script> -->
```

## Stwórz przycisk na, który gracz będzie klikał.
Następnie stwórz plik JavaScript i podłącz go do strony.<br>
```js
var przycisk = getElementId("idPrzycisku"); //HTML <button id="idPrzycisku">Przycisk</button>
przycisk.addEventListener("click", function(){
    core.coins.add(1);
});
// od teraz po kliknięciu na przycisk ilość monet będzie się zwiększać. Gracz jeszcze nie widzi zmiany.
```

## Wyświetlanie zmiany monet
```js
var licznik = getElementId("idLicznika"); //HTML <span id="idLicznika"></span>
document.addEventListener('amountCoinsChanged', function(){
    licznik.innerText = core.coins.get();
});
// od teraz co zmianę ilości monet tekst `licznik`a będzie się zmieniał na wartość monet
```

## Zapisywanie stanu monet
```js
// Kiedy strona zotanie wczytana
window.addEventListener('load', function(){
    // Wczytaj poprzedni stan monet
    core.coins.load();
});

// Kiedy strona zostanie zamknięta
window.addEventListener('beforeunload', function(){
    // Zapisz aktualny stan monet
    core.coins.save();
});
```

# Ulepszenia

## Jak tworzyć?
**Zalecany przykład:**
```js
var ulepszenie = {
    key: "klucz", // unikatowy
    displayName: "Wyświetlana nazwa",
    description: "Opis",
    upgrades: [
        {cost: 100, clickBonus: 1, cps: 0}, // poziom 1
        {cost: 150, clickBonus: 2, cps: 0}, // poziom 2
        {cost: 225, clickBonus: 3, cps: 0} // poziom 3
    ]
};
core.upgrades.register(ulepszenie);
// i tak dla ulepsenie2
// ulepszenie3
// ulepszenie4
// po wszystkich zarejestrowaniach

var divUlepszenia = getElementId("divUlepszenia");

core.upgrades.upgradesItems.forEach(upgrade => {
    // tutaj wykona się kod dla kazdego zarejestrowanego ulepszenia
    // dla przykładu teraz pokazemy je.
    divUlepszenia.innerHTML += "<div id=\" + upgrade.key + \"><h4>" + upgrade.displayName + "</h4><p>" + upgrade.description + "</p><button>" + core.upgrades.getNextLevel().cost + "<button></div>";
    // powyzej dodajemy do diva z ulepszeniami nowego diva który pokazuje ulepszenie.
    // Jego wyświetlaną nazwe jako nagłówek, opis i koszt następnego poziomu.
});


```
