# Entry 3
##### 2/3/25

## Content 
So as you may know we have this project called the freedom project which is our year long project. We pick a tool that we wanted to use and make a game out of it. So what I decided to pick was kaboom js. I been using this tool by using [kaboom website](https://kaboomjs.com/) in this website you are allowed to see the codes you can use and you can go to the playground which has games and codes for those games. Another thing I used was the [learning log](../tool/learning-log.md) Here you can see all the processes I have done. So before break we had to write a blog in which I explained everything I was going to do during break. Everything I did during break you can see here:
## What I did during the break
So I made a thing where you can talk to people and it changes the character on the screen when you do. The code is here:
````` js
kaboom({
	background: [ 255, 209, 253 ],
})

loadSprite("bean", "/sprites/../person.png")
loadSprite("mark", "/sprites/../women.png")

// Define the dialogue data
const dialogs = [
	[ "bean", "hi my butterfly" ],
	[ "bean", "i love u" ],
	[ "bean", "you love me? pretty baby" ],
	[ "bean", "he did not know how to take care of you..." ],
	[ "mark", "you don't know me ..." ],
	[ "bean", "what! baby???" ],
	[ "mark", "oh...hi " ],
]

let curDialog = 0

// Text bubble
const textbox = add([
	rect(width() - 200, 120, { radius: 32 }),
	anchor("center"),
	pos(center().x, height() - 100),
	outline(4),
])

// Text
const txt = add([
	text("", { size: 32, width: width() - 230, align: "center" }),
	pos(textbox.pos),
	anchor("center"),
	color(0, 0, 0),
])

// Character avatar
const avatar = add([
	sprite("bean"),
	scale(3),
	anchor("center"),
	pos(center().sub(0, 50)),
])

onKeyPress("space", () => {
	// Cycle through the dialogs
	curDialog = (curDialog + 1) % dialogs.length
	updateDialog()
})

// Update the on screen sprite & text
function updateDialog() {

	const [ char, dialog ] = dialogs[curDialog]

	// Use a new sprite component to replace the old one
	avatar.use(sprite(char))
	// Update the dialog text
	txt.text = dialog

}

updateDialog()


`````

![](../tool/women.png)
![](../tool/hi.png)

As you can see above the people are talking to each other.


### Plans
So the firs thing we need to do is combined this with Katherine thing. So we can have a game where you can go through levels and talk to people. After we need to add more levels, make it so wehn you press space you talk to people and esc to leave the talking. These are some of the plans we got and that we still need to work on. 

## Engineering Design Process
The Engineering Design process is the part of the project you are on. So I am currently on the fifth Engineering Design process which is create, so the problem we are fixing is that people are too scared to cook. So maybe they would want to cook online, what we are doing is making a game where people can cook, make their own way of cooking, serving customers and having fun with friends. So far we have made a prototype where my teammate has made the levels and I have made it so you can talk to people. This is our prototype so far, we need to add improvements and add more things to do in the game. therefore the step we are on is the create step which is making a prototype of the game which we made a part of the game so far. 

## Skills 

## Researching


## Communication 





[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)
