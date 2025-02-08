# Platform game tutorial met python

## Introductie @showdialog

Welkom! In deze tutorial leren we je stap voor stap hoe je een leuke platform game maakt. In het spel moet de speler de schat vinden, maar als die in de lava valt heeft de speler verloren. 

![Platform game screenshot](https://raw.githubusercontent.com/tim-vh/makecode-arcade-tutorials/master/docs/static/images/platform-game-screenshot.png)


Versie: 1.0


## Achtergrond kleur instellen

Als eerst gaan we de achtergrondkleuk instellen. Dit kan met de code ``scene.set_background_color(9)``. De kleur negen is lichtblauw.

~hint Welke kleuren zijn er nog meer? 🤷🏽

    0: transparant
    1: wit
    2: rood
    3: roze
    4: oranje
    5: geel
    6: blauwgroen
    7: groen
    8: blauw
    9: licht blauw
    10: paars
    11: licht paars
    12: donker paars
    13: geelbruin
    14: bruin
    15: zwart

hint~


```python
scene.set_background_color(9)
```


## Sprite voor de speler toevoegen

In deze stap gaan we een sprite toevoegen voor de speler. Als de sprite is toegevoegd willen we deze kunnen besturen met de pijltjestoetsen. 

~hint Wat is een sprite? 🤷🏽

Een sprite is een soort plaatje die je aan het spel toevoegd en die we daarna kunnen programmeren. We kunnen de sprite bijvoorbeeld laten bewegen door het spel. Een sprite kunnen we gebruiken voor bijvoorbeeld de speler, een vijand of muntjes die je moet verzamelen.

hint~

Voeg de code ``speler = sprites.create(img(""""""), SpriteKind.player)`` toe. Er verschijn nu een teken icoontje voor deze regel code. Door hier op te klikken kun je gemakkelijjk een sprite tekenen of kiezen uit de gallery.

Om de speler te laten beweren kunnen we de volgende code gebruiken ``controller.move_sprite(speler)``

```python
scene.set_background_color(9)
speler = sprites.create(img("""
    . . . . . . . . . . . . . . . .
    . . . . . f f f f f f . . . . .
    . . . f f e e e e f 2 f . . . .
    . . f f e e e e f 2 2 2 f . . .
    . . f e e e f f e e e e f . . .
    . . f f f f e e 2 2 2 2 e f . .
    . . f e 2 2 2 f f f f e 2 f . .
    . f f f f f f f e e e f f f . .
    . f f e 4 4 e b f 4 4 e e f . .
    . f e e 4 d 4 1 f d d e f . . .
    . . f e e e e e d d d f . . . .
    . . . . f 4 d d e 4 e f . . . .
    . . . . f e d d e 2 2 f . . . .
    . . . f f f e e f 5 5 f f . . .
    . . . f f f f f f f f f f . . .
    . . . . f f . . . f f f . . . .
"""), SpriteKind.player)

controller.move_sprite(speler)
```

## Platforms toevoegen

Om een level met platforms te maken voegen we een tilemap toe aan ons spel.

~hint Wat is een tilemap? 🤷🏽

Een tilemap is een raster van tegels (tiles) die samen een spelwereld of level vormen. Elke tegel is een afbeelding die een de achtergrond, een platform, een muur of een ander onderdeel van het spel is.

hint~

Voeg de code ``tiles.set_current_tilemap(tilemap(""" """))`` om de tilemap voor het spel in te stellen.

Voeg daarna tiles toe aan de tilemap die je hebt toegevoegd. Dit kun je doen door op het 'kaart' icoon te klikken die voor de regels staat die je net hebt toegevoegd.  Deze tiles gebruiken we als platforms waar de speler op kan springen.


Om het spel te laten weten dat we op de platforms moeten kunnen staan geven we in de tilemap editor aan dat het 'walls' of 'muren' zijn.

Om ervoor te zorgen dat we door het hele level kunnen bewegen willen we er voor zorgen dat de camera meebeweegt met de speler. Dit kunnen we doen door de code ``scene.camera_follow_sprite(speler)`` toe te voegen.

```python
scene.set_background_color(9)
speler = sprites.create(img("""
    . . . . . . . . . . . . . . . .
    . . . . . f f f f f f . . . . .
    . . . f f e e e e f 2 f . . . .
    . . f f e e e e f 2 2 2 f . . .
    . . f e e e f f e e e e f . . .
    . . f f f f e e 2 2 2 2 e f . .
    . . f e 2 2 2 f f f f e 2 f . .
    . f f f f f f f e e e f f f . .
    . f f e 4 4 e b f 4 4 e e f . .
    . f e e 4 d 4 1 f d d e f . . .
    . . f e e e e e d d d f . . . .
    . . . . f 4 d d e 4 e f . . . .
    . . . . f e d d e 2 2 f . . . .
    . . . f f f e e f 5 5 f f . . .
    . . . f f f f f f f f f f . . .
    . . . . f f . . . f f f . . . .
"""), SpriteKind.player)

controller.move_sprite(speler)

tiles.set_current_tilemap(tilemap("""level1"""))

scene.camera_follow_sprite(speler)
```

## Zwaartekracht

De speler kan nu door het gemaakte level bewegen. Maar om ervoor te zorgen dat de speler naar beneden valt en op de platforms kan springen willen we zwaartekracht toevoegen.

Om dit te doen voegen we de code ``speler.ay = 350``. Hiermee stellen we de y-acceleration in voor de speler.

~hint Meer uitleg 🤷🏽

Met 'y-acceleration' stellen we in dat het spel de y snelheid steeds probeert te vehogen. De y staat voor de verticale richting (van boven naar beneden). Doordat die snelheid steeds hoger wordt vallen we naar beneden totdat we ergens tegenaan botsen. Bijvoorbeeld een platform.

hint~

```python
scene.set_background_color(9)
speler = sprites.create(img("""
    . . . . . . . . . . . . . . . .
    . . . . . f f f f f f . . . . .
    . . . f f e e e e f 2 f . . . .
    . . f f e e e e f 2 2 2 f . . .
    . . f e e e f f e e e e f . . .
    . . f f f f e e 2 2 2 2 e f . .
    . . f e 2 2 2 f f f f e 2 f . .
    . f f f f f f f e e e f f f . .
    . f f e 4 4 e b f 4 4 e e f . .
    . f e e 4 d 4 1 f d d e f . . .
    . . f e e e e e d d d f . . . .
    . . . . f 4 d d e 4 e f . . . .
    . . . . f e d d e 2 2 f . . . .
    . . . f f f e e f 5 5 f f . . .
    . . . f f f f f f f f f f . . .
    . . . . f f . . . f f f . . . .
"""), SpriteKind.player)

controller.move_sprite(speler)

tiles.set_current_tilemap(tilemap("""level1"""))

scene.camera_follow_sprite(speler)

speler.ay = 350
```

## Springen

Als volgende stap willen we de speler kunnen laten springen. Dat kunnen we doen door de y-snelheid van de speler in te stellen op -150 als er op de a knop wordt gedrukt. Om dit te doen moeten we eerst een functie maken die we 'spring' noemen. Dit doen we op deze manier: ``def spring():``. Daarna kunnen we de speler later springen door hier de code ``speler.vy = -150`` aan toe te voegen.

Nu moeten we de functie uitvoeren wanneer er op de A knop wordt gedrukt. Gebruik hiervoor de volgende code: ``controller.A.on_event(ControllerButtonEvent.PRESSED, spring)``.

Om ervoor te zorgen dat we niet in de lucht kunnen springen willen we de y-snelheid alleen veranderen als deze op dat moment 0 is. Dit kan door de code  ``logic:if speler.vy == 0:`` toe te voegen aan de spring functie.

```python
scene.set_background_color(9)
speler = sprites.create(img("""
    . . . . . . . . . . . . . . . .
    . . . . . f f f f f f . . . . .
    . . . f f e e e e f 2 f . . . .
    . . f f e e e e f 2 2 2 f . . .
    . . f e e e f f e e e e f . . .
    . . f f f f e e 2 2 2 2 e f . .
    . . f e 2 2 2 f f f f e 2 f . .
    . f f f f f f f e e e f f f . .
    . f f e 4 4 e b f 4 4 e e f . .
    . f e e 4 d 4 1 f d d e f . . .
    . . f e e e e e d d d f . . . .
    . . . . f 4 d d e 4 e f . . . .
    . . . . f e d d e 2 2 f . . . .
    . . . f f f e e f 5 5 f f . . .
    . . . f f f f f f f f f f . . .
    . . . . f f . . . f f f . . . .
"""), SpriteKind.player)

controller.move_sprite(speler)

tiles.set_current_tilemap(tilemap("""level1"""))

scene.camera_follow_sprite(speler)

speler.ay = 350

# @highlight
def spring():
    if speler.vy == 0:
        speler.vy = -150

# @highlight
controller.A.on_event(ControllerButtonEvent.PRESSED, spring)
```

## Verliezen

Om de speler te laten verliezen als deze van een platform afvalt kunnen we het level aanpassen door onderin het level bijvoorbeeld lava tiles toe te voegen.

Wanneer de speler deze raakt is het spel afgelopen en heeft die verloren. Maak hiervoor een functie aan ``raak_lava(sprite, location)`` met hierin de code ``game.game_over(False)``. Gebruik de volgende code om de functie uit te voeren wanneer de speler de lava raakt ``scene.on_overlap_tile(SpriteKind.player, sprites.dungeon.hazard_lava0, raak_lava)``.

```python
scene.set_background_color(9)
speler = sprites.create(img("""
    . . . . . . . . . . . . . . . .
    . . . . . f f f f f f . . . . .
    . . . f f e e e e f 2 f . . . .
    . . f f e e e e f 2 2 2 f . . .
    . . f e e e f f e e e e f . . .
    . . f f f f e e 2 2 2 2 e f . .
    . . f e 2 2 2 f f f f e 2 f . .
    . f f f f f f f e e e f f f . .
    . f f e 4 4 e b f 4 4 e e f . .
    . f e e 4 d 4 1 f d d e f . . .
    . . f e e e e e d d d f . . . .
    . . . . f 4 d d e 4 e f . . . .
    . . . . f e d d e 2 2 f . . . .
    . . . f f f e e f 5 5 f f . . .
    . . . f f f f f f f f f f . . .
    . . . . f f . . . f f f . . . .
"""), SpriteKind.player)

controller.move_sprite(speler)

tiles.set_current_tilemap(tilemap("""level1"""))

scene.camera_follow_sprite(speler)

speler.ay = 350

def spring():
    if speler.vy == 0:
        speler.vy = -150

controller.A.on_event(ControllerButtonEvent.PRESSED, spring)

def raak_lava(sprite, location):
    game.game_over(False)
    
# @highlight
scene.on_overlap_tile(SpriteKind.player,
    sprites.dungeon.hazard_lava0,
    raak_lava)

```

## Winnen

Om de speler te laten winnen plaatsen we aan het einde van het level een kist (chest). Wanneer de speler deze raakt heeft die het spel uitgespeeld.

Dit kan op bijna dezelfde manier als de vorige stap. Maak een functie ``raak_kist(sprite, location)`` en voer deze uit als de speler de kist raakt.

```python
scene.set_background_color(9)
speler = sprites.create(img("""
    . . . . . . . . . . . . . . . .
    . . . . . f f f f f f . . . . .
    . . . f f e e e e f 2 f . . . .
    . . f f e e e e f 2 2 2 f . . .
    . . f e e e f f e e e e f . . .
    . . f f f f e e 2 2 2 2 e f . .
    . . f e 2 2 2 f f f f e 2 f . .
    . f f f f f f f e e e f f f . .
    . f f e 4 4 e b f 4 4 e e f . .
    . f e e 4 d 4 1 f d d e f . . .
    . . f e e e e e d d d f . . . .
    . . . . f 4 d d e 4 e f . . . .
    . . . . f e d d e 2 2 f . . . .
    . . . f f f e e f 5 5 f f . . .
    . . . f f f f f f f f f f . . .
    . . . . f f . . . f f f . . . .
"""), SpriteKind.player)

controller.move_sprite(speler)

tiles.set_current_tilemap(tilemap("""level1"""))

scene.camera_follow_sprite(speler)

speler.ay = 350

def spring():
    if speler.vy == 0:
        speler.vy = -150

controller.A.on_event(ControllerButtonEvent.PRESSED, spring)

def raak_lava(sprite, location):
    game.game_over(False)
    

scene.on_overlap_tile(SpriteKind.player,
    sprites.dungeon.hazard_lava0,
    raak_lava)

# @highlight
def raak_kist(sprite, location):
    game.game_over(True)
    
# @highlight
scene.on_overlap_tile(SpriteKind.player,
    sprites.dungeon.chest_closed,
    raak_kist)
```