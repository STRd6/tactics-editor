Editor
======

Our editor will allow editing of abilities, effects, map chunks, characters, and
possibly more. Pretty much everything in the game.

Tilesets and images too.

    require "./setup"

    Canvas = require "touch-canvas"
    Sprite = require "sprite"

    App = require "./pixie"

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
        x = (i % 32).floor() * 32
        y = (i / 32).floor() * 32

        sprite.draw canvas, x, y
    , 10
