<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
  <title></title>
  <link rel="stylesheet" type="text/css" media="all" href="playingCards.ui.css"/>
  <link rel="stylesheet" type="text/css" media="all" href="style.css"/>
  <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
  <script type="text/javascript" src="playingCards.js"></script>
  <script type="text/javascript" src="playingCards.ui.js"></script>
</head>
<body>
  <div id="container">
    <div id="error"></div>
    <div>
      <h2>Your Hand</h2>
      <input type="button" id="draw" value="draw a card" />
      <input type="button" id="addCard" value="add drawn card back" />
      <br/><br/>
    </div>
    <div>
      <div id="yourHand"></div>
      <h2><br/>Card Deck</h2>
      <input type="button" id="shuffler" value="shuffle" />
      <input type="button" id="orderByRank" value="order by rank" />
      <input type="button" id="orderBySuit" value="order by suit" />
      <br/><br/>
      <div id="cardDeck"></div>
    </div>
    <script type="text/javascript">

      $(document).ready(function(){
        var cardDeck = $("#cardDeck").playingCards();
        cardDeck.spread();
        var hand = [];
        var showError = function(msg){
          $('#error').html(msg).show();
          setTimeout(function(){
            $('#error').fadeOut('slow');
          },3000);
        };

        var showHand = function(){
          var el = $('#yourHand');
          el.html('');
          for(var i=0; i<hand.length; i++){
            el.append(hand[i].getHTML());
          }
        };

        var doShuffle = function(){
          cardDeck.shuffle();
          cardDeck.spread();
        };

        var doDrawCard = function(){
          var c = cardDeck.draw();
          if(!c){
            showError('no more cards');
            return;
          }
          hand[hand.length] = c;
          cardDeck.spread();
          showHand();
        };

        var doOrderByRank = function(){
          cardDeck.orderByRank();
          cardDeck.spread();
        };

        var doOrderBySuit = function(){
          cardDeck.orderBySuit();
          cardDeck.spread();
        };

        $('#shuffler').click(doShuffle);

        $('#draw').click(doDrawCard);

        $('#addCard').click(function(){
          if(!hand.length){
            showError('your hand is empty');
            return;
          }
          var c = hand.pop();
          showHand();
          cardDeck.addCard(c);
          cardDeck.spread();
        });

        $('#orderByRank').click(doOrderByRank);

        $('#orderBySuit').click(doOrderBySuit);
      });

    </script>
  </div>

  <script type="text/javascript">

    var _gaq = _gaq || [];
    _gaq.push(['_setAccount', 'UA-16813977-1']);
    _gaq.push(['_trackPageview']);

    (function() {
      var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
      ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
      var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
    })();

  </script>
</body>
</html>


