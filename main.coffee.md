Editor
======

Our editor will allow editing of abilities, effects, map chunks, characters, and
possibly more. Pretty much everything in the game.

Tilesets and images too.

    require "./setup"

    Canvas = require "touch-canvas"

    App = require "./pixie"

    canvas = Canvas
      width: App.width
      height: App.height

    $("body").append canvas.element()
    
    canvas.fill "#F00"
