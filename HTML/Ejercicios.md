## HTML Attributes

##### Add a tooltip
    <p title="About W3Schools">W3Schools is a web developer's site.</p>

##### Set the size of the image to 250 pixels wide and 400 pixels tall.
    <img src="w3schools.jpg" width="250" height="400">

##### Make the element below into a link that goes to "https://www.w3schools.com".
    <a href="https://www.w3schools.com">This is a link</a>

##### Specify an alternate text for the image.
Alternate text is useful when the image cannot be displayed, like when the page is read by a screen reader.
    <img src="w3schools.png" *alt*="w3schools Logo">

## HTML Headings

##### Use the correct HTML tag to add a heading with the text "London".
    <h1>London</h1>

##### Add a horizontal rule between the heading and the paragraph.
    <h1>London</h1>
    <hr>
    <p>London is the capital city of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13       million inhabitants.</p>

##### Add six headings to the document with the text "Hello".
    <html>
    <body>
    <h1>Hello</h1>
    <h2>Hello</h2>
    <h3>Hello</h3>
    <h4>Hello</h4>
    <h5>Hello</h5>
    <h6>Hello</h6>
    </body>
    </html>

##### Mark up the text with appropriate tags:

"Universal Studios Presents" is the most important heading.
"Jurassic Park" is the next most important heading.
"About" is the third most important heading.
The last sentence is just a paragraph.
Start with the most important heading (the largest) and end with the least important heading (the smallest).

    <h1>Universal Studios Presents</h1>
    <h2>Jurassic Park</h2>
    <h3>About</h3>
    <p>On the Island of Isla Nublar, a new park has been built: Jurassic Park is a theme park of cloned dinosaurs!!</p>

## HTML Paragraphs

##### Use the correct HTML tag to add a paragraph with the text "Hello World!".

    <html>
    <body>
    <p>Hello World!</p>
    </body>
    </html>
    
##### Clean up this document with proper end tags.
    <h1>This is a Heading</h1>
    <p>This is a paragraph.</p>

##### Add a line break in the middle of the paragraph:
    <p>My Bonnie lies<br>over the ocean.</p>
    
##### Wrap this poem around HTML tags that will preserve all spaces and linebreaks when the element is displayed.
    <pre>
      My Bonnie lies over the ocean.

      My Bonnie lies over the sea.

      My Bonnie lies over the ocean.

      Oh, bring back my Bonnie to me.
    </pre>

## HTML Styles
 
##### Use the correct HTML attribute, and CSS, to set the color of the paragraph to "blue".
    <p style="color:blue;">This is a paragraph.</p>
 
##### Use CSS to set the font of the paragraph to "courier".
    <p style="font-family:courier;">This is a paragraph.</p>
    
 ##### Use CSS to center align the paragraph.
    <p style="text-align:center;">This is a paragraph.</p>
    
##### Use CSS to set the text size to 50 pixels.
    <p style="font-size:50px;">This is a paragraph.</p>
    
##### Use CSS to set the background-color of the document to yellow.
    <html>
    <body style="background-color:yellow;">
    <h1>This is a heading</h1>
    <p>This is a paragraph.</p>
    </body>
    </html>
    
##### Use CSS to center align the document.
    <html>
    <body style="text-align:center;">
    <h1>This is a heading</h1>
    <p>This is a paragraph.</p>
    </body>
    </html>

## HTML Formatting
 
##### Add extra importance to the word "degradation" in the paragraph below.
    <p>WWF's mission is to stop the <strong>degradation</strong> of our planet's natural environment.</p>
    
##### Emphasize the word "metropolitan" in the text below.
    <h1>Tokyo</h1>
    <p>Tokyo is the capital of Japan, the most populous <em>metropolitan</em> area in the world.</p>
  <p>Tokyo is the capital of Japan, the most populous <em>metropolitan</em> area in the world.</p>
  
##### Highlight the word "FUN" in the text below.
    <p>HTML is <mark>FUN</mark> to learn!</p>
  <p>HTML is <mark>FUN</mark> to learn!</p> (FUN se debería ver con un color de fondo amarillo)
 
 ##### Apply subscript formatting to the number "2" in the text below.
    <p>H<sub>2</sub>O is the scientific term for water.</p> 
  <p>H<sub>2</sub>O is the scientific term for water.</p>
  
##### Add a line through (strikeout) the letters "blue" in the text below.
    <p>My favorite color is <del>blue</del> red.</p>
   <p>My favorite color is <del>blue</del> red.</p>
   
## HTML Quotations

##### Use an HTML element to add quotation marks around the letters "cool".
    <p>I am so <q>cool</q>.</p>
   <p>I am so <q>cool</q>.</p>
   
