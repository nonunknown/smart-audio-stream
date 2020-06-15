# Smart Audio Stream

* Godot 3.2

## Description

Currently its only implemented for **AudioStreamPlayer3D**
but you can easily convert it just by changing:

```
extends AudioStreamPlayer3D # change 3D to 2D
```

## What this plugin does?

Simple, think a jumping audio with a duration of 1 sec but your player takes only .5s to
do jumps, using the normal AudioStream it will cut the currently playing audio and start it again, with this plugin it knows if a sound is already playing and instead of cut and play again
it will set another stream to play so you will hear the sounds without cutting them.

## How to use?

* Activate plugin
* Create a Node searching by SmartAudioStream3D
* set the initial amount of streams
* set the array of audio samples (.wav or .ogg)
* them with a reference to this node call `$SmartStream.play_audio(sample_index)`
* Tips:
``` 
# you can use a enum for easily refer the audio you want
# suppose you have This tree
# - KinematicBody (this script is here)
#  L SmartAudioStream3D
#  L OtherNodes
# suppose too you have two audios on SmartAudio samples exported var [jump,talk]
# use this:

enum AUDIO {JUMP, TALK}

func _ready():
	$SmartAudioStream3D.play_audio(AUDIO.TALK)

```

## How does it works behind the scenes?
The smartAudio stream class has:

* initial_stream - (how many AudioStreamPlayer3D will be generated at _ready)
* samples - Audio Files Array
* play_audio(sample_idx) - play the audio according to samples array
* the following are private:
	- _create_stream (generate streams to avoid audio cutting)
	- _play_last_stream (when all audios from array are playing it will generate a new stream and play the audio on it)


