---
title: Arduino
layout: page
---
## TODO

* Skriv ut [referens sidan](http://arduino.cc/en/Reference/HomePage). Markera koncept man använt/kan.
* Borde man ha det koden som eleven ska skriva utskrivet på papper?

## Anti-patterns

### Blink

Blink (`File->Examples->1.Basics->Blink`) är frestande eftersom man får mycket att hända utan att skriva nåt (de första gångerna använde jag Blink). Ett problem är att den använder sig av pin `13` som automatiskt blinkar när man programmerar Arduinon vilket gör att det är lätt att få fel uppfattning om ens program. Det är också många koncept på en gång som gör det svårt att förstå vad som händer. Dessutom tror jag att man missar lite av känslan att själv få lampan att blinka.

Jag rekommenderar BareMinimum (`File->Examples->1.Basics->BareMinimum`) minus kommentarer som start.

## Blinka lilla lampa där

Man kan göra mycket med en blinkande lampa...

### Koppla

Du behöver:

* 1 Arduino
* 2 kablar
* 1 lysdiod
* 1 motstånd (220 ohm)
* 1 experimentbräda

`GND--motstånd--lysdiodens katodben (det korta)--lysdiod--lysdiodens anodben (det långa)--5V`

Jag föredrar att koppla ihop en egen och låta studenten kopiera.

Motståndet kan vara på andra sidan av motståndet också, men genom att ha det på grundens sida kan man använda ett motstånd när man kopplar in två lysdioder.

Genom att koppla direkt till `5V` kan man testa att man kopplat allt rätt (t.ex. vänt dioden åt rätt håll) och slipper felsöka när man börjar programmera.

När allt fungerar kan koppla om så att dioden är kopplad till en av de digitala pinnarna. Jag skulle undvika `13` (eftersom den används till annat, se Blink ovan) och har haft problem med `0` och `1` (de används för programmeringen av Arduinon). Fortsättningen antar pin `2`.

`GND--motstånd--lysdiodens katodben (det korta)--lysdiod--lysdiodens anodben (det långa)--2`

### Orientering

Visa Arduino IDE på datorn. Öppna BareMinimum (`File->Examples->1.Basics->BareMinimum`) ta bort kommentarerna och visa `Upload` knappen och förklara hur det hänger ihop.

    void setup() {
    
    }
    
    void loop() {
    
    }

### Tänd lampan -- `setup()`, `pinMode()`, `digitalWrite()`, `HIGH`

Tänd lampan med ett program. Det här får nog mentoren skriva in för hand.

    void setup() {
      pinMode(2, OUTPUT);
      digitalWrite(2, HIGH);
    
    }
    
    void loop() {
    
    }

Testa och förklara.

### Släck lampan -- `LOW`

Be eleven ändra `HIGH` till `LOW`.

    void setup() {
      pinMode(2, OUTPUT);
      digitalWrite(2, LOW);
    
    }
    
    void loop() {
    
    }

### Tänd lampan, vänta, släck lampan -- `delay()`

`delay()` är klurigt och används ganska mycket framöver för att blinka så det är värt att man förstår det i dess enklaste form. Millisekunder är svårt.

    void setup() {
      pinMode(2, OUTPUT);
      digitalWrite(2, HIGH);
      delay(1000);
      digitalWrite(2, LOW);
    
    }
    
    void loop() {
    
    }

Viktigt att man förstår vad som händer, annars blir det svårt att förstå när man loopar.

### Blinka -- `loop()`

Flytta blinkningen till `loop()`.

    void setup() {
      pinMode(2, OUTPUT);
    
    }
    
    void loop() {
      digitalWrite(2, HIGH);
      delay(1000);
      digitalWrite(2, LOW);
      delay(1000);
    
    }

Kolla att eleven förstår vad som händer genom att få den att blinka snabbare, långsammare, vara tänd länge, släckt kort tid etc.

### Två lampor koppling

Du behöver:

* 1 kabel
* 1 lysdiod (gärna annan färg än den första)

`GND--motstånd--lysdiodens katodben (det korta)--lysdiod--lysdiodens anodben (det långa)--2` <br>
`.............\-lysdiodens katodben (det korta)--lysdiod--lysdiodens anodben (det långa)--3`

### Två lampor (unisont vs ambulans)

Låt eleven duplicera vad som görs för den första dioden också för andra dioden. Det är klurigt att veta var man ska lägga raderna och vad man ska ändra för att båda dioderna ska blinka så det kan behövas mycket hjälp.

    void setup() {
      pinMode(2, OUTPUT);
      pinMode(3, OUTPUT);
    
    }
    
    void loop() {
      digitalWrite(2, HIGH);
      digitalWrite(3, HIGH);
      delay(1000);
      digitalWrite(2, LOW);
      digitalWrite(3, LOW);
      delay(1000);
    
    }

När de blinkar unisont är uppdraget att få de att blinka som en ambulans.

### Flytta lampan -- `int`

Det sista uppdraget är att flytta någon av dioderna till en annan pinne. Det är lite jobbigt att ändra på så många ställen.

När eleven väl flyttat en gång kan man be eleven att flytta den andra dioden. För att inte få en högaffel som tack kan man förklara att man kan använda en variabel. Mentoren får nog skriva själva variabeln och eleven kan kanske göra resten.

    int gron = 2;
    int rod = 3;

    void setup() {
      pinMode(gron, OUTPUT);
      pinMode(rod, OUTPUT);
    
    }
    
    void loop() {
      digitalWrite(gron, HIGH);
      digitalWrite(rod, HIGH);
      delay(1000);
      digitalWrite(gron, LOW);
      digitalWrite(rod, LOW);
      delay(1000);
    
    }

Största anledningen att göra det här är att om man väntar tills när det är mer naturligt att använda en variabel blir det ofta samtidigt som när man inför något annat nytt.

### Genomgång

Gå igenom vad man lärt sig.

## Knapp lampa

### Läsa knapp -- `digitalRead()`

## Reaktionsspel
