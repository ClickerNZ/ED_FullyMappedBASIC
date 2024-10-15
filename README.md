# ED_FullyMappedBASIC

Basic WARTHOG TARGET script with no smarts

### PURPOSE

The purpose of this script is to give people who may be new to Elite Dangerous and have a Thrustmaster WARTHOG Joystick and Throttle, a starting point should they want to get into TARGET scripting now, or maybe in the future.  

### REQUIREMENTS

To use this script you will need a THRUSTMASTER WARTHOG Throttle and a Thrustmaster F16 or F18 Flight stick connected to a Warthog or AVA base. Rudder pedals are not required, but recommended.  
  
Also, you will need the latest firmware for these devices and the very latest version of TARGET software.  
Whilst the latest version of TARGET software now supports 64 DX inputs, sadly, at time of writing, Elite: Dangerous still only supports 32 DX inputs.  

### ZIP PACKAGE  

The zip file contains the following:  
- ED_FullyMappedBASIC.tmc main script file which contains all the configuration axes and button mapping  
- ED_GameBindings.ttm script support file which contains definitions of various keypresses and DX inputs
- This readme.md file  
- A Map Files folder which contains  
  * 2x Image files for each of the Throttle and Joystick
  * 1x showing the button and switch actions for each (helps with game usage while you are coming up to speed)  
  * 1x showing the button and switch names for each (helps if/when you need to dig under the covers and take on some scripting)  
- A Bind Files folder which contains
  * Binds files supporting Odessey and Horizons as well as the earlier legacy versions  

### INSTALLATION

If you have just bought a Thrustmaster WARTHOG or AVA Throttle and Joystick, you can be up a running very quickly.  
You will, however need to spend some time becoming accustomed to what the buttons and switches all do.  

The \'Map Files\' folder contains some images which should help with this, so I recommend you print these out.

- Unzip the package to a local drive/folder of your choice.
- I suggest creating c:\Thrustmaster and copying into there.
- Create a backup of your current bind files which can be found at...
	
	C:\Users\\<username\>\AppData\Local\Frontier Developments\Elite Dangerous\Options\Bindings  
	(change \<username\> in the above path to your Windows username)
 
- Copy the contents of the Bind file folder into the above bindings folder.

### USAGE

- Open the TARGETScriptEditor program.  
- Open ED_FullyMappedBASIC.tmc  
- Click 'compile'  
- If you get no errors, hit 'run'  

If you get a syntax error, try to resolve, save and click 'compile'.  
Repeat as necessary.  

Once the script is running the script editor console will show 'main returned 0' if everything is ok.  

If the script aborts, it might mean you do not have the required controllers connected.  
Read the abort error message carefully.  
If you get stuck, post a query in the Elite Dangerous forums.  

Assuming the script compiled and runs fine, start Elite Dangerous.  

> NOTE: You need to always run the script before starting the game  

### SETTING SCRIPT BINDS IN  GAME

Once the game is running, hit escape key and choose OPTIONS then CONTROLS then each of the GENERAL, SHIP and SRV.  
Set the PRESET for each of these to 'Clicker-FullyMappedBASIC' and hit APPLY for each one then go flying!  

But, what if I want to change some of the actions bound to a button or switch?  
What if I want to change them all?  

Read on.  

### CHANGING BINDS  

My script uses 36 seperate pre-defined actions.  

---  

<figure>  
    <img src="/MapFiles/ED_JoystickChart-BASIC-ACTIONS.png" width="640">      
</figure>  

<center>ED_JoystickChart - ACTIONS</center>  

---  

<figure>
    <img src="/MapFiles/ED_ThrottleChart-BASIC-ACTIONS.png" width="640">
    <figcaption>          ED_ThrottleChart - ACTIONS</figcaption>
</figure>  

---  

If you are happy to go with these then things are pretty simple, you are done.  
However, if you want to change what the buttons and switches do, then there are several ways to accomplish this.  

This is where things might get a bit complicated, so you will need a healthy dose of patience if you want to change a lot of the pre-configured binds in this package.  

No doubt if you have been playing Elite Dangerous for a while you will already have your own preferred binds.  
If you want to use this script but want to use your own binds then this is what you can do...  

You have 2 options here...  

#### OPTION 1 - For a lot or most of the BINDS

This option has a hard limit (32) on the number of buttons and switches you can map.  

