# OVC-World-Control
A system of scripts and shaders I have made to be capable of controlling DMX within a world. Screenmapping is a planned feature.
It can also be referred to as an audio-DMX system, it's main thing is mixing the audiolink colors and converting into DMX for the fixtures!
Currently, it supports up to 10 different groups of fixture arrays, up to 20 channels each.

<img width="1107" height="688" alt="image" src="https://github.com/user-attachments/assets/e0c3b2df-9238-46d1-b995-511a3f6b283c" />

It is a bit.. confusing.. But generally, there are three main prefabs for v1.0! 
The control panel prefab holds all of the necessary stuff to run the system. There is also the screen debug prefab that holds the control variable, DMX linear output, and 9 universe gridnode!
Finally, there is a prefab for recording the equivalent DMX for the world! 

Fundale from Stage Flight made a binary gridnode encoder for the world, thanks!
V1.0 introduces world mode swapping, and Metronome controls!
OVCWorldControlPanelV0.5: a control panel! It contains the main scripts the system needs to run.
The metronome is a variable that constantly loops between 0 and 2*pi, controlling all time varying movements.
The texture yeeter is taken from v0.1 and configured for this!
OVC_Variable DMX Manager manages all of the variables that the system uses to synchronize, and to also print out a debug control texture.

The buttons also each have a script on them

<img width="475" height="901" alt="image" src="https://github.com/user-attachments/assets/de54c401-e248-452e-9658-843628524451" />

They work by having the control arrays use an index like an ID. The buttons update the central DMX manager's synced byte value (0-255) index. each script checks if the synced value matches the ID of an array on it (if not, it just skips.), and if it does, it will send it into shader for the dmx generator and also to the manager to convert to the debug texture.
The first four values of the 64 long control array defines the group. 0 - universe offset, 1 - channel offset, 2 - number of fixtures, 3 - channels per fixture
The next 60 are formatted in triplets; Waveform, phaseOffset, and Stagger. In the image, it is formatted to create a ring of flying light fixtures

The DMX generator takes the data in that format, and converts it into a 1-D texture.

There is a gridnode generator that takes that texture and converts it to a 9-universe gridnode.

A separate gridnode generator made by Fundale puts it into MDMX format.

There are few other scripts; tweener readback makes an array of tweeners to move objects, and takes its variables from VRSL's GPU Readback. Instanced Tweenback is an unfinished upgraded version that will be placed on any object you want to move, and it will automatically do readback for at most a dozen channels each.

# Additional Comments
This system is designed to use VRSL's 9 universe mode, and does target the same texture as MIDIDMX's binary to VRSL script. as such, MIDIDMX must be disabled for this controller to pass data to VRSL successfully

My view for this system is to make it easier to run big clubs while using few external programs. This is for people who want to implement it into their worlds.

Please do not replace your VJs and LDs with this system. Multiple people working on a set is greater than the sum of its parts. Doing so will also make me feel bad.
