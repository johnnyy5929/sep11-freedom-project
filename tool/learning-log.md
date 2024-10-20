# Tool Learning Log

## Tool: **Kaboom**

## Project: **Cooking game**

---

### 10/6/24:
Using kaboom for the first time,
So to start off I had to learn how to instead it first;
The code to instead kaboom is

`````
<script type="module">

// import kaboom.js
import kaboom from "https://unpkg.com/kaboom@3000.0.1/dist/kaboom.mjs";

// initialize kaboom context
kaboom();

// add a piece of text at position (120, 80)
add([
    text("hello"),
    pos(120, 80),
]);

</script>
`````
This is one way of insteading, if you instead this way there will be text and you can change teh sides of the background. 
![hi](Screenshot_6-10-2024_15712_jsbin.com.jpeg)

The other way of insteading it is the same but there isn't any words. 
````
<script src="https://unpkg.com/kaboom@3000.0.1/dist/kaboom.js"></script>

<script>
    kaboom();
</script>
````
![hi](Screenshot_6-10-2024_15134_jsbin.com.jpeg)

So after doing m,y research on Kaboom I learned many things and combined them. So somethings that I added to this is sprite which is the character of this game. Another thing I added was const which makes everything the same. another example of this is `````js const Speed =320````` 


<!-- 
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
