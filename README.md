# wineskin-engines
wineskin engines optimized for OS X 10.9 and beyond

I've tested these successfully on 10.9.5 and 10.10.3 with online games like Star Wars: The Old Republic, Everquest II and Neverwinter Online and performance is quite good, especially on post-2012 Mac hardware.

Most of these are compiled from the wine-staging releases found here: https://github.com/wine-compholio/wine-staging/releases

## Engines

* WS9Wine1.7.44-StagingSWTOR.tar.7z - contains patches to run SWTOR natively (without swtorfix.exe) and reduce volatility of the map/quest bug.
 * also contains the newer libpng.16 and libtxc_dxtn support.  You will need to install the additional Wrapper dylib below to get the new libpng and libtxc_dxtn support.
 
### How to use:

* install [Wineskin Winery](http://wineskin.urgesoftware.com/tiki-index.php?page=Downloads)
* Download and copy the engines you wish to use into ~/Library/Application Support/Wineskin/Engines
* Create a new Wrapper and select the engine
 * OR 
* Show package contents of an existing Wineskin wrapper you have already made, then:
 * open the *Wineskin* app you see in there
 * click **Advanced**
 * click **Tools** tab at top
 * click *Change Engine Used* button (right-most column, last button)
 * Select the new engine you wish to switch to and click OK
 * wait a few seconds for the new Engine to be installed, then check your Screen Options and winecfg settings (next)
 
 Other Wineskin settings to enable:
 
 * Screen Options
  * always choose *Automatic Screen settings* - trying to use any desktop Override has always resulted in crash before the character selection screen in SWTOR
  * Try *Use Mac Driver instead of X11* checked (it may take up to 20 seconds to actually launch on your first load, so wait a bit before clicking again.) If you are having serious performance issues, try again with Mac Driver off, but it should work better enabled on newer Mac hardware.
 * To enable the high performance graphics features of these engines, you will need to ensure some settings using the **Config Utility (winecfg)** tool from the Tools menu of each Wineskin wrapper you install this engine for.  After you *open winecfg*:
  * Under the **Staging** tab, make sure *Enable CSMT for better graphic performance* is checked.
  * Under **Libraries**, find *wined3d-csmt* and *d3dcompiler_43* and add them both as *native,builtin* libraries (you should also see the rest of the *d3dx9_##* libs in there as well for your normal SWTOR / Everquest II Wine setup)
  * Under **Applications**, I like to keep Windows Version at *Windows XP* or *Windows Vista* mode - YMMV
  * Under **Graphics**, make sure *Automatically capture the mouse in full-screen windows* is checked.  This will keep your mouse from 'jumping' to the center of the screen on every click which has all kinds of bad effects on gameplay.  This still isn't perfect on SWTOR but seems to fix the problem on Everquest II.

 When you are done with settings, exit the *Wineskin* app, back out of your wine Wrapper package and give it a try!

## Additional Wrapper Framework Libraries

To use most of the Engines listed above to their full potential, you will want to copy at least *libpng.16.16.dylib* and *libtxc_dxtn.lib* files from Slice's **WrapperUpdate.zip** (linked below) into your individual Wineskin wrapper's *Contents/Frameworks* folders, where you will see the rest of the standard wrapper .dylib files (these are core libraries used to run your Wineskin wine wrapper.) Not having these libraries installed into your wrappers may result in performance issues like slowness, missing or black textures or outright crashes.

* [WrapperUpdate.zip](https://dl.dropboxusercontent.com/u/17286472/Other/WrapperUpdate-2.zip) - just *libpng16.16.dylib* and *libtxt_dxtn.dylib* for now - compiled for OS X by Slice.

### WrapperDylib installation instructions:

* Show package contents of an existing Wineskin wrapper you have already made, then:
 * Open the **Contents/Frameworks** folder
 * copy the files from the WrapperDylibs.zip file below into the opened **Contents/Frameworks** folder of your Wineskin wrapper
 
To make this process easier to update for multiple Wineskin wrappers you may have out there you can also copy these files into *~/Library/Application Support/Wrapper/Wineskin-2.6.0.app/Contents/Frameworks* and then use the Update Wrapper option of your wrapper's internal Wineskin to refresh your wrapper internal libraries with the additional .dylib files.


## Notes
 * The games this wine engine was designed and tested for are high-end 3D games that use your GPU to it's fullest. With this in mind:
  * Do not expect it to work well or at all on integrated Intel chipsets, even the HD versions - it might work but if it doesn't, don't be surprised.
  * Use your primary display, always. Do not attempt to use on an external or secondary screen, I've never had great success with this, especially with aspect ratio issues in SWTOR.
  * If you are on a laptop with dual GPUs (most Macbook Pro models have dual GPUs, one for longer battery life and one for high-end graphics needs) be sure to set your System Preferences > Energy Saver > Graphics to Higher Performance, which will force your system to use the high-end GPU on your Macbook.

Any other issues, please file a report here and I will update this readme with more info as I have it.


## Special Thanks
* compholio for the wine-staging releases, without these I would have given up my dream of playing SWTOR on a Mac
* Slice for persistence with continually improving the Staging releases to work best on Mac OS - thanks especially for *libtxc_dxtn* tip off!


