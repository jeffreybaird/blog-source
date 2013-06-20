---
layout: post
title: I/O...FINALLY! - Learn With Jeff
date: 2012-05-21 10:00
comments: true
categories:
---

<p>When I was learning to play the piano, I remember wanting to jump right into Billy Joel. “Hot Cross Buns” and “Mary Had a Little Lamb” were boring and very uncool for an eight year old boy to be learning.</p>

<p>I have had the same feeling while learning to code. I spent a lot of time doing methods, objects and classes never really getting to use them as I would in the real world.</p>

<p>There is one question I wanted to be able answer since the day I started programming: “How the hell do I interact with a program?”</p>

<p>Today, I figured that out.  The code below is from the main program file for the game I created in the <a href="http://online.pragmaticstudio.com/courses/ruby">Pragmatic Studios course</a>. In it, there are two examples of some of ruby’s basic input functions.</p>

<pre><code>knuckleheads = StudioGame::Game.new(&amp;quot;Knuckleheads&amp;quot;)

default_player_file = File.join(File.dirname(__FILE__), 'players.csv')
knuckleheads.load_players(ARGV.shift || default_player_file)

loop do
  puts &amp;quot;\nHow many game rounds do you want to play?&amp;quot;
  answer = gets.downcase.chomp
  case answer
  when /^\d+$/
    knuckleheads.play(answer.to_i)
  when 'quit','exit'
    knuckleheads.print_stats
    break
  else
    puts &amp;quot;Please enter a number or 'quit'&amp;quot;
  end
end

knuckleheads.save_high_scores
</code></pre>

<p>The first input I learned was the “gets” method. Here, the program prompts the user to provide a number, the code checks that it is in fact a number (or a quit command) and then uses the number as an argument for the method.</p>

<pre><code>loop do
  puts &amp;quot;\nHow many game rounds do you want to play?&amp;quot;
  answer = gets.downcase.chomp
  case answer
  when /^\d+$/
    knuckleheads.play(answer.to_i)
  when 'quit','exit'
    knuckleheads.print_stats
    break
  else
    puts &amp;quot;Please enter a number or 'quit'&amp;quot;
  end
</code></pre>

<p>The next one is a little more complicated so I will try to break it up into pieces.</p>

<p>What I am trying to accomplish is to allow non-programmers to add players to my game using a csv file and no code. They should be able to simply input the name of a player and the program automatically adds a Player object to the game.</p>

<p>To do this I created a player.csv file (in the above code a person could theoretically create their own file and load it in) with a series of players each on their own line. Then I included the following code in my Game class:</p>

<pre><code>  def load_players (filename=&amp;quot;players.csv&amp;quot;)
    CSV.foreach(filename) do |line|
      player = Player.new(line[0], line[1].to_i)
      add_player(player)
    end
  end
</code></pre>

<p>This takes a file (defaulted with my players.csv) and goes through each line of the file, creating a Player object for each one.</p>

<p>Then, I included this in the main program file:</p>

<pre><code>default_player_file = File.join(File.dirname(__FILE__), 'players.csv')
knuckleheads.load_players(ARGV.shift || default_player_file)
</code></pre>

<p>This loaded the players from the file given by the user or my default file if none is give and then runs the program as normal.</p>

<p>So, after two months of hard work and a steep learning curve I have completed my first gem! w00t! You can download it if you want:</p>

<p>$gem install blam_and_woot</p>

<p>If you want to peek at the source code you can find it<a href="https://github.com/jeffreybaird/blam_and_woot">here</a></p>

<p>I will be writing about packaging the gem and some issues I ran into with that later. For now, I am celebrating!</p>