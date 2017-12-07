# SVG + Javascript

# Javascript Basics

### Javascript Resourcen

- Mozilla
	- [Javascript Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics)
	- [Javascript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- W3schools
	- [Javascript Tutorial](https://www.w3schools.com/js/)
	- [Javascript Reference](https://www.w3schools.com/jsref/)
- [Javascript.info](https://javascript.info/)

### Browser Developer Console

Jeder moderne Browser hat mittlerweile eine Developer Console / Developer Tools eingebaut.
(Jede ist ein bischen anders, daher nutzen wir Chrome).

#### Shortcut

- Mac-Shortcut für [Chrome](https://developer.chrome.com/devtools) / [Firefox](https://developer.mozilla.org/en-US/docs/Tools) / [Safari](https://developer.apple.com/safari/tools/) : `CMD` + `ALT`+ `i`
- Win-Shortcut für [Chrome](https://developer.chrome.com/devtools) / [Firefox](https://developer.mozilla.org/en-US/docs/Tools) / [Edge](https://docs.microsoft.com/en-us/microsoft-edge/f12-devtools-guide): `Ctrl` + `Shift` + `i`

In Safari muss man das [Develop Menu aktivieren](https://developer.apple.com/library/content/documentation/NetworkingInternetWeb/Conceptual/Web_Inspector_Tutorial/EnableWebInspector/EnableWebInspector.html).

### Warum die Console?

- javascript snippets ausprobieren
- javascript objecte inspizieren
- debugging: `console.log(variable);`

### Javascript Basics

- Ausdrücke
	- Mathematische Ausdrücke: `1 + 1` (ergibt eine Zahl)
	- Boolsche Ausdrücke `"pink" === "pink"` (ergibt einen Wahrheitswert:`true` oder `false`)
- Zuweisung und Variablen

		var a = 1 + 1;

	das Ergebnis des Ausdrucks `1 + 1` wird in der variable `a` gespeichert

- Funktions- Deklaration

		function hallowelt(name) {
			alert("Hallo " + name);
		}

- Funktions-Aufruf

		hallowelt('Mainz');


- Kommentare

		// Kommentar bis zum Ende der Zeile

		/*
		Einen ganzen
		Block auskommentieren
		*/

# DOM

- DOM = Document Object Model
- Baum-Modell einer Webseite:

  ![Processing.js NodeTree](https://i.stack.imgur.com/WVdlD.png)
- Siehe auch: [HTML Tree Generator](https://chrome.google.com/webstore/detail/html-tree-generator/dlbbmhhaadfnbbdnjalilhdakfmiffeg)
- Der Browser verwandelt den HTML-Text in eine hierarchische Objekt-Struktur:
	- `Tag` = Text im HTML-Dokument
	- `Element` = Objekt im DOM-Baum

## Mit Javascript Elemente in der DOM finden

Wir können die _Methoden_ (Methode = Funktion eines Objekts) des [document Objekt](https://www.w3schools.com/jsref/dom_obj_document.asp) nutzen um Elemente in der DOM zu finden. Aber auch jedes der [DOM-Elemente](https://www.w3schools.com/jsref/dom_obj_all.asp) hat diese Methoden.


### Mit CSS-Selektoren suchen

Am einfachsten + mächtigsten ist die Suche mit CSS-Query-Selektoren [`querySelector`](https://www.w3schools.com/jsref/met_document_queryselector.asp) und [`querySelectorAll`](https://www.w3schools.com/jsref/met_document_queryselector_all.asp):

- `document.querySelector('h2')` gibt den ersten Treffer zurück
- `document.querySelectorAll('h2')` gibt eine Array mit allen Treffern zurück

### Nach Ids, Tags und Klassen suchen

Alternativ kann man auch spezifische Methoden verwenden um Element(e) mit einer bestimmten id, tag-namen oder Klasse zu suchen [`getElementById`](https://www.w3schools.com/jsref/met_document_getelementbyid.asp), [`getElementsByTagName`](https://www.w3schools.com/jsref/met_document_getelementsbytagname.asp) und [`getElementsByClassName`](https://www.w3schools.com/jsref/met_document_getelementsbyclassname.asp):


- `document.getElementById('inhalt')` gibt das Element mit der id `inhalt` zurück
- `document.getElementsByTagName('svg')` gibt einen Array mit allen `svg`-Elementen zurück
- `document.getElementsByClassName('wichtig')` gibt einen Array mit allen Elementen mit class `wichtig` zurück


### Durch den DOM-Baum hangeln

Wenn `e` ein Element aus dem DOM-Baum ist `e = document.querySelector('div');` kann man sich mit den Attributen [`parentElement`](https://www.w3schools.com/jsref/prop_node_parentelement.asp) und [`childNodes`](https://www.w3schools.com/jsref/prop_node_childNodes.asp)

-  gibt `e.childNodes` alle Kinder eines Elements  zurück
-  gibt `e.parentElement` den Patent-Knoten zurück

### Element löschen

DOM-Elemente kann man nach Auswah mit [`remove`](https://www.w3schools.com/jsref/met_select_remove.asp) direkt löschen:

- `document.querySelector('#logo').remove()` sucht das Element mit der id `logo` und entfernt es

Alternativ kann man ein Kind auch mit der [`removeChild`](https://www.w3schools.com/jsref/met_node_removechild.asp)-Methode des Eltern-Knotens löschen.

### HTML einfügen

Mit dem `innerHTML` Attribut kann man HTML direkt in ein Element einfügen.	Der Browser übersetzt das HTML in DOM-Elemente (man spricht auch von parsen) und fügt sie in den DOM-Baum ein.

	// HTML ersetzen
	var e = document.querySelector('h1');
	e.innerHTML = 'Neue <b>tolle<b> headline'

	// HTML hinten anhängen
	var e = document.querySelector('h1');
	e.innerHTML = e.innerHTML + '!!!!!';

	// HTML vorne anhängen
	var e = document.querySelector('h1');
	e.innerHTML = 'Unglaublich: ' + e.innerHTML;

Mehr Kontrolle darüber wo das HTML eingefügt wird kann man mit [`insertAdjacentHTML`](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML) erreichen.


### SVG einfügen

Das `innerHTML` Attribut funktioniert in aktuellen Browsern auch mit SVG (Chrome 6+, Safari 5+, Firefox 4+ and IE9+):

	// SVG anhängen
	var svg = document.querySelector('svg')
	svg.innerHTML = svg.innerHTML + '<use href="#z" x="200" y="800"/>';

### HTML-Elemente in Javascript basteln und einfügen

Wir können DOM-Elemente auch programatisch mit Javascript erzeugen. Das ist etwas umständlicher, aber es lohnt sich, wenn man viele Elemente dynamisch erzeugt.

	// Link Element erzeugen
	var e = document.createElement('a');

	// Wir können Id und Klasse mit dem Attributen id und className setzen
	e.id = 'link-1'
 	e.className = 'external-link';

 	// Andere Attribute setzen
 	e.setAttribute('href', 'http://google.de');

 	// Text-Inhalt des Links setzen
 	e.textContent = 'google';

 	// Element im Abschnitt mit der ID `links` einfügen
 	var links = document.querySelector('.links');
 	links.appendChild(e);

### SVG-Element in Javascript basteln und einfügen

SVG basiert auf XML (Extensible Markup-Language).
Wenn das SVG in eine HTML-Seite eingebettet ist, wird es in die DOM eingebaut, und wir können es mit Javascript genauso manipulieren andere Elemente der DOM.

- Style-Attribut verändern (`style= "fill: red; stroke: black;"`)
- Klassen hinzufügen / entfernen ( `class="hilight"`)
- Andere Attribute ändern (`x="10"`, `y="10"`, ...)
- SVG-Elemente löschen und einfügen
- Event-Handler an SVG-Elemente knüpfen (`onmousedown`, `onmouseover`, `onkeypress`, `onkeydown` ...)

__Wenn man SVG-Elemente in eine HTML-Seite einfügen will, muss man den XML-NameSpace angeben: `http://www.w3.org/2000/svg`__

	// Use-Element erzeugen
	var e = document.createElementNS("use", "http://www.w3.org/2000/svg");

	//  Attribute setzen
	e.setAttribute('href', '#a');
	e.setAttribute('x', 1);
	e.setAttribute('y', 1);

	// Use-Element an das SVG-Element anhängen
	var editor = document.querySelector('#editor')
	editor.appendChild(e);

### XML / SVG parsen und einfügen

Statt SVG-Elemente zu erzeugen, können wir selbst SVG-Markup parsen (ähnlich wie bei innerHTML / insertAdjacentHTML). Das ist praktisch, wenn man mit den SVG-Elementen jonglieren will (z.B. SVG-Snippets an beliebigen Stellen dynamisch einfügen und entfernen).
In der Praxis braucht man das allerdings sehr selten.

	// SVG als Zeichenkette
	var svgString = '<svg xmlns="http://www.w3.org/2000/svg">' +
	'<use href="#a" x="1" y="1" />' + '</svg>';

	// SVG in DOM-Element umwandeln
	var parser = new DOMParser();
	var e = parser.parseFromString(svgString, "image/svg+xml").documentElement;

	// Neues Element irgendwo an das SVG-Element anhängen
	var editor = document.querySelector('#editor');
	var randomChild = editor.children[Math.floor(Math.random() * editor.children.length)];
	editor.insertBefore(e, randomChild);

# Events

Wichtigeste Eventhandler für Interaktion:

- `onclick`
- `onkeydown`, `onkeypress	`
- `onmousedown`, `onmouseover`, `onmouseout`


Mehr Info:

- [Alle Events](https://www.w3schools.com/jsref/dom_obj_event.asp)
- [Javascript Events Tutorial](https://www.w3schools.com/js/js_events.asp)
- [Touch Events](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events)

## Events zuweisen

Jedes DOM-Element hat ein Attribut für jeden Eventhandler.
Wenn man so einem Attribut eine Funktion zuweist, wird die Funktion durch das Event getriggert.

*`mousedown`-event an das erste `use`-Element des Abschnitts hängen:*

	function mouseFn(evt) {
		console.log('mouseFn', this, evt);
	}

	var letter = document.querySelector('#buchstaben-tafel use');
	letter.onmousedown = mouseFn;

## Events mehreren Elementen zuweisem

In Javascript gibt es verschiedene Möglichkeiten eine Funktion mehreren Elementen zuzuweisen. Am einfachsten ist die von aktuellen Browsern unterstützte ES 6-Syntax.

*`mousedown`-event an alle `use`-Elemente des Abschnitts hängen:*

	function mouseFn(evt) {
		console.log('mouseFn', this, evt);
	}

	var letters = document.querySelectorAll('#buchstaben-tafel use');
	letters.forEach( letter => letter.onmousedown = mouseFn );

## Mehrere Events zuweisen

Man kann immer nur eine Funktion an einen Eventhandler hängen.
Wenn z.B. mehrere Funktionen an ein Element gehängt werden sollen, kann man das mit [`addEventListener`](https://www.w3schools.com/jsref/met_element_addeventlistener.asp) realisieren.

## Event Bubbling

MouseEvents werden durch die DOM nach oben gereicht ([Event Bubbling](https://javascript.info/bubbling-and-capturing)).
