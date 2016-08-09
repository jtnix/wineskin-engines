# wineskin-engines
##### wineskin prepared engines optimized for OS X 10.9 Mavericks, 10.10 Yosemite and 10.11 El Capitan

I've tested these successfully on 10.9.5, 10.10.3 and 10.11.5 specifically with online games Star Wars: The Old Republic, Everquest II and Neverwinter Online. Performance is excellent as of the recent updates to Wine 1.9, especially on post-2012 Mac hardware with AMD or nVidia graphics chips.

*Disclaimer: do not expect success with lower end Apple systems, especially older Air or mini models that rely entirely on Intel integrated graphics.*

Most of these are compiled from the wine-staging releases found here: https://github.com/wine-compholio/wine-staging/releases

## Engine Patches
**Notice** all engines contain the following patches:

* additional thread.c routines that consistently updates a network timing segment used by some programs to authenticate usage or handshake with a server.  Specifically Star Wars: The Old Republic works with these engines *without* needing swtorfix.exe.  Please see https://bugs.winehq.org/show_bug.cgi?id=29168 for more info.
* libpng.16 png library and texture compression library libtxc_dxtn.  You will need to install the additional Wrapper dylib to get support for these updated libraries. (see below)

## Engines
updated Aug 9 2016

* **WS9Wine1.7.44-StagingSWTOR.tar.7z** - contains patches to run SWTOR natively (without swtorfix.exe) and reduce volatility of the map/quest bug.
* **WS9Wine1.9.15-staging-NetworkTiming-10.11-libs.tar.7z** - compiled against native 10.11.5 X11 libs and SDK; only works on El Capitan 10.11.x at this time.
 
### How to use:

* install [Wineskin Winery](http://wineskin.urgesoftware.com/tiki-index.php?page=Downloads)
* Download and copy the engines you wish to use into ~/Library/Application Support/Wineskin/Engines
 * Create a new Wrapper and select the engine
 OR 
 * Use OS X to *Show package contents* of an existing Wineskin wrapper, then:
  * open the *Wineskin* app you see in there
  * click **Advanced**
  * click **Tools** tab at top
  * click *Change Engine Used* button (right-most column, last button)
  * Select the new engine you wish to switch to and click OK
  * wait a few seconds for the new Engine to be installed, then check your Screen Options and winecfg settings (next)
 
 Screen Options
  * *Automatic Screen settings* - the best option, especially if experiencing crashes in SW:TOR on character select screen using 1.7 engine.
  * Check *Use Mac Driver instead of X11* if you are having performance issues with the Wineskin X11 driver (last built in 2012!)  When using this setting it may take several seconds to actually appear launched on the taskbar.
  
 Staging Engine Options
 
 * To enable the high performance graphics features of these engines, you will need to ensure some settings using the **Config Utility (winecfg)** tool from the Tools menu of each Wineskin wrapper you install this engine for.  After you *open winecfg*:
  * Under the **Staging** tab, try *Enable CSMT for better graphic performance* is checked. *note: keep this disabled if having crashes or using lower end Intel HD video chipsets
  * Under **Libraries**, find *wined3d-csmt* and *d3dcompiler_43* and add them both as *native,builtin* libraries (you should also see the rest of the *d3dx9_##* libs in there as well for your normal SWTOR / Everquest II Wine setup)
  * Under **Applications**, I like to keep Windows Version at *Windows XP* or *Windows Vista* mode, whatevs maybe
  * Under **Graphics**, check *Automatically capture the mouse in full-screen windows*  This can keep your mouse from 'jumping' to the center of the screen on every click.  This seems to fix the problem on Everquest II.

 When you are done with settings, exit the *Wineskin* app, back out of your wine Wrapper package and give it a try!

## Additional Wrapper Framework Libraries

To use most of the Engines listed above to their full potential, you will want to copy at least *libpng.16.16.dylib* and *libtxc_dxtn.lib* files from Slice's **WrapperUpdate.zip** (linked below) into your individual Wineskin wrapper's *Contents/Frameworks* folders, where you will see the rest of the standard wrapper .dylib files (these are core libraries used to run your Wineskin wine wrapper.) Not having these libraries installed into your wrappers may result in performance issues like slowness, missing or black textures or outright crashes.

* [WrapperUpdate.zip](https://dl.dropboxusercontent.com/u/17286472/Other/WrapperUpdate-2.zip) - just *libpng16.16.dylib* and *libtxt_dxtn.dylib* for now - compiled for OS X by Slice.

### WrapperDylib installation instructions:

* Show package contents of an existing Wineskin wrapper you have already made, then:
 * Open the **Contents/Frameworks** folder
 * copy the files from the WrapperDylibs.zip file below into the opened **Contents/Frameworks** folder of your Wineskin wrapper
 
To make this process easier to update for multiple Wineskin wrappers you may have out there you can also copy these files into *~/Library/Application Support/Wrapper/Wineskin-2.6.x.app/Contents/Frameworks* and then use the Update Wrapper option of your wrapper's internal Wineskin to refresh your wrapper internal libraries with the additional .dylib files.


## Notes
 * The games this wine engine was designed and tested for are high-end 3D games that use your GPU to it's fullest. With this in mind:
  * This **may not work well or at all on integrated Intel chipsets**, even the HD versions. Give it a try, it might work but if it doesn't, don't be surprised.
  * Use your primary display, always, especially on a laptop. Attempting to run games on a secondary displays will likely results in all kinds of funk, especially with aspect ratio on SWTOR.
  * If you are on a laptop with dual GPUs (most Macbook Pro models have dual GPUs, one for longer battery life and one for high-end graphics needs) be sure to set your System Preferences > Energy Saver > Graphics to Higher Performance, which will force your system to use the high-end GPU on your Macbook.

Any other issues, please open an issue here and I try and help as best as possible.

## Special Thanks
* compholio for the wine-staging releases, without these I would have given up my dream of playing SWTOR on a Mac
* Slice for persistence with continually improving the Staging releases to work best on Mac OS - thanks especially for *libtxc_dxtn* tip off!


