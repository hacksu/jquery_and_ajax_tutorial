# JQuery and Ajax Tutorial

Hacksu goers: you can follow along here: https://codepen.io/bhollan5/professor/mxvZPg/
Here's a link to the first API we're using: https://yesno.wtf/api
Here's a link to the second API we're using: http://funtranslations.com/api

## Step 1: Wait, what are we doing again?

We're learning JQuery and Ajax!

Ajax is a tool to let us make HTTP requests. We're going to be using it to get information from an API. Basically, APIs let us programatically get data from databases. 

Ajax can be used with vanilla javascript, but it's way easier to use with JQuery, so we're using that. JQuery is an extremely basic Javascript library.

## Step 2: Setting up our document

We're going to be using (Codepen)[http://codepen.io] for this project! Open it up, click `Create` in the upper right hand corner, and click `New Pen`.

In the HTML box, write this for now. I'm not going to go over HTML in this tutorial, so if you don't know what these elements are, feel free to google:

```
<button onclick="getAnswer()">Get a Yes or No Answer</button>

<br><br>
Answer: <span id="answer"></span>
<br>
<img id="myImage" src="">
```

Next, in the JS box, click on the gear icon, click the drop down labeled `Quick Add`, and add Jquery (NOT jquery UI).

## Step 3: Using Jquery to make our first API call

Jquery lets us access elements in our HTML by their `id` attribute more easily, and manipulate it more easily. For example, if we wanted to select the div with the id `answer` and set its inner text to say `Hello World`:

```
// With vanilla JS:
document.getElementById('answer').innerHTML = "Hello World";

// With JQuery:
$('#answer').html('hello world');
```

In the following code, I set up a function that can be called by our button that gets data from the yesno.wtf api and outputs it on our page:

```
function getAnswer() {
  
  console.log("Calling api: ");
  
  // Setting the page to say 'loading' - this will get overwritten when
  // the API is done getting our data.
  $('#answer').text("Loading...");
  $('#myImage').attr('src', '');
  
  // Here's the API call! Note that the function defined here in the .done function
  // is a "callback" function. This means that it won't execute until the API request is complete.
  // Our call back function is passed data, (which we could have named anything, but i chose to call it "data")
  $.ajax('https://yesno.wtf/api').done(function (data) {
    
    console.log("Our response:", data);
    $('#answer').text(data.answer);
    
    // This is JQuery shorthand for changing the 'src' attribute of our img tag
    $("#myImage").attr('src', data.image);
    
  }).fail(function() {
    // This function will be called if the API call fails. 
    // You can test it by changing the ajax URL above to anything that isnt an API.
    $("#answer").text("There was an error!");
  })
  
 
  // Note that the above callback functions will run AFTER any code you put down here!
  // That's how asynchronous functions run - asynchornously!
  
}
```

## Step 4: Our second API call

I'm going to append some stuff into our HTML now, so we can make a second API call! Here's our new, updated HTML:

```
<button onclick="getAnswer()">call function</button>


<br><br>
Answer: <span id="answer"></span>
<br>
<img id="myImage" src="">

<!-- Below is the new stuff -->

<br><br>
<input value="hi" id="myInput"></input>

<button onclick="translateText()">Translate!</button>

<br><br>

<div id="translation"></div>
```

Here's the new JS function we'll be using. I strongly recommend you go to http://funtranslations.com/api and change the URL to the language of your choice!

```
function translateText() {
  var text = $("#myInput").val();
  console.log("Our text:" + text)
  
  $.ajax('https://api.funtranslations.com/translate/leetspeak.json?text='
        + text).done(function (data) {
    console.log(data);
    
    $("#translation").text(data.contents.translated)
  })
  
}
```