##### The text below should be a quoted section.
Add the proper HTML element to it, and specify that it is quoted from the following URL:
http://www.worldwildlife.org/who/index.html

    <blockquote cite="http://www.worldwildlife.org/who/index.html">
    For 50 years, WWF has been protecting the future of nature. The world's leading conservation organization, WWF works in 100             countries and is supported by 1.2 million members in the United States and close to 5 million globally.
    </blockquote>

##### Make the text below go right-to-left.
    <bdo dir="rtl">What a beautiful day!</bdo>

##### The letters "WHO" in the text below is an abbreviation of "World Health Organization".
Use an HTML element to provide the specified abbreviation of "WHO".
    <p>The <abbr title="World Health Organization"> WHO</abbr> was founded in 1948.</p>

## HTML Comments

##### Use the HTML comment tag to make a comment out of the "This is a comment" text.
    <h1>This is a heading</h1>
    <!-- This is a comment -->
    <p>This is a paragraph.</p>
    
##### Add comment tags around the paragraph:
    <!-- <p>This is a paragraph.</p> -->

## HTML CSS

##### Use CSS to set the background color of the document (body) to yellow.
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    body
     {
        background-color:yellow;
     }
    </style>
    </head>
    <body>

    <h1>My Home Page</h1>

    </body>
    </html>
    
##### Use CSS to set the font of the document to "courier".
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    body {
        font-family:courier;
        }
    </style>
    </head>
    <body>

    <h1>My Home Page</h1>

    </body>
    </html>
    
##### Use CSS to set the text color of the document to red.
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    body {
    color:red;
    }
    </style>
    </head>
    <body>

    <h1>My Home Page</h1>

    </body>
    </html>
    
##### Use CSS to make a yellow, 1 pixel thick, border around all paragraphs.
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    p { border: 1px solid yellow;
    }
    </style>
    </head>
    <body>

    <p>This is a paragraph.</p>
    <p>This is a paragraph.</p>
    <p>This is a paragraph.</p>

    </body>
    </html>

##### Use the correct attribute to make sure that the last paragraph gets the styling as described in the style element.
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    #special {
      color:gray;
      background-color:lightblue;
    }
    </style>
    </head>
    <body>

    <p>This is a paragraph.</p>
    <p>This is a paragraph.</p>
    <p id="special">This is a paragraph.</p>

    </body>
    </html>
    
##### Use the correct attribute to make sure that the last paragraph gets the styling as described in the style element.
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    p.intro {
      font-size:20px;
      color:gray;
      background-color:lightblue;
    }
    </style>
    </head>
    <body>
    <p>This is a paragraph.</p>
    <p>This is a paragraph.</p>
    <p class="intro">This is a paragraph.</p>
    </body>
    </html>
    
## HTML Links

#####  Use the correct HTML to make the text below into a link to "default.html".
    <a href="default.html">Visit our HTML tutorial.</a>

##### Use CSS to remove the underline from the link.
    <a href="html_images.asp" style="text-decoration:none">HTML Images</a>
    
##### Use the correct HTML attribute to make the link open in a new window.
    <a href="html_images.asp" target="_blank">HTML Images</a>
    
##### Use the correct HTML to make the image become a link to "default.html".
    <a href="default.html">
    <img src="smiley.gif">
    </a>

##### Add a "tooltip" to the link.

The "tooltip" should say "Home".
    <a href="default.html" title="Home">Back to Home</a>
 
## HTML Images

##### Use the HTML image attributes to set the size of the image to 250 pixels wide and 400 pixels tall.
    <img src="scream.png" width="250" height="400">
    
##### Use CSS to set the size of the image to 250 pixels wide and 400 pixels tall.
    <img src="scream.png" style="width:250px;height:400px;">
    
##### Use the correct HTML to make the image become a link to "default.html".
    <a href="default.html">
    <img src="smiley.gif">
    </a>

##### Make the image below float to the right of the paragraph.
    <p>
        <img src="smiley.gif" style="float:right;">
        This is a paragraph.
        This paragraph contains an image
    </p>
    
##### Add the correct HTML attribute to display the "smiley.gif" image.
    <img src="smiley.gif">

##### Specify an alternate text for the image.
The alternate text should say "Smiley".
Alternate text is useful when the image cannot be displayed, like when the page is read by a screen reader.

    <img src="smiley.gif" alt="Smiley">

## HTML Tables

##### Add a table row with two table headers.
The two table headers should have the value "Name" and "Age".

        <table>
        <tr>
            <th>Name</th>
            <th>Age</th>
        </tr>
         <tr>
            <td>Jill Smith</td>
            <td>50</td>
         </tr>
        </table>
        
<table>
<tr>
    <th>Name</th>
    <th>Age</th>
