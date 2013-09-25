---
title: HaxeSpel
layout: page
---
<h2>Skapa projekt</h2>

<p>I ett terminalfönster/kommandotolk skriv:</p>

<pre><code>openfl create project HaxeSpel
cd HaxeSpel
openfl test flash
</code></pre>

<p>Kör igång ett tomt vitt &quot;spel&quot; i din webbläsare.</p>

<h2>Ställ in din utvecklingsmiljö</h2>

<h3>IntelliJ</h3>

<p>Öppna IntelliJ. Välj File ➤ Import Project... Leta upp HaxeSpel och välj OK. &quot;Create project from existing sources&quot; är valt, klicka på Next, Next. Om HaxeSpel/Export/flash/haxe är med i listan klicka bort den, det är bara HaxeSpel/Source som ska va iklickad. Klicka på Next, Next, Next. Välj Haxe som SDK. Klicka på Next, Finish. Nu ska du ha ett projekt öppet.</p>

<p>I listan till vänster kan vi leta upp källkoden till vårt &quot;spel&quot;, klicka på ➤HaxeSpel, ➤Source, Main.hx. Som du ser är den ganska tom.</p>

<p>Nu behöver vi säga åt IntelliJ att det är ett OpenFL projekt (den vet bara att det är ett Haxe projekt, inte att det är OpenFL vi vill använda). File ➤ Project Structure... I dialogen välj Modules, HaxeSpel, Haxe. Här är nog &quot;Haxe compiler&quot; ifyllt. Välj &quot;OpenFL&quot; och klicka på OK.</p>

<p>Snart klara, vi behöver bara säga åt IntelliJ hur den ska köra vårt spel. Run ➤ Edit Configurations... Längst uppe till vänster i dialogen finns en plus knapp, klicka på den och välj Haxe Application. Ändra namnet från &quot;Unnamed&quot; till &quot;HaxeSpel&quot;. Klicka på knappen till höger om Module: och välj HaxeSpel. Klicka på OK.</p>

<p>Nu kan du köra &quot;spelet&quot; genom att klicka på den gröna spela knappen, eller välja Run ➤ Run &#39;HaxeSpel&#39;. Den gör samma sak som <code>openfl test flash</code> som vi använde tidigare, men det är lite smidigare.</p>
<h2>Rita spelaren</h2>

<p>Vi har ju nu en tom <code>Main.hx</code>. <strong>TODO</strong> Beskriv hur man skapar en sprite. Beskriv hur de olika ritmetoderna funkar. Koordinatsystem är klurigt, behöver vi nån debughjälp så man fattar var olika positioner finns? Hur förklarar man att varje sprite har ett eget koordinatsystem?</p>

<h3>Koden</h3>

<pre><code>package;

import flash.display.Sprite;

class Main extends Sprite {
    var spelare:Sprite;

    public function new() {
        super();

        // skapa spelaren
        spelare = new Sprite();
        addChild(spelare);
        ritaSpelare();
        // starta spelaren i mitten av spelet
        spelare.x = stage.stageWidth / 2;
        spelare.y = stage.stageHeight / 2;
    }

    function ritaSpelare() {
        var g = spelare.graphics;
        // rita kroppen
        g.beginFill(0xFF0000); // rött
        g.drawCircle(0, 0, 20);

        // rita ögon
        g.beginFill(0x000000); // svart
        g.drawEllipse(-7, -23, 14, 10); // bakgrund
        g.beginFill(0xFFFFFF); // vitt
        g.drawCircle(-4, -19, 1.5);
        g.drawCircle(4, -19, 1.5);

        // rita prickar
        g.beginFill(0x000000); // svart
        g.drawCircle(0, -9, 2);
        g.drawCircle(-8, -4, 2);
        g.drawCircle(8, -4, 2);
        g.drawCircle(-4, 3, 2);
        g.drawCircle(4, 3, 2);
        g.drawCircle(-7, 10, 2);
        g.drawCircle(7, 10, 2);
    }
}
</code></pre>
<h2>Rör på spelaren</h2>

