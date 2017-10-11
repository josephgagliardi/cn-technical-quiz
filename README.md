# Joseph Gagliardi Technical Quiz

### Question 1: 
Using PHP and HTML, create a page that takes the data from the two JSON feeds below and combines them using the ID property. Output the resulting data with these properties: ID, show, and game.

JSON 1: http://www.cartoonnetwork.com/test/backend-quiz/games.json

JSON 2: http://www.cartoonnetwork.com/test/backend-quiz/shows.json

```php
<?php

$json1 = file_get_contents('http://www.cartoonnetwork.com/test/backend-quiz/games.json');
$json2 = file_get_contents('http://www.cartoonnetwork.com/test/backend-quiz/shows.json');

$games = json_decode($json1)->games;
$shows = json_decode($json2)->shows;

$media = array();

foreach ($games as $game) {
    $id = $game->id;
    foreach ($shows as $show) {
        if ($show->id == $id) {
            $data = (object) array_merge((array) $game, (array) $show);
            array_push($media, $data);
        }
    }
}

foreach($media as $item){
    echo "<p>".$item->id."</p>";
    echo "<p>".$item->show."</p>";
    echo "<p>".$item->game."</p>";
}


?>
```
Example: https://www.tehplayground.com/kR8zMliUo9ao26zU




### Question 2:

Using PHP, create a function that loops through the following array and outputs the resulting HTML.

Then, using JavaScript (jQuery is allowed), add the following functionality: clicking one of the games on the left should display the corresponding badges in the panel on the right.

Example JS: http://jsfiddle.net/n0opfr4m/

Example PHP and Markup:

```php
<?php
$json_string = 
<<<EOD
[
{
game: "Royal Ruckus",
badges: ["Approximate Beatdown", "Huge Money", "Taste the Rainbow", "Done & Dungeon", "Let's Rage"]
},
{
game: "Cake's Tough Break",
badges: ["Nip It!", "Yay BMO!", "One Fast Cat", "Hang In There, Baby", "Piece of Cake", "Super Amadeus"]
},
{
game: "Lemon Break",
badges: ["Lemon Aid", "Sweet Kicks", "BMO Hope", "Elephant Prowess", "Unacceptable Escape"]
},
{
game: "Finn & Bones",
badges: ["Rock Family Tree", "Clash of Bones", "Chemistry 101", "Mix Master", "Kiss of Death"]
}
])
EOD;

$badgeArray = json_decode($json_string);

?>

<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8">

  <title>Game Badges</title>
  <meta name="description" content="Game Badges">
  <meta name="author" content="Joseph Gagliardi">

  <link rel="stylesheet" href="css/styles.css?v=1.0">

  <!--[if lt IE 9]>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html5shiv/3.7.3/html5shiv.js"></script>
  <![endif]-->
  
  <script
  src="https://code.jquery.com/jquery-3.2.1.js"
  integrity="sha256-DZAnKJ/6XZ9si04Hgrsxu/8s717jcIzLy3oi35EouyE="
  crossorigin="anonymous"></script>
  
  <script>
    //Control dynamic display of tabbed content
	$('.nav ul li:first').addClass('active');
	$('.tab-content:not(:first)').hide();
	$('.nav ul li a').click(function(event) {
		event.preventDefault();
		var content = $(this).attr('href');
		$(this).parent().addClass('active');
  	$(this).parent().siblings().removeClass('active');
		$(content).show();
		$(content).siblings('.tab-content').hide();
	});
  </script>
</head>

<body>
    <div class="nav">
        <ul id="games">
        <?php foreach ( $badgeArray as $game ) : ?>
        <?php $name = $game->game; ?>
            <li class="active">
                <a href="#section-$name">$name</a>
            </li>
        <?php endforeach; ?>
        </ul>
    </div>
    <?php foreach ( $badgeArray as $game ) : ?>
    <?php $name = $game->game; ?>
    <div class="section tab-content" id="section-$name">
	    <h1>$name</h1>
	    <ul>
        <?php foreach ( $game->badges as $badge ) : ?>
        	<li>
				<a href="#">$badge</a>
			</li>
	    <?php endforeach; ?>
	    </ul>
    </div>
</body>
</html>
```

### Question 3:

Write the following SQL statements.

a) Get Phone number of Mary Parker

```sql
SELECT phone FROM employees WHERE FNAME = 'Mary' AND LNAME = 'PARKER'
```

b) Remove Janice Greenwald
```sql
DELETE FROM employees
WHERE FNAME = 'Janice' AND LName = 'Greenwald';
```

c) Increase Michael Pennington's salary by 10%
```sql
UPDATE employee
SET salary =  salary * 1.1 
WHERE FNAME = 'Michael' AND LName = 'Pennington';
```

### Question 4: 
Using PHP, write a function that opens and saves a file.

```php
function saveFile() {
    $file = 'demo.txt';
    $handle = fopen($file, 'w') or die('Cannot open file:  '.$file);
    fclose($handle);
}
```

#### Bonus:

##### 1. Explain how Drupal 8 Caching works: 
Drupal 8 Cache works by assigning various tags to blocks of content for the purpose of caching. This allows the CMS to dynamically re-render only the updated pieces of content or underlying structure based on the tag instead of requiring a purge of the entire cached block. This is very powerful because it means that a change to content does not necessarily mean the menu structure or associated content will require a re-render from the server and unlike previous version of Drupal, Drupal 8 simplifies caching configuration by allowing configuration only of a max age parameter to inform the browser how often to purge this cache rather than in previous versions of the CMS which required additional knowledge regarding the server and other session information. 

Additionally, and for greater control over the scoping of caching layers, Drupal 8 allows declaration and configuration of caching at the level of various contexts including the user, session, and request context.
