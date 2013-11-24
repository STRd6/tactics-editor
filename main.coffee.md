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

    canvas.on "touch", (position) ->
      console.log position.scale(tileSize).floor()
