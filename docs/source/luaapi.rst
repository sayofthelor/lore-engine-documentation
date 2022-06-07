Lua Script API
===============
The Lua script API is a relatively simple, but very powerful modding API for Lore Engine.

This page will be updated with pretty much every version of Lore Engine, since both Psych and Lore's documentation is here.

Lua scripts are automatically executed under several conditions for any given mod:

- When a song is loaded, from ``[mod]/data/[song]/script.lua``
- When a stage is loaded, from ``[mod]/stages/[stage].lua``
- All scripts in the ``[mod]/scripts`` folder when any song in the mod is loaded

.. _callbacks:

Callbacks 
----------

**``onCreate()``**

    Called once at the beginning of PlayState's ``create()`` function.

.. note::

    This is before many variables are properly initialized, so anything you set here  in PlayState will likely be overwritten.

**``onCreatePost()``**

    Called once at the end of PlayState's ``create()`` function.

**``onUpdate(elasped)``**

    Called once per frame, at the beginning of PlayState's ``update()`` function. ``elapsed`` is the time since the last frame, in milliseconds.

.. note::

    This is before many variables are properly initialized, so anything you set here in PlayState will likely be overwritten.

**``onUpdatePost(elasped)``**

    Called once per frame, at the end of PlayState's ``update()`` function. ``elapsed`` is the time since the last frame, in milliseconds.

**``onDestroy()``**

    Called once whenever the song fade out is complete for any reason.

**``onBeatHit()``**

    Called once per beat.

**``onStepHit()``**

    Called once per step, four times per beat.

**``onSongStart()``**

    Called when the song starts, and ``Conductor`` time = 0.

**``onEndSong()``**

    Called when the song ends.

    You can return ``Function_Stop`` to stop the song end function from running.

**``onPause()``

    Called before ``PauseSubState`` is entered.

    You can return ``Function_Stop`` to stop the player from pausing the game.

**``onResume()``**

    Called when the song is resumed.

.. note::

    This is not always after the game pauses.

**``onStartCountdown()``**

    Called when the countdown begins.

    You can return ``Function_Stop`` to stop the song from starting.

**``onCountdownTick(tick)``**

    Called every beat while the countdown is running.

.. note::

    Key:

    0 = first beat

    1 = "ready"

    2 = "set"

    3 = "go"
    
    4 = nothing, called at the same time as ``onSongStart``

**``onMoveCamera(char)``**

    Called when the camera is moved. ``char`` can equal ``dad``, ``gf``, or ``boyfriend``.

**``onEvent(name, val1, val2)``**

    Called when an event is triggered. ``name`` is the event name, and ``val1`` and ``val2`` are the 2 values input in the Chart Editor.

**``eventNoteEarlyTrigger(name)``**

    Called to trigger an event earlier than it is put in the Chart Editor.

    To use this you'll need to return the ms value to start early.

    Here's an example:

    .. code-block:: console
        if name == "Kill Henchmen" then
            return 280
        end

**``goodNoteHit(id, direction, noteType, isSustainNote)``**

    Called when a note is hit.

    ``id`` is the note member ID. ``direction`` is the note direction. ``noteType`` is the note type string/tag. ``isSustainNote`` tells you whether or not it is a sustain.\

.. note::
    Direction key (applies to all callbacks where ``direction`` is used):

    0 = left

    1 = down

    2 = up

    3 = right   

**``noteMiss(id, direction, noteType, isSustainNote)``**

    Called when a note is missed, after the miss calculations, if the player lets the note go offscreen.

    Parameters are identical to ``goodNoteHit``.

**``oponnentNoteHit(id, direction, noteType, isSustainNote)``**

    Called when the opponent hits a note.

    Parameters are identical to ``goodNoteHit``.

**``onGhostTap(direction)``**

    Called when the player taps a key and there's no note. Called regardless of whether or not ghost tapping is enabled.


**``noteMissPress(direction)``**

    Called when the player presses a key and there's no note. Called only when ghost tapping is disabled.

**``onKeyPress(direction)``**

    Called when the player presses a key.

**``onKeyRelease(direction)``**

    Called when the player releases a key.

**``onGameOverStart()``**

    Called once ``GameOverSubstate`` is entered.

**``onGameOver()``**

    Called every frame when health is less than or equal to 0.

    You can return ``Function_Stop`` to stop the game over function from running.

**``onGameOverConfirm(retry)``**

    Called when the player confirms the game over screen. ``retry`` is true if the player pressed the retry button intead of ``ESC``.

**``onRecalculateRating()``**

    Called when the rating is recalculated.

    Use ``setRatingPercent`` to set the rating blurb.

    You can return ``Function_Stop`` to stop the function and do your own calculations.

**``onHeadBop()``**

    Called when the head bop animation plays.

    You can return ``Function_Stop`` to stop the animation, and use your own custom scale values, with the variable ``iconSize``.

**``onNextDialogue(line)``**

    Called when the next dialogue line is displayed. ``line`` starts at 1.

**``onSkipDialogue(line)``**

    Called when the player skips a dialogue line with ``ENTER``. ``line`` starts at 1.

**``onTweenCompleted(tag)``**

    Called when a tween completes. ``tag`` is the tag of the tween.

**``onTimerCompleted(tag, loops, loopsLeft)``**

    Called when a timer completes. ``tag`` is the tag of the timer. ``loops`` is the number of times the timer has looped. ``loopsLeft`` is the number of times the timer will loop again.

**``onCheckForAchievement(name)``**

    Called when you want to check for an achievement.

    You can get conditional properties and the achievement name from ``name``, then return ``Function_Continue`` to unlock the achievement.