- Comment out the 'MapAllKeys()' call on line 72 in ED_FullyMappedBASIC.tmc file by adding 2x slashes at the beginning of the line (ie. //)
- Compile and run the script.
- Run Elite Dangerous
- Go to OPTIONS | CONTROLS
- Select GENERAL, SHIP and SRV one by one and go through each line and press the button or switch you want to use.  

This method will allow you to assign a JOY# (ie DX#) to each of the actions up to JOY32.  
Anything after 32 you will need to assign a keypress.  
If you don't want or need to use a joystick or throttle button to send these keypresses, you are done!  

Otherwise, note the keypresses down if you want to use with an otherwise unmapped joystick or throttle button.  
Edit ED_FullyMappedBASIC.tmc using notepad (I prefer and use Notepad++). 
Directly after line 72 that you commented out earlier start entering MapKey definitions for only those buttons you want to map a keypress to.  

The syntax is: 
> MapKey(&device, button name, PULSE+keypress);
>
> device = either MyJoystick or MyThrottle  
> button name = the name of the button on the device  
> PULSE+ = Pulse sends a KEYDOWN and then KEYUP signal to the game.  
> - Use PULSE for binds with a TOGGLE setting.  
> - Don't use PULSE for binds with a HOLD setting. Simply HOLD the button on the device for these like you would a keyboard key.
>   
> keypress = key you want to use. Example 'a' (include the single quotees)  

EXAMPLE:  
> MapKey(&MyThrottle, BSF, PULSE+'a');
>    
> device = MyThrottle  
> button name = BSF = Boat Switch Forward (Boat Switch is the red thumb switch on the Throttle arm).  
> keypress = a  
   
ie. sends an 'a' keypress to the game when you press the red Boat Switch on the throttle forward.  

Check out my image files within the 'Map Files' folder for all the button and switch names used by TARGET script.  

---  

<figure>  
    <img src="/MapFiles/Warthog-Joystick-Chart-BUTTONS.png" width="640">  
    <centre><figcaption>ED_JoystickChart - BUTTON NAMES</figcaption></centre>
</figure>  

---  

<figure>
    <img src="/MapFiles/Warthog-Throttle-Chart-BUTTONS.png" width="640">
    <figcaption>          ED_ThrottleChart - BUTTON NAMES</figcaption>
</figure>  

---  



#### OPTION 2 - Best for a dozen or so BIND changes  

This is a better option if there's not too many BINDS you want to change.

- Re-instate your saved bind files.  
- Run the game without running this script and take note of all your preferred bindings via OPTIONS | CONTROLS | etc.  
- Note each key including modifiers (ie Left Shift + key) and each JOY#.  
  
- Open the ED_GameBindings.ttm file using notepad (or Notepad++)  
- Go through each of the defines and change the USB code for your preferred key or key combo.  

> At the very bottom of the file there is a USB code table for reference.

  
As mentioned DX# numbers show up as JOY# within the bind process in game.  
  
Simply change the USB code to the DX#.  
Example, if you use JOY3 for a button instead of a keypress, change the define for that button to DX3  

> :warning: **Warning:** 
You can only assign a maximum of 32 DX numbers. This is a limitation of Elite Dangerous and not TARGET.  

  
### CHANGE BUTTON ACTIONS  
  
Edit the ED_FullyMappedBASIC.tmc file using notepad (or Notepad++)  
Starting on line 111 is the Mapkey assignment subroutine which is called from Line 72 of the script.  
  
So long as you are happy with my preconfigured actions, simply and swap the action part between buttons.  
  
EXAMPLE:  
You swap the action of these two buttons  
  
> MapKey(&MyJoystick, H1L, PULSE+LandingGear);  // Press Hat 1 Left (H1L) to send 'L'  
> MapKey(&MyJoystick, H1R, PULSE+ShipLights);  // Press Hat 1 Right (H1R) to send 'insert' key  

  
By making this change 

> MapKey(&MyJoystick, H1L, PULSE+ShipLights);  // send 'insert' key
> MapKey(&MyJoystick, H1R, PULSE+LandingGear);  // send 'L' key  
		
NOTE: It's always a good idea to update the comments at the end of the line to reflect what the statement does.
  
EXAMPLE:  
You can map more than one button to do the same action.  

> MapKey(&MyJoystick, H1L, PULSE+ShipLights);  // 'insert' key  
> MapKey(&MyJoystick, H1R, PULSE+ShipLights);  // 'insert' key  
  
This results in both buttons (H1L and H1R) sending the same action to the game.  
  
Or, take a look in the ED_GameBindings.ttm file and pick a defined action of an unused (commented) action.  
Uncomment the unused action and use the define name in the action part of the MapKey statement for the button you want to change.  
  
EXAMPLE:  
In ED_GameBindings.ttm file, uncomment the unused action definitions  
> //  define RollLeft  'W'  // LSHIFT+W  
> //  define RollRight 'S'  // LSHIFT+S  
  
So they are now  
> define RollLeft  'W'  // LSHIFT+W  
> define RollRight 'S'  // LSHIFT+S  
  
'RollLeft' and 'RollRight' may now be used in our script.  
  
...next...  
Change the action part of the MapKey statements to match the action definition  
> MapKey(&MyJoystick, H1L, PULSE+RollLeft);    // LSHIFT+W  
> MapKey(&MyJoystick, H1R, PULSE+RollRighht);  // LSHIFT+S  
    
When testing this you might find the Ship Roll is not as smooth as you'd like.  
Try removing PULSE+.  
>  MapKey(&MyJoystick, H1L, RollLeft);   // LSHIFT+W  
> MapKey(&MyJoystick, H1R, RollRighht);  // LSHIFT+S  
  
The ship should now roll smoothly for as long as you are holding the button.  
  
### SUPPORT  
  
If you get stuck or just want to understand more, post a question in the forum, or PM me.  
  
Cheers  
Clicker  
