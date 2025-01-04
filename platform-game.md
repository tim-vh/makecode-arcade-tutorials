# Platform game tutorial

## Introductie @showdialog

Tutorial om een platform game te maken.

Gebaseerd op de video [How to Make a Platformer Game](https://www.youtube.com/watch?v=9bSX9Q5aP6E) van Microsoft MakeCode


## Achtergrond kleur instellen

Voeg een blok toe om de achtergrond kleur van het spel te veranderen naar blauw. Dit blok is te vinden in de ``||scene:Scene||`` categorie.

```blocks
scene.setBackgroundColor(9)
```

## Sprite voor de speler toevoegen

Voeg een sprite toe voor de speler. Als de sprite is toegevoegd willen we deze kunnen besturen met de pijltjestoetsen. 

```blocks
scene.setBackgroundColor(9)
let speler = sprites.create(img`
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
    `, SpriteKind.Player)
controller.moveSprite(speler)
```

## Platforms toevoegen

Om een level met platforms te maken voegen we een tilemap toe aan ons spel.

Voeg daarna tiles toe aan de tilemap die je hebt toegevoegd. Deze tiles gebruiken we als platforms waar de speler op kan springen.

Om het spel te laten weten dat we op de platforms moeten kunnen staan geven we in de tilemap editor aan dat het 'walls' of 'muren' zijn.

Om ervoor te zorgen dat we door het hele level kunnen bewegen willen we er voor zorgen dat de camera meebeweegt met de speler.

```blocks
scene.setBackgroundColor(9)
let speler = sprites.create(img`
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
    `, SpriteKind.Player)
controller.moveSprite(speler)
// @highlight
tiles.setCurrentTilemap(tilemap`level1`)
// @highlight
scene.cameraFollowSprite(speler)
```

## Zwaartekracht

Om de speler naar beneden te laten vallen voegen we een y-acceleration toe van 350.

```blocks
scene.setBackgroundColor(9)
let speler = sprites.create(img`
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
    `, SpriteKind.Player)
controller.moveSprite(speler)
tiles.setCurrentTilemap(tilemap`level1`)
scene.cameraFollowSprite(speler)
// @highlight
speler.ay = 350
```

## Springen

We kunnen de speler laten springen door de y-snelheid van de speler in te stellen op -150 als er op de a knop wordt gedrukt.

Om ervoor te zorgen dat we niet in de lucht kunnen springen willen we de y-snelheid alleen veranderen als deze op dat moment 0 is.

```blocks
scene.setBackgroundColor(9)
let speler = sprites.create(img`
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
    `, SpriteKind.Player)
controller.moveSprite(speler)
scene.cameraFollowSprite(speler)
tiles.setCurrentTilemap(tilemap`level1`)
speler.ay = 350

// @highlight
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    if (speler.vy == 0) {
        speler.vy = -150
    }
})
```

## Verliezen

Om de speler te laten verliezen als deze van een platform afvalt kunnen we het level aanpassen door onderin het level bijvoorbeeld lava tiles toe te voegen.

Wanneer de speler deze raakt is het spel afgelopen en heeft die verloren.

```blocks
scene.setBackgroundColor(9)
let speler = sprites.create(img`
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
    `, SpriteKind.Player)
controller.moveSprite(speler)
scene.cameraFollowSprite(speler)
tiles.setCurrentTilemap(tilemap`level1`)
speler.ay = 350

// @highlight
scene.onOverlapTile(SpriteKind.Player, lava, function (sprite, location) {
    game.gameOver(false)
})
```

## Winnen

Om de speler te laten winnen plaatsen we aan het einde van het level een chest (kist). Wanneer de speler deze raakt heeft die het spel uitgespeeld.

```blocks
scene.setBackgroundColor(9)
let speler = sprites.create(img`
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
    `, SpriteKind.Player)
controller.moveSprite(speler)
scene.cameraFollowSprite(speler)
tiles.setCurrentTilemap(tilemap`level1`)
speler.ay = 350

// @highlight
scene.onOverlapTile(SpriteKind.Player, chest, function (sprite, location) {
    game.gameOver(true)
})
```