</tr>
 <tr>
    <td>Jill Smith</td>
    <td>50</td>
 </tr>
</table>

##### Add a table caption that says "Names".

    <table> 
    <caption>Names</caption>
      <tr>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Points</th>
      </tr>
      <tr>
        <td>Jill</td>
        <td>Smith</td>
        <td>50</td>
      </tr>
    </table>

<table> 
<caption>Names</caption>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Points</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
</table>

##### Use CSS styles to make the table 300 pixels wide.
    <table style="width:300px">
      <tr>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Points</th>
      </tr>
      <tr>
        <td>Jill</td>
        <td>Smith</td>
        <td>50</td>
      </tr>
    </table>

<table style="width:300px">
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Points</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
</table>

##### Add a table row at the end of the table, with two table cells.

The two table cells should have the value "Eve Jackson" and "94".

        <table>
          <tr>
            <th>Name</th>
            <th>Age</th>
          </tr>
          <tr>
            <td>Jill Smith</td>
            <td>50</td>
          </tr>
          <tr>
            <td>Eve Jackson</td>
            <td>94</td>
          </tr>
        </table>
        
<table>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve Jackson</td>
    <td>94</td>
  </tr>
</table>

##### Use the correct HTML attribute to make the first TH element span two columns.
        <table>
          <tr>
            <th colspan="2">Name</th>
            <th>Age</th>
          </tr>
          <tr>
            <td>Jill</td>
            <td>Smith</td>
            <td>50</td>
          </tr>
          <tr>
            <td>Eve</td>
            <td>Jackson</td>
            <td>94</td>
          </tr>
        </table> 

<table>
  <tr>
    <th colspan="2">Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table>

##### Use the correct HTML attribute to make the second TH element span two rows.
    <table>
      <tr>
        <th>Name</th>
        <td>Jill Smith</td>
      </tr>
      <tr>
        <th rowspan="2">Phone</th>
        <td>555-77854</td>
      </tr>
      <tr>
        <td>555-77854</td>
      </tr>
    </table>

<table>
  <tr>
    <th>Name</th>
    <td>Jill Smith</td>
  </tr>
  <tr>
    <th rowspan="2">Phone</th>
    <td>555-77854</td>
  </tr>
  <tr>
    <td>555-77854</td>
  </tr>
</table>


## HTML List

##### Add a list item with the text "Coffee" inside the <ul>.
    
    <ul>
    <li>Coffee</li>
    </ul>
##### Finish the HTML code to make an ordered list.

    <ol>
      <li>Coffee</li>
      <li>Tea</li>
      <li>Milk</li>
    </ol>

##### Use CSS to display squares instead of bullets.
    <ul style="list-style-type:square;">
      <li>Coffee</li>
      <li>Tea</li>
      <li>Milk</li>
    </ul>
##### Use the correct HTML attribute to display letters (uppercase ABC) instead of numbers.
    <ol type="A">
      <li>Coffee</li>
      <li>Tea</li>
      <li>Milk</li>
    </ol>
##### Use the correct HTML attribute to display uppercase roman numbers.
    <ol type="I">
      <li>Coffee</li>
      <li>Tea</li>
      <li>Milk</li>
    </ol>
    
##### Use the correct HTML elements to make a description of each term in the description list.
    <dl>
      <dt>Coffee</dt>
        <dd>
        - black hot drink
        </dd>
      <dt>Milk</dt>
        <dd>
        - white cold drink
        </dd>
    </dl>
    
## HTML Classes

##### Create a class selector named "special".

Add a color property with the value "blue" inside the "special" class.

    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .special 
    {
      color:blue;
    }
    </style>
    </head>
    <body>
    <p class="special">My paragraph</p>
    </body>
    </html>
    
##### Add the correct class to make the H1 element red.
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .mystyle {color:red;}
    </style>
    </head>
    <body>

    <h1 
    class="mystyle">My Home Page</h1>

    </body>
    </html>
    
##### Add two classes to the H1 element, to make the background pink and the color red.
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .intro {background:pink;}
    .special {color:red;}
    </style>
    </head>
    <body>
    <h1 class="intro special">My Home Page</h1>
    </body>
    </html>
    
## HTML Id

##### Add the correct HTML attribute to make the H1 element red.
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    #myheader {color:red;}
    </style>
    </head>
    <body>

    <h1 id="myheader">My Home Page</h1>

    </body>
    </html>
    
##### Create an id selector named "special".

Add a color property with the value "blue" inside the "special" declaration block.

    <!DOCTYPE html>
    <html>
    <head>
    <style>
    #special
    {
    color:blue    ;
    }
    </style>
    </head>
    <body>
    <p id="special">My paragraph</p>
    </body>
    </html>

