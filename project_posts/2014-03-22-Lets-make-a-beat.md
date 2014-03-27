###Javascript, Javascript Everywhere

Now that we found our sounds, I need to find a way to download them and manupilate them in order to make beat. SoundCloud API does not allow cross-origin requests on the actual audio stream urls. I had to use `XMLHttpRequest` to get the sounds ready as `arraybuffer` to be used in HTML5's Web Audio API audio graph. This issue delayed my project the longest since I did not have any experience in developing on the server-side. I just knew that I need to create a proxy server to solve this issue but I did know any server-side language. I consider myself new as a coder (one year) and the only language I know good (at least I think I do) is Javascript. The good thing about Javascript is that it is everywhere. It runs on every old and new device, on every browser and recently it appeared on music production softwares such as [Bitwig](http://www.ohdratdigital.com/software-news/bitwig-studios-controller-scripting-gets-teased/) and [Logic Pro X](http://www.macprovideo.com/hub/logic-pro/logic-pro-x-free-script-for-incredible-new-scripter-midi-fx-plug-in). I see coding as another tool for me to creativity and availability of Javascript provides a good opportunity for me to prototype quickly. At the same time, it makes me lazy and stops me from learning more languages. In this case, [Node.js](http://nodejs.org/) allowed me to use my beloved JS in the server-side without worrying about learning Ruby or something like that. Lazy... but it does the job.

I came across a small node module called [cors-anywhere](https://github.com/Rob--W/cors-anywhere) which makes it really easy to create a proxy server to handle cross-origin request. And that was exactly what I needed. 

__Long live JS__.


###It is quiet probable!

As mentioned in the previous posts, a big part of this project for me is to create __a tool that does what I am not able to do__. I wanted to leave a lot of the choices to the computer to make so I use a lot of randomisation. But in order to have the output make a little bit of musical sense, I had to define some boundaries for this randomisation otherwise it would be a complete chaos. For example, to have everything sound like a beat, the snare will always be on the downbeat, or the probability amount for the hihat is less than the sample. But everything else from tempo speed to the patterns and playback rates will be randomised.

All of these are going to happen within a one bar loop with 16 possible steps for each sounds.

````
var generatePattern = function(probability){
    var array = [];
	for(var i =0; i < 16; i++){
		
		var random = Math.round(Math.random() * probability);

		//the higher the probability - the lower the chance
		if(random === 1){
			array[i] = true;
		}
	}
	return array;
};
````

The drum sounds all use the same function for their patterns, but the main sample uses an additional function to create a second pattern for playback offset. This will help achieving a more interesting result by using different sections of the sample for each hit as oppose to playing the sample from the beginning every time.

````
var generateOffsetPattern = function(){
    var array = [];
	for(var i =0; i < 16; i++){
		array[i] = Math.random();
	}
	return array;
};

````
After all the magic and selecting a speed, the `play` function will start a loop, and will schedule the playback according to the give pattern object.

````
//play function starts the loop
function play(){
    //the loop function run every bar
	l = new loop(function(next){

		//here i play the sounds 

		for(var i = 0; i < 16; i++){
			
			//kick
			if(kick.loaded && kickPattern[i]){

				kick.start(next + (sixteenthNote * i));
				kick.stop(next + (sixteenthNote * i) + (sixteenthNote));

			}
			//snare
			if(snare.loaded){

				snare.start(next + (quarterNote * 2));
				snare.stop(next + (quarterNote * 2) + sixteenthNote);
			}
			//hihat
			if(hat.loaded && hatPattern[i]){

				hat.start(next + (sixteenthNote * i));
				hat.stop(next + (sixteenthNote * i) + sixteenthNote);
			}
			//perc
			if(perc.loaded){
				perc.start(next + (quarterNote * 3));
				perc.stop(next + (quarterNote * 3.5));
			}
			//sample
			if(sample.loaded && samplePattern[i]){

				var offset = sampleOffsetPattern[i] * (sample.buffer.duration);
				sample.start(next + (sixteenthNote * i),offset);
				sample.stop(next + (sixteenthNote * i) + (sixteenthNote));
			}

		}
		

	},0,speed,context);
	beatGain.gain.value = 1;
	l.start();
}
````
The next steps will be to design a simple UI and add recording functionality. I will post some of the generated results on the upcoming posts.
