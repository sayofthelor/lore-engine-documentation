Compiling Lore Engine
=====================

.. _haxelib-installation:

Installing Haxe and dependencies
--------------------------------
**To properly compile Lore Engine, you'll need the following.**
`Haxe`_ (Please stop using Haxe 4.1.5.)

`git-scm`_ (https://git-scm.com/downloads)

`VS Community`_ (https://visualstudio.microsoft.com/vs/community/) (Only required on windows and needed for compiling to Windows on Windows, specifically MSVC v142 - VS 2019 C++ x64/x86 build tools and Windows SDK (10.0.17763.0).)

`Xcode`_ (https://apps.apple.com/us/app/xcode/id497799835?mt=12) (Only required on Mac and needed for compiling to Mac on Mac. Please note compiling is not tested on Mac, and I'm not responsible if it doesn't work.)

.. note::

    If you’re running Linux, you'll need some kind of C++ compiler, such as ``g++`` or ``clang``.
    You’ll also need your distro-specific version of ``libluajit-5.1-2`` or the game likely won’t even run.
    I’m not sure about this, but it bugged out for me. If you want to try without installing it, be my guest.
    Please report if it works.

**Once you have everything installed, run the following commands in your console.**
.. code-block:: console

    haxelib install lime
    haxelib install openfl
    haxelib install flixel
    haxelib run lime setup
    lime setup flixel
    lime setup [windows][mac][linux]
    haxelib git polymod https://github.com/larsiusprime/polymod.git
    haxelib git discord_rpc https://github.com/Aidan63/linc_discord-rpc
    haxelib git linc_luajit https://github.com/nebulazorua/linc_luajit
    haxelib install haxeui-core
    haxelib install haxeui-openfl

.. _compiling-game:

Compiling the game:
---------------------
To compile the game, type ``lime test [windows][mac][linux]`` into your terminal or command prompt. To debug your mod, add `-debug` to the end of the command.

The final files go in ``export/[debug/release]/[platform]/bin``.

Happy mod making!

.. _Haxe: https://haxe.org/download/
.. _git-scm: https://git-scm.com/downloads
.. _VS Community: https://visualstudio.microsoft.com/vs/community/
.. _Xcode: https://apps.apple.com/us/app/xcode/id497799835?mt=12