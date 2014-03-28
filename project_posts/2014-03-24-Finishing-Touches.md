## Effects Processing
Web Audio API provides a reasonable set of tools to be used for effects processing. Nodes such as Delay, Convolver and Dynamics Compressor are more than enough for this scenario. I used the delay effect mostly on the main sample with the delay-time set to a eighth-note to give a little bit of depth to the sound. I used the convolver node as a reverb effect to glue the whole beat together. Finally, I used the compressor to control the levels and limit the gain to prevent clipping.

## Recorder.js
Now that we genereted our beats, It would be trivial if we did not have a way to record and store them. It is quiet unlikely that a beat will be generated a second time, so it would be nice to have a recorder and a way to save the recorded file. [Recorder.js](https://github.com/mattdiamond/Recorderjs) does exactly the same. The library uses Web Audio API's `ScriptProccesorNode` in conjunction with [Web Workers](http://www.w3.org/TR/workers/) and lets you export a wav file of the recording.

## The Interface
Although the inteface design is not the main goal of this project, it is important to have a basic and simple GUI. I decided to use four big buttons for the main functions which are New Sounds, New Pattern, Play/Pause and Record. On the bottom section, we have loading indicators which use [Spin.js](http://fgnass.github.io/spin.js/) and finally there will be links to original sounds used on the beat as well as mute buttons for each sound.

## Let there be Tumblr!

In the first post, I talked a little bit about one of my earlier experiments [Tumblr-Mashr](http://www.zya.cc/tumblr-mashr). Just to add a little bit of excitment to the interface, and to finish it up, I decided to use the same technique to get a random gif from Tumblr and set it as background. A `JSONP` request will get a series of posts from Tumblr that are tagged as "glitch" and "gif", one of them will be selected and set as `background` attribute of the page. The gif will be zoomed in significantly (500%) and will be changed on every pattern refresh or sound refresh.

![Interface and Tumblr Background"](project_images/interface1.png?raw=true "Interface and Tumblr Background")

## Mobile Last!

Silly Beat was not intended for mobile but luckily, since it is all HTML5, the app just works on mobile. But I had to compensate a little bit from the effects processing in order to prevent the mobile browsers to crash. The convolver effect is really demanding, so one of the last tasks for me was to detect the browser and remove some features accordingly. I mostly tested it on my iPad mini using Chrome iOS and Safari iOS, and it seems like it works fine. 