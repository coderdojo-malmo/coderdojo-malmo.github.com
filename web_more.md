---
title: Webb - Mer resurser att upptäcka
layout: page
---

Vi samlar på oss lite fusklappar och annat här. Alla som jobbar med webben
använder fusklappar. Ingen kommer ihåg allt.

Om du har ett bra tips på en sida eller bok som du lärt dig av, mejla dem gärna
till oss. Det är bara roligt.

## De tre stora webb-teknikerna

Det finns massor att upptäcka.

1. [HTML](/web_html.html) är ett exempeldokument som visar många av de s.k. taggarna. Använd <kbd>View/Page Source</kbd>!
1. CSS är det som bestämmer <em>hur</em> innehållet ska visas
1. [JavaScript](/web_js.html) låter en aktivera knappar och formulär och annat rörligt på webbsidorna

## Att prova själv

[Webb med Batman](/web_batman.html) är en uppgift som passar nybörjare. Prova gärna!

[Wayback Machine](/web_wayback.html) visar hur en webbsida såg ut för många år sedan!

[Webbläsartillägg](/web_browser_extensions.html) utökar andras webbsidor genom nya, egna knappar i din webbläsare.

## Tips om CSS

	/* A-taggar på list-element i en UL-lista */
	UL LI A {
		text-decoration: none;
	}

	/* Lite mellanrum efter varje listpunkt */
	UL LI {
		margin-bottom: 25px;
	}

	/* Runda hörn, med beige bakgrund */
	UL LI {
		border-radius: 5px;
		background-color: beige;
	}

	/* Ett undantag för att några element i listan behövde mer plats:
	   lägg in class="mer-plats" på det elementet.
	*/
	UL LI.mer-plats {
		margin-top: 15px;
	}

	/* Alternativt: en enklare selector för denna regel: enklare är bättre */
	.mer-plats {
		margin-top: 15px;
	}

	/* Man kan proppa in bakgrundsfärg eller bild på vad som helst. BODY-taggen är bra: */
	BODY {
		background: url(http://web.coderdojo.se/u/olle/bakgrunden.jpg);
	}

	/* Ge lite utrymme efter en YouTube-film som embeddats in på sidan */
	IFRAME {
		margin-bottom: 10px;
	}

## Mer att läsa

### Nybörjarartiklarna på WebPlatform.org

[Web development for beginners](http://docs.webplatform.org/wiki/beginners) *"This set of articles is for complete beginners to work through in confidence, building up their essential skills at the beginning of the journey to becoming a web designer or developer."*

### Webbprojekt


[Wikipedia om HTML](http://sv.wikipedia.org/wiki/HTML) är en teknisk beskrivning
av vad HTML är. (<em>Krångligt språk!</em>)