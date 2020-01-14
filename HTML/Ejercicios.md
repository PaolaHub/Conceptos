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
   
#####

#####

#####

#####

#####

#####

#####

#####

 
 
