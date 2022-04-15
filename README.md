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
3. now to see what we can do here in this shell like screen type ```help``` and hit enter
4. As you can see there are some commands listed in the shell: 
<img src="https://user-images.githubusercontent.com/12997366/163626592-ae4d596e-27ab-4633-a8aa-b358ec1ad7d5.png" width="400"/>
5. Type: ```install_demos``` + Enter in the shell
6. to start one specific of the downloaded games type: ```load ./demos/wander.p8``` + Enter
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

## Lets staticaly place our objects into the game world
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