## HTML Iframes

##### Create an iframe with a URL address that goes to https://www.w3schools.com.
    <iframe src="https://www.w3schools.com"></iframe>
    
##### Use an iframe attribute to make the iframe 500 pixels wide.
    <iframe src="https://www.w3schools.com" width="500"></iframe>
    
##### Use CSS to display an iframe with no borders.
    <iframe src="https://www.w3schools.com" style="border:none"></iframe>
    
##### Create an iframe with a URL address that goes to "default.html".
    <iframe src="default.html">

## HTML Scripts

##### Use JavaScript to change the HTML content of the <p> element to "Hello World!".
    
    <body>
    <p id="demo">Hi.</p>
    <script>
    document.getElementById("demo").innerHTML = "Hello World!";
    </script>
    </body>
##### Use JavaScript to change the text size of the <p> element to 40 pixels.
    
    <body>
    <p id="demo">Hi.</p>
    <script>document.getElementById("demo").style.fontSize = "40px";</script>
    </body>

##### Use JavaScript to set the color of the <p> element to "red".
    
    <body>
    <p id="demo">Hi.</p>
    <script>document.getElementById("demo").style.color = "red";
    </script>
    </body>
 
##### Use JavaScript to change the image source from "scream.png" to "smiley.gif".
    <body>
    <img id="demo" src="scream.png">
    <script>
    document.getElementById("demo").src = "smiley.gif";</script>
    </body>

## HTML Computercode

##### Define the text "var person;" as programming code.
    <p>Code example: <code>var person;</code></p>
    
##### Define the text inside the <code> element as preformatted text (to preserve spaces and line breaks).

    <p>Code example:</p>
    <pre>
    <code>var person = {
      firstName:"John",
      lastName:"Doe"
    }</code>
    </pre>


##### Define the character "x" in the equation as a variable.
    <p>A simple math equation: <var>x</var> = 3 + 2; </p>
    
## HTML Forms

##### In the form below, add an input field with the type "button" and the value "OK".
    <form>
    <input type="button" value="OK">
    </form>
    
##### In the form below, add two radio buttons, both with the name "gender".
    <form>
    <input type="radio" name="gender" value="male"> Male
    <input type="radio" name="gender" value="female"> Female
    </form>
    
##### Add a submit button, and specify that the form should go to "/action_page.php".
    <form action="/action_page.php">
    Name: <input type="text" name="name">
    <input type="submit">
    </form>
    
##### Specify that the form is submitted using the "POST" method.
    <form action="/action_page.php" method="post">
    Name: <input type="text" name="name">
    <input type="submit">
    </form>
    
##### In the form below, add an empty drop down list with the name "cars".
    <form action="/action_page.php">
    <select name="cars">
    </select>
    </form>
    
##### In the form below, add two option elements to the drop down list.

The first option must have the value "Volvo"
The second option must have the value "Ford".

    <form action="/action_page.php">
    <select name="cars">
    <option value="Volvo">Volvo</option>
    <option value="Ford">Ford</option>
    </select>
    </form>
    
##### In the form below, add a text area with the name "note".

    <form action="/action_page.php">
    <textarea name="note"></textarea>
    </form>

## HTML Input Types

##### In the form below, add an input field for text, with the name "username" .
    <form action="/action_page.php">
    <input type="text" name="username">
    </form>
    
##### In the form below, add a submit button with the value "Submit Form".
    <form action="/action_page.php">
    <input type="text" name="username">
    <input type="submit" value="Submit Form">
    </form>
    
##### Add two radio buttons with the name "color".
    <form action="/action_page.php">
      Favorite color:
      Blue
      <input value="blue" type="radio" name="color">
      Red
      <input value="red" type="radio" name="color">
      <input type="submit">
    </form>
    
##### In the form below, add a <button> element with the text "Click Me".
    
    <form action="/action_page.php">
    <button>Click Me</button>
    </form>
    
##### In the form below, add a input field that can only contain numbers
Use the correct input attributes to only allow numbers between 1 and 5.

    <form action="/action_page.php">
    <input type="number" min="1" max="5">
    </form>

## HTML Form Attributes

##### In the input field below, add placeholder that says "Your name here".
    <form action="/action_page.php">
    <input type="text" placeholder="Your name here">
    </form>
    
##### Disable the input field below.
    <form action="/action_page.php">
    <input type="text" disabled>
    </form>
    
##### Set the max numbers of characters allowed in the input field to 40.
    <form action="/action_page.php">
    <input type="text" maxlength="40">
    </form>
    
##### Set the input field to be read only (meaning that the value cannot be changed).

    <form action="/action_page.php">
    <input type="text" readonly>
    </form>
