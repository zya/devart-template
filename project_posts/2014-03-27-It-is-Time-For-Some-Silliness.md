Some final tweaks and it is done. After having the main structure working, I spent some time changing the little parameters for a better performance and nicer results. 

I tweaked the time range for each sample so that the drum sounds are downloaded quicker and are ready before the main sample. I changed the probability factor of sounds like hihat to prevent chaos and finally I tweaked the mix a little bit further for an optimal sounding beat. I also refactored the code a little bit for a better and readable code.

```

//generate search params - query,tags,durationfrom,durationto
kickParams = generateParameters("kick drum","",300, 40000);
snareParams = generateParameters("snare","",100,30000);
hatParams = generateParameters("hihat","",100,30000);
sampleParams = generateParameters("","",5000,500000); //uses nothing as string for more various results
percParams = generateParameters("percussion sample","",0,30000);

//volumes - Balance mix
kickGain.gain.value = 1;
reverbGain.gain.value = 0.5;
hatGain.gain.value = 0.4;
snareGain.gain.value = 0.15;
percGain.gain.value = 0.4;
sampGain.gain.value = 1;
delay.output.gain.value = 0.5;

//patterns and probability
hatPattern = generatePattern(3);
samplePattern = generatePattern(1);
kickPattern = generatePattern(3);
sampleOffsetPattern = generateOffsetPattern();

```

[Here](https://soundcloud.com/iamzya/sets/silly-beat/s-fvZRF) you can listen to 10 beats I recorded today using Silly Beat. And you can check the video demos below.

https://www.youtube.com/watch?v=zeseaRbhyew

https://www.youtube.com/watch?v=ODjQAlNG500

As you can hear, there are some interesting results. For me this was a great journey into generative music. Having used soundcloud as the sound source and by using a series for random elements and by having minimum control over the sound, I believe the possibilities are endless are I would really love to discover this field further. Also, I would like to hear what everybody else will create using Silly Beat.