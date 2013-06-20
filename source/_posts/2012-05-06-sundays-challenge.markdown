---
layout: post
title: Sunday's Challenge - Learn With Jeff
date: 2012-05-06 10:00
comments: true
categories:
---


<p>Full of the knowledge gained from <a href="http://www.meetup.com/tampa-rb/events/60266012/" target="_blank">Coder Night</a> on Thursday, I made an attempt at creating a poker game. My original plan was to create three classes, a Player class, a Deck class and a Game class. The general construction of the game would be the Game class would use take a new deck object and pop the last card out of the shuffled array and assign it to one of the players in the array “hand”</p>

<p>The first problem I ran into was getting each player cards from the same deck. When I wrote the program the first time I assigned a new deck to each player.</p>

<p>I think I finally figured out the problem there, but I broke the program :/</p>

<p>I am pretty sure the problem is somewhere in my Game class. Any ideas?</p>

<pre><code>require_relative 'player'
class Game
  attr_reader :hand
  attr_accessor :make_game
  def initialize numplayers
    @numplayers = numplayers
    hand = []
  end
  def make_game
    i = 0
    while i &amp;lt; @numplayers
    hand &amp;lt;&amp;lt; Player.new()
    i+=1
    end
  end
end
</code></pre>