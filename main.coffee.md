Editor
======

Our editor will allow editing of abilities, effects, map chunks, characters, and
possibly more. Pretty much everything in the game.

Tilesets and images too.

    require "./setup"

    Canvas = require "touch-canvas"
    Sprite = require "sprite"

    App = require "./pixie"

    {Size} = require "./lib/util"

    tileExtent = Size(32, 18)
    tileSize = Size(32, 32)

    canvas = Canvas
      width: App.width
      height: App.height

    $("body").append canvas.element()

    canvas.fill "#000"

    global.canvas = canvas

    images = JSON.parse(localStorage.images)

    sprites = Object.keys(images).map (name) ->
      Sprite.load(images[name])

    setTimeout ->
      sprites.forEach (sprite, i) ->
        {x, y} = tileSize.mapping(i).scale(tileSize)

        sprite.draw canvas, x, y
    , 10

    spriteToDataURL = (sprite) ->
      tmpCanvas = Canvas sprite

      sprite.draw(tmpCanvas, 0, 0)

      tmpCanvas.element().toDataURL()

    canvas.on "touch", (position) ->
      p = position.scale(tileExtent).floor()
      n = tileSize.mapping(p)

      console.log spriteToDataURL sprites[n]
