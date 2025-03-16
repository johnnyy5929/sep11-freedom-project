# Entry 4
##### 3/163/25

## Content 
This is my blog 4. So as you may know we have this project called the Freedom Project which is our year-long project. We picked a tool that we wanted to use and made a game out of it or whatever we wanted. So what I decided to pick was kaboom js. I have been using this tool by using [kaboom website](https://kaboomjs.com/) in this website you are allowed to see the codes you can use and you can go to the playground which has games and codes for those games. Another thing I used was the [learning log](../tool/learning-log.md) Here you can see all the LL I have done. So we had a break and we did some stuff but most of what I have done is for my LL.

## My LL 7-9
So something I have been learning is how to move the character in different ways, and also how to use different keys when trying to play a game. What I mean by this is when you press w you move up or when you press left mouse you attack or something so I been driving deeper into this and learned:
`````js
// Tweeeeeening!

kaboom({
	background: [141, 183, 255],
})

loadSprite("bean", "/sprites/bean.png")

const duration = 1
const easeTypes = Object.keys(easings)
let curEaseType = 0

const bean = add([
	sprite("bean"),
	pos(center()),
	rotate(0),
	anchor("center"),
])

const label = add([
	text(easeTypes[curEaseType], { size: 64 }),
	pos(24, 24),
])

add([
	text("Click anywhere & use arrow keys", { width: width() }),
	anchor("botleft"),
	pos(24, height() - 24),
])

onKeyPress("left", () => {
	curEaseType = curEaseType === 0 ? easeTypes.length - 1 : curEaseType - 1
	label.text = easeTypes[curEaseType]
})

onKeyPress("right", () => {
	curEaseType = (curEaseType + 1) % easeTypes.length
	label.text = easeTypes[curEaseType]
})

let curTween = null

onMousePress(() => {
	const easeType = easeTypes[curEaseType]
	// stop previous lerp, or there will be jittering
	if (curTween) curTween.cancel()
	// start the tween
	curTween = tween(
		// start value (accepts number, Vec2, and Color)
		bean.pos,
		// destination value
		mousePos(),
		// duration (in seconds)
		duration,
		// how value should be updated
		(val) => bean.pos = val,
		// interpolation function (defaults to easings.linear)
		easings[easeType],
	)
})
`````






### Future and MVP

## Engineering Design Process
The Engineering Design process is the part of the project you are on. I am currently on the fifth Engineering Design process which is created, so the problem we are fixing is that people are too scared to cook. So maybe they would want to cook online, what we are doing is making a game where people can cook, make their own way of cooking, serving customers, and having fun with friends. So far we have made a prototype where my teammate has made the levels and I have made it so you can talk to people. This is our prototype so far, we need to make improvements and add more things to do in the game. therefore the step we are on is the create step which is making a prototype of the game which we made a part of the game so far. 

## Skills 

## Researching


## Communication 






[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
