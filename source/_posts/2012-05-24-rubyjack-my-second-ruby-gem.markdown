---
layout: post
title: RubyJack my second Ruby Gem! - Learn With Jeff
date: 2012-05-24 10:00
comments: true
categories:
---

<p>For the last two days I have been slaving over my second attempt at a real ruby program, this one with no help from my friends over at pragmatic programming. I am going to briefly go over something I learned doing this, some of the problems I faced and some of the features I am still working on.</p>

<p>If you want to find the project I am working on, the source code can be found <a href="https://github.com/jeffreybaird/RubyJack/tree/master/black_jack">here</a> on my GitHub profile.</p>

<p>You can install the gem with $gem install RubyJack</p>

<h2>TIL:</h2>

<p>Today I learned a little bit about ruby’s regular expressions. I  know there is a lot more that I don’t know about them, but from what I can tell, they are powerful. The most basic definition I could find of a regular expression is from the Programming Ruby 1.9 book (the latest PickAxe addition):</p>

<blockquote>
<p>A regular expression is a pattern that can be matched against a string. It can be a simple pattern, such as <em>the string must contain the sequence of letters “cat”,</em> or the pattern can be complex, such as <em>the string must start with a protocol identifier, followed by two literal forward slashes, followed by…,</em> and so on. This is cool in theory. But what makes reqular expressions so powerful is what you can do with them in practice:</p>

<p>-You can test a string to see whether it matches a pattern
-You can extract from a string the sections that match all or part of a pattern.
-You can change the string, replacing parts that match a pattern</p>
</blockquote>

<p>The job I needed regular expressions for in my code is most likely based in the poor design of my deck of cards. The following is the code that initialized a new deck:</p>

<pre><code>def create_a_deck
  new_suits = %w(hearts spades clubs diamonds )
  new_value = %w(Ace 2 3 4 5 6 7 8 9 10 Jack Queen King)
  @new_deck = Array.new
  #creates a new array by combining the information in the
  #above two
  new_value.each do |card|
    new_suits.each do |suited|
      @new_deck &amp;lt;&amp;lt; &amp;quot;#{card} of #{suited}&amp;quot;
    end
  end
end
</code></pre>

<p>What I am doing above is creating an array of strings that have combined the strings found in the “new_suits” array and the “new_value” array above to make a new array that includes an entire deck. The iterator starts with “Ace” and combines it with “hearts” to make “Ace of hearts” which is then added on to the end of the @new_deck array. The iterator goes through and makes 52 cards in this fashion.</p>

<p>The problem with this method of making a deck is that all of my cards are now Strings and I need a way to covert them into point values for the Black Jack game. I did some research and came upon regular expressions.</p>

<p>Here is the method I used to parse the deck and assign values:</p>

<pre><code>def card_value card
  if card =~ /Queen/
    10
  elsif card =~ /King/
    10
  elsif card =~ /Jack/
    10
  elsif card =~ /Ace/
    11
  elsif card =~ /2/
    2
  elsif card =~ /3/
    3
  elsif card =~ /4/
    4
  elsif card =~ /5/
    5
  elsif card =~ /6/
    6
  elsif card =~ /7/
    7
  elsif card =~ /8/
    8
  elsif card =~ /9/
    9
  elsif card =~ /10/
    10
  else
    0
  end
end
</code></pre>

<p>I have a gut feeling that any rubyists that are reading this, died a little bit inside with that method. However, it got the job done and it taught me a little about regular expressions. Essentially what this method does is search the string I give it (I’m using this with an iterator and passing it each card in the player’s hand) and assigning a value based on what it finds. I will probably add another method to this in order to expand upon the Ace, but more on that later.</p>

<h2>Problems I faced:</h2>

<p>So there are a couple parts to blackjack that were a little tough for me to get in the program. They are, dealer play, the option of playing an Ace as a 1 or 11, and the ability to bet.  I am not going to attack the betting capability just yet but I do think I will discuss dealer play and  Ace action.</p>

<h3>Dealer Play:</h3>

<p>On the surface, this problem seemed pretty simple. The dealer is just a special player. So, create a subclass of player and write some methods that automate the play of the dealer (I won’t paste all that code here, go look at the source!). However, every time I called a method from the dealer class my program crashed. I have to keep fiddling with that to see if I can get it to work.</p>

<h3>Ace Action:</h3>

<p>I actually think I solved this problem while I was writing this blog post (which is why I write this blog). I think if I add call a method in when the card_value method finds “Ace” that prompts the user to make a choice, it will solve the problem. The tricky part will be offering that choice repeatedly (so if the user changes his mind later in the hand) and automating it for the dealer.</p>

<h2>Features to come:</h2>

<p>So you can probably gather that I plan on adding the above two features today. Another feature that I want to add is the ability of the user to place bets, have holdings and play multiple games.</p>

<p>Please go play the game ($gem install RubyJack) and give me some feedback! Thanks!</p>