<h3>Gå upp, ner, vänster, höger</h3>

<p><strong>TODO</strong> Berätta hur man lyssnar på keyboard events. Vad är enter frame? Flytta upp, ner, vänster, höger</p>

{% highlight diff %}
diff --git a/Source/Main.hx b/Source/Main.hx
index 8769f45..a0f7d1c 100644
--- a/Source/Main.hx
+++ b/Source/Main.hx
@@ -1,9 +1,16 @@
 package;

+import flash.events.Event;
+import flash.ui.Keyboard;
+import flash.events.KeyboardEvent;
 import flash.display.Sprite;

 class Main extends Sprite {
     var spelare:Sprite;
+    var upp:Bool;
+    var ner:Bool;
+    var vanster:Bool;
+    var hoger:Bool;

     public function new() {
         super();
@@ -15,6 +22,11 @@ class Main extends Sprite {
         // starta spelaren i mitten av spelet
         spelare.x = stage.stageWidth / 2;
         spelare.y = stage.stageHeight / 2;
+
+        // prenumerera på events
+        stage.addEventListener(KeyboardEvent.KEY_DOWN, onKeyDown);
+        stage.addEventListener(KeyboardEvent.KEY_UP, onKeyUp);
+        stage.addEventListener(Event.ENTER_FRAME, onEnterFrame);
     }

     function ritaSpelare() {
@@ -40,4 +52,37 @@ class Main extends Sprite {
         g.drawCircle(-7, 10, 2);
         g.drawCircle(7, 10, 2);
     }
+
+    function onKeyDown(event:KeyboardEvent) {
+        switch (event.keyCode) {
+            case Keyboard.UP: upp = true;
+            case Keyboard.DOWN: ner = true;
+            case Keyboard.LEFT: vanster = true;
+            case Keyboard.RIGHT: hoger = true;
+        }
+    }
+
+    function onKeyUp(event:KeyboardEvent) {
+        switch (event.keyCode) {
+            case Keyboard.UP: upp = false;
+            case Keyboard.DOWN: ner = false;
+            case Keyboard.LEFT: vanster = false;
+            case Keyboard.RIGHT: hoger = false;
+        }
+    }
+
+    function onEnterFrame(event:Event) {
+        if (upp) {
+            spelare.y -= 3;
+        }
+        if (ner) {
+            spelare.y += 3;
+        }
+        if (vanster) {
+            spelare.x -= 3;
+        }
+        if (hoger) {
+            spelare.x += 3;
+        }
+    }
 }
{% endhighlight %}

<h3>Rotera och gå fram/bakåt</h3>

<p><strong>TODO</strong> matrix grejen är lite svår, skippa att förklara?</p>

{% highlight diff %}
diff --git a/Source/Main.hx b/Source/Main.hx
index a0f7d1c..a064f78 100644
--- a/Source/Main.hx
+++ b/Source/Main.hx
@@ -1,5 +1,6 @@
 package;

+import flash.geom.Point;
 import flash.events.Event;
 import flash.ui.Keyboard;
 import flash.events.KeyboardEvent;
@@ -73,16 +74,22 @@ class Main extends Sprite {

     function onEnterFrame(event:Event) {
         if (upp) {
-            spelare.y -= 3;
+            flyttaSprite(spelare, 2);
         }
         if (ner) {
-            spelare.y += 3;
+            flyttaSprite(spelare, -2);
         }
         if (vanster) {
-            spelare.x -= 3;
+            spelare.rotation -= 3;
         }
         if (hoger) {
-            spelare.x += 3;
+            spelare.rotation += 3;
         }
     }
+
+    function flyttaSprite(sprite:Sprite, fart:Float) {
+        var p = sprite.transform.matrix.transformPoint(new Point(0, -fart));
+        sprite.x = p.x;
+        sprite.y = p.y;
+    }
 }
{% endhighlight %}

