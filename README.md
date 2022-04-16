# Pico-8-for-lovers
A brief introduction to Pico8 edu version.

# What is Pico8?
- Fantasy console representing the 8bit area
- [www.lexaloffle.com](https://www.lexaloffle.com/pico-8.php)

Up until now Pico 8 had to be bought for a small amount of 15.-$. Since April 2022 this is no longer the case. 

Pico8 educational version is now available [here](https://www.pico-8-edu.com/)

# What can I do with Pico8?
- making 8bit games 
- making pixel art (very limited)
- making pixel art maps
- making 8bit music
- make small art projects

# Why I personaly think Pico8 is a great and fun Game engine
- Enforces small projects trough limitations
- Great Community which will love your games, gives feedback and offers help
- It is just fun because it does not want to be you "ready to be used as a professional game engine to kickstart my indie carreer"

# Lets create a small Testproject

## Open the engine for the first time
1. [open the website](https://www.pico-8-edu.com/)
2. click the play button in the middle of the screen
3. now to see what we can do here in this shell like screen type "help" and hit enter
4. As you can see there are some commands listed in the shell: 
<img src="https://user-images.githubusercontent.com/12997366/163626592-ae4d596e-27ab-4633-a8aa-b358ec1ad7d5.png" width="400"/>
5. Type: "install_demos" + Enter in the shell
6. to start one specific of the downloaded games type: "load ./demos/wander.p8" + Enter
7. Now as it promps you with "Loaded ..." hit CTRL + S to start the game
8. Wander arround with the arrows to see what happens

## OK that was fun but lets now programm our own Game
The Game we will programm is very simple and easy to make. It will be similiar to my [satelite-catcher](https://saturn91.dev/play?game=Satelite%20Catcher) game. It will only lack some of its features.

We call the Game coin collect. So as the name suggests we will create a simple caracter which we can move arround the screen and which will collect some coins. Based on that we will increase a simple UI Counter.

### Start a new Project 
1. [reload the page](https://www.pico-8-edu.com/) so that we have a clean version of the fantasy console open
2. click the play button to see the console again
3. hit ESC on your keyboard to get this view:

<img src="https://user-images.githubusercontent.com/12997366/163627201-ddb347b8-a909-4cf7-8e22-a29cd5f00836.png" width="400"/>

4. What you see on the screen is the Coding environement. The red blinking square is your cursor. Try it out by typing some letters. Notice that even if you type non capital letters on your keyboard the are always capital as they get displayed.

### Lets draw our Grafics
1. To draw a character and a coin which we like, we have to select the sprite editor tab. it is the small Cat image near the highlited "()" symbol on top. 
2. Click the Cat symbol on top so it gets highlighted and you see the following screen

<img src="https://user-images.githubusercontent.com/12997366/163627519-59626cc7-923d-4dbc-9215-1065ee2b19ae.png" width="400"/>

3. Now draw your player and a coin as shown bellow: I went for a very simple design
<img src="https://user-images.githubusercontent.com/12997366/163628479-85f8c4f1-f5bc-4b8b-bcb9-f224be844342.png" width="400"/>

### Lets place our objects into the game world
1. change back to the coding environement and start typing:
```lua
--native function! draw stuff
function _draw()
	
	--draw sprite 1 on 60,60
	spr(1,60,60)	
	
	--draw sprite 2 on 20,25
	spr(2,20,25)
end
```
<img src="https://user-images.githubusercontent.com/12997366/163628995-5cb4c32f-f45b-44b7-aef4-5039adaf11fa.png" width="400"/>
2. as you type this first bit of code please note that some lines (beginning with "--") are this purple like color, those are comments and will not run! I only added them to explain the code. Feel free to not paste them in, they are optional. Note that it is a good practice to explain code where it is needed.
3. Actually run your game: as we did before with the demo game: hit CTRL + R to start the game
<img src="https://user-images.githubusercontent.com/12997366/163629239-e28f5d87-491d-44dc-8fbc-1d3359063611.png" width="400"/>
4. Don't worry that we still see some text (you might see different ones) is intended. But at least we can now see our player and our coin, as expected!
5. Lets fix that we do not want to see the text anymore! Pico8 is exactly doing what we told it to do. Drawing this two sprites. But we also have to clear the screen before each draw call! So lets implement that. "cls(1)" will clear the screen with a blue background color.
<img src="https://user-images.githubusercontent.com/12997366/163629789-4e3dfe24-3326-49d7-948d-6f005285f3d1.png" width="400"/>
6. Lets play the game again and check with CTRL + R
<img src="https://user-images.githubusercontent.com/12997366/163630038-13caf29d-2df3-47f9-88f8-88c03454a8dd.png" width="400"/>
7. Ok that is more like it :D

### Variables
If we want to change something e.g. the position of the player we can not simply draw the player at a static position like 60 and 60... So we need a value there which we can change once the input suggest it. So let me introduce variables. Variables are basically container for changable values. For better readability we can give them names. So lets create a variable player_x and one player_y:

```lua
player_x = 60
player_y = 60

//also change the old player code spr(1,60,60) to:
--draw player
spr(1,player_x,player_y)	
```
<img src="https://user-images.githubusercontent.com/12997366/163632234-93683055-18cc-4e33-86d2-da788fa720bb.png" width="400"/>

if you check the current state now, you should get exactly the same result as before - the player gets drawn in the middle


### Player Input and Movement
Pico 8 has a very limited Input system. Like the NES System at its time it supports 8 Buttons: for direction inputs (left, up, right, down), two interactions (A+B or in Pico language X+O or X+C) and start (Enter) and select (Esc). The later two are reserved for pausing the game and interact with the engine itself. 
The code doing this is the following:
```lua
btn(⬆️)	//arrow key up
btn(⬇️) //arrow key down
btn(➡️) //arrow key right
btn(⬅️) //arrow key left
btn(❎) //x button
btn(🅾️) //o or c button
```
To actually update our player we need to introduce a new function the "_update" function. Code in the update function gets called 30 times per second and will be used to actually change stuff in our game e.g. moving the player. So lets create that function

1. create the update function 
```lua
function _update()
	
end
```
2. the "if" statement. As the english term "if" suggest we want to move the player "up" (negativ y) if the "up" btn is pressed. So lets code that
```lua
function _update()
	if btn(⬆️) then
		player_y -= 1
	end

	if btn(⬇️) then
		player_y += 1
	end

	if btn(⬅️) then
		player_x -= 1
	end

	if btn(➡️) then
		player_x += 1
	end
end
```
<img src="https://user-images.githubusercontent.com/12997366/163632419-269f6bdd-067a-4847-8ad7-108a1d777c04.png" width="400"/>
3. now lets test if we can move our player
4. Did it work? if not check if your code is exactly the same as bellow:

```lua

player_x = 60
player_y = 60

function _update()
	if btn(⬆️) then
		player_y -= 1
	end
	
	if btn(⬇️) then
		player_y += 1
	end
	
	if btn(⬅️) then
		player_x -= 1
	end
	
	if btn(➡️) then
		player_x += 1
	end
end

function _draw()
	cls(1) //clear screen grey
	
	--draw player
	spr(1,player_x,player_y)	
	
	--draw sprite 2 on 20,25
	spr(2,20,25)
end
```

### Now lets get the coin :D
1. We need to be able to tell where that coin is, so lets make two variables coin_x and coin_y which give the position of the coin. Can you do it yourself?
<details>
<summary>Solution</summary>
  
```lua
--variables
player_x = 60
player_y = 60

coin_x = 20
coin_y = 35

--native function update stuff
function _update()
	if btn(⬆️) then
		player_y -= 1
	end
	
	if btn(⬇️) then
		player_y += 1
	end
	
	if btn(⬅️) then
		player_x -= 1
	end
	
	if btn(➡️) then
		player_x += 1
	end
end

--native function! draw stuff
function _draw()
	cls(1) //clear screen grey
	
	--draw player
	spr(1,player_x,player_y)	
	
	--draw sprite 2 on 20,25
	spr(2,coin_x,coin_y)
end
```
</details>

3. now we need to check if the player is on top of the coin and move it to a different position e.g. 60,60. 
4. We could just check if the position of the player is the same as the one from the coin.
5. Hint "if coin_x == player_x and coin_y == player_y then ..." might be helpfull, but where to put it?

<details>
<summary>Solution</summary>
!!Spoiler!! this isn't optimal...  

```lua
--variables
player_x = 60
player_y = 60

coin_x = 20
coin_y = 35

--native function update stuff
function _update()
	--player movement
	if btn(⬆️) then
		player_y -= 1
	end
	
	if btn(⬇️) then
		player_y += 1
	end
	
	if btn(⬅️) then
		player_x -= 1
	end
	
	if btn(➡️) then
		player_x += 1
	end
	
	--check for coin
	if player_x == coin_x and player_y == coin_y then
		coin_x = 60
		coin_y = 60
	end
end

--native function! draw stuff
function _draw()
	cls(1) //clear screen grey
	
	--draw player
	spr(1,player_x,player_y)	
	
	--draw sprite 2 on 20,25
	spr(2,coin_x,coin_y)
end
```
</details>

But how to improve, we do not want the player to be at the exactly same position but to overlap the coin. So lets do that.

### Collision
1. lets create our own function which we call player_on_coin. This function will be a sensor which checks if the player is on top of the coin each time the update function gets called. If the player is on top it will answer with "yes" (or true in programming language) else with "no" (or false)

```lua
function player_on_coin()
   if player_x >= coin_x - 8 and
      player_x <= coin_x + 8 and
      player_y >= coin_y - 8 and
      player_y <= coin_y + 8 then
   	return true
   else 
   	return false
   end
end
```
So instead of our if player_x == coin_x and so on in update we can now use this function. Can you find out how?

<details>
<summary>Solution</summary>

```lua
--variables
player_x = 60
player_y = 60

coin_x = 20
coin_y = 35

--native function update stuff
function _update()
	--player movement
	if btn(⬆️) then
		player_y -= 1
	end
	
	if btn(⬇️) then
		player_y += 1
	end
	
	if btn(⬅️) then
		player_x -= 1
	end
	
	if btn(➡️) then
		player_x += 1
	end
	
	--check for coin
	if player_on_coin() then
		coin_x = 60
		coin_y = 60
	end
end

--native function! draw stuff
function _draw()
	cls(1) //clear screen grey
	
	--draw player
	spr(1,player_x,player_y)	
	
	--draw sprite 2 on 20,25
	spr(2,coin_x,coin_y)
end

function player_on_coin()
   if player_x >= coin_x - 8 and
      player_x <= coin_x + 8 and
      player_y >= coin_y - 8 and
      player_y <= coin_y + 8 then
   	return true
   else 
   	return false
   end
end
```
</details>

### random positioning of the coin
Ok so the basics are working. You could now define a hundert different positions within the code and we would be finished :D but the game would always be the same... boring! Also it would be a lot of work. We can do better!
Lets look at the "rnd" function. A lot of programming languages provide some kind of random functions to generate random numbers. Our rnd() function will generate a number from 0..1 (excluding one). We can test this in the Pico 8 console. 
	
1. hit ESC to go back to the console
2. type "print(rnd())" and hit enter
3. repeat some time (you can get the last command you typed by pressing the "up" arrow if you are in the console)
	
<img src="https://user-images.githubusercontent.com/12997366/163667187-eda3f88c-7513-48df-842e-21114dc53a41.png" width="400"/>

4. What you get is some random numbers between 0 and 1 (which will never be 1!). Please also note that I already introduced you to the print function :D we will come back to that later.
5. So how can we make use of this to implement this in our game?
- the screen in Pico8 is 128 x 128 pixels wide.
- a sprite in Pico 8 (like our Coin) is 8 pixels in x and y coordinates
- a spr(...) function draws the sprites upper left corner on the postion we give to it...
- so we need for both coordinates a value from (0-120)
- how could we do this using this rnd() function? Maybe already within a seperat function "new_coin_pos()"?

<details>
<summary>Solution</summary>

```lua
function new_coin_pos()
	coin_x = rnd() * 120
	coin_y = rnd() * 120
end
```
<img src="https://user-images.githubusercontent.com/12997366/163667444-18ec4b9d-3e01-4d46-a44e-b5aaf7d56c42.png" width="400"/>
</details>

We can use this function now within our code which results in:

```lua
--variables
player_x = 60
player_y = 60

coin_x = 20
coin_y = 35

--native function update stuff
function _update()
	--player movement
	if btn(⬆️) then
		player_y -= 1
	end
	
	if btn(⬇️) then
		player_y += 1
	end
	
	if btn(⬅️) then
		player_x -= 1
	end
	
	if btn(➡️) then
		player_x += 1
	end
	
	--check for coin
	if player_on_coin() then
		new_coin_pos()
	end
end

--native function! draw stuff
function _draw()
	cls(1) //clear screen grey
	
	--draw player
	spr(1,player_x,player_y)	
	
	--draw sprite 2 on 20,25
	spr(2,coin_x,coin_y)
end

function player_on_coin()
   if player_x >= coin_x - 8 and
      player_x <= coin_x + 8 and
      player_y >= coin_y - 8 and
      player_y <= coin_y + 8 then
   	return true
   else 
   	return false
   end
end

function new_coin_pos()
	coin_x = rnd() * 120
	coin_y = rnd() * 120
end
```

Now as we have this new function why should we not also place the coin at a random position right at the beginning? Let me introduce you to an other not yet explained native pico8 function: _init. This function will get called first before all other code is run. Lets show this to you by actually using it.

Lets also for better readability set the default values of the coin_x and y to 0, just to initialize the variables.
```lua
coin_x = 0
coin_y = 0

--native function, runs once at start
function _init()
	new_coin_pos()	
end
```

Make sure to test that each time you press CTRL + R the coin is in a different location as the game starts.

### Game boring - need score!
Next thing on our todo list is to show a score which we increase each time the player collects a coin. Lets do that using the print function which we already used in the console.

The print function allows you to display text on screen. 

```lua
print(text, xPos, yPos, text-color) //not functional code just the explenation ;-) 

--print score (functional code)
score = 0

print("score: "..score, 2, 2, 7) //print "score: 0" 2px down and 2px right from the top right screen in color 7 (white)		       
```

So our next exercise includes several steps:
1. create a variable for score
2. increase the score if a coin is collected
3. display the text "score: " and then the current score as a number
		       
Try it yourself:

<details>
<summary>Solution</summary>

```lua
--variables
player_x = 60
player_y = 60

coin_x = 0
coin_y = 0

score = 0

--native function 1call at start
function _init()
	new_coin_pos()	
end

--native function update stuff
function _update()
	--player movement
	if btn(⬆️) then
		player_y -= 1
	end
	
	if btn(⬇️) then
		player_y += 1
	end
	
	if btn(⬅️) then
		player_x -= 1
	end
	
	if btn(➡️) then
		player_x += 1
	end
	
	--check for coin
	if player_on_coin() then
		score += 1
		new_coin_pos()
	end
end

--native function! draw stuff
function _draw()
	cls(1) //clear screen grey
	
	print("score: "..score, 2, 2, 7)
	
	--draw player
	spr(1,player_x,player_y)	
	
	--draw sprite 2 on 20,25
	spr(2,coin_x,coin_y)
end

function player_on_coin()
   if player_x >= coin_x - 8 and
      player_x <= coin_x + 8 and
      player_y >= coin_y - 8 and
      player_y <= coin_y + 8 then
   	return true
   else 
   	return false
   end
end

function new_coin_pos()
	coin_x = rnd() * 120
	coin_y = rnd() * 120
end
```
</details>		       

the expected result:

<img src="https://user-images.githubusercontent.com/12997366/163673012-38028bf7-5fc6-4158-b8e3-ce745ba39d56.png" width="400"/>

### Ok we need more fun lets add an sound effect on coin collect
Pico 8 offers an integrated sound editor which is fairly easy. It really is, you will see when you try out some videos about it on youtube [e.g. this](https://www.youtube.com/watch?v=nwFcitLtCsA&list=PLur95ujyAigsqZR1aNTrVGAvXD7EqywdS). for now, lets create one simple sound effect for the collect. In the Pico8 edu version click on the reversed play button icon in the top right.
	
<img src="https://user-images.githubusercontent.com/12997366/163673104-a358b318-674f-4cb5-95e7-96309a1a4e2c.png" width="400"/>

By clicking and drawing into the upper blackspace on the side you can "draw" your sound effect like this:

<img src="https://user-images.githubusercontent.com/12997366/163673144-0e0d1d38-2f58-4695-8680-f00919cda9f6.png" width="400"/>

Note that this is the "00" sfx and that you can create many more by clicking on the pink arrows to the right.

To actually test the sound you just drew: hit space on your keyboard. Then adjust it to your likeing.

To play the sound in code, you can use the sfx(0) function. this will play the sfx at position 00 (which we just created) once.

Any Ideas yet where to do that in the code?
<details>
<summary>Solution</summary>
	
```lua
--variables
player_x = 60
player_y = 60

coin_x = 0
coin_y = 0

score = 0

--native function 1call at start
function _init()
	new_coin_pos()	
end

--native function update stuff
function _update()
	--player movement
	if btn(⬆️) then
		player_y -= 1
	end
	
	if btn(⬇️) then
		player_y += 1
	end
	
	if btn(⬅️) then
		player_x -= 1
	end
	
	if btn(➡️) then
		player_x += 1
	end
	
	--check for coin
	if player_on_coin() then
		score += 1
		new_coin_pos()
		sfx(0)
	end
end

--native function! draw stuff
function _draw()
	cls(1) //clear screen grey
	
	print("score: "..score, 2, 2, 7)
	
	--draw player
	spr(1,player_x,player_y)	
	
	--draw sprite 2 on 20,25
	spr(2,coin_x,coin_y)
end

function player_on_coin()
   if player_x >= coin_x - 8 and
      player_x <= coin_x + 8 and
      player_y >= coin_y - 8 and
      player_y <= coin_y + 8 then
   	return true
   else 
   	return false
   end
end

function new_coin_pos()
	coin_x = rnd() * 120
	coin_y = rnd() * 120
end
```
		       
</details>

We wont write our ownmusic in this tutorial, as it takes way to long. I highly suggest to watch some youtube videos on that topic ;-). In short you create music similiar as we did with our sound effect and then play it in a loop with music(0) (it is a little bit more to do... but pretty much this).
	
### Other pico 8 features to look into
- Map

### pico 8 cheat set
Gives you an overview about most functions pico 8 provides
![PICO-8_CheatSheet](https://user-images.githubusercontent.com/12997366/163673455-248991d0-5bde-495e-affa-ddcbb71e42d6.png)

### buying pico 8
I highly recommend spending the 15$ on Pico 8 full version anyway as it gives you a lot more possibility to export your game. e.g. as Web build, Windows, Linux or Max build. And it also shows some love to the developper which did a really good job!

Keep in mind that you only pay once and you have a life long access to the download link to download ALL existing OS versions!

Also you get Splore, the possibility to download and play the newest games for Pico8 which where released on the pico87 website.

<img src="https://user-images.githubusercontent.com/12997366/163673586-bf927bf3-a0f4-4727-94cf-5430b0f5b636.png" width="400"/>

### pico 8 on a raspberry pi / Gameboy
Pico 8 runs fantasticly on any Raspberry PI which makes Raspberry Pi almost to an Operating system which allows you to make games on very minimalistic machines. This could be a good opertunity to give Children a Computer they can play games on and learn programming in a safe environement. (other than for downloading games you dont need Internet ;-).

I have a neet little Gameboy mock which runs Pico8 this allows me to play my own Games on a original feeling Gameboy :D I love that!
