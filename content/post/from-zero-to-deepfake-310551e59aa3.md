+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1738/1*X8FEdL05AQchZh335BtYzA.png"
date = "2019-09-18T04:27:15.383Z"
title = "From Zero to Deepfake"
categories = [ ]
+++




<span class=subtitle>Exploring deepfakes with DeepFaceLab</span>


<!--more-->

This is my experience getting started with deepfakes using DeepFaceLab. This article chronicles the general steps I went through to create a deepfake video to demonstrate how advanced the technology has gotten and how simple it is to use. This is not a step-by-step tutorial but it will point you to where you need to go.


## Intro


I am beyond fascinated with deepfakes. From the videos of celebrity mashups like Jim Carrey’s face transferred onto Alison Brie’s body…

<iframe width="560" height="315" src="https://www.youtube.com/embed/b5AWhh6MYCg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

…to the implications fake video and audio will have on the world in general…

<iframe width="560" height="315" src="https://www.youtube.com/embed/bE1KWpoX9Hk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Why? We’ve all seen The Avengers or The Lord of the Rings movies and their incredible computer effects. We know what good CGI looks like because we’ve also seen awful CGI. Great CGI is expensive and big-name movies that have bad computer effects stand out because you expect the opposite. The contrast between expectation and reality is jarring. It’s not that the CGI is bad, it’s that you’re expecting it to be good. The deepfakes we’ve seen go viral are so compelling because the videos have virtually no value but the quality of the effect is incredible. You’re not expecting much but you get Steve Buscemi’s face on Jennifer Lawrence. Your Instagram filters are going to get wild.


How easy is it to generate a deepfake?


## Background


I had the recent opportunity to explore deepfake research as a side project and, of course, I jumped on it. I had zero experience in deepfakes but I’ve been following the news about them like everyone else is. I do have machine learning experience but for unrelated applications. None of my experience was applicable to these experiments outside of being able to troubleshoot general software roadblocks. I started from zero.


I brushed off my old Windows 10 PC, booted it up and started working on updates. Quick research showed Windows was OK so I stuck with it for now. There was a time limit on the first round of research so I cut the corners that looked safe to cut. I started the experiment with my old Nvidia Geforce GTX 970 4gb graphics card but later upgraded to dual Nvidia Geforce RTX 2080 11gb cards. 2080s are big, expensive, and over-the-top for most applications. If you’re looking to experiment with deepfakes as a hobby, you can get away with an 11gb GTX 1080. The RAM is critical and you won’t get far without it.


## Getting started: DeepFaceLab vs Faceswap


Two projects dominate open source deepfake generation, DeepFaceLab(DFL) and Faceswap. Faceswap, on the surface, looked like the safer bet. It has multiple contributors, greater popularity, and more documentation but I couldn’t get far with it. I had a lot of difficulty training and, even when getting enough to push forward, the conversion process would never finish. I have since solved both problems — the first by ditching the GUI and using Ubuntu, the second by tweaking video FPS settings — but I had to commit to DFL because it just worked and the clock was ticking.


## Using DeepFaceLab


You can download pre-built Windows builds from Google Drive or Mega. These will get you the dependencies and allow you to get started the fastest. The manual comes translated from Russian via Google Translate and, even still, it does the job and gets you through each step with minimal headache.


## Step 1: Extraction


The first step in deepfake creation is to extract the frames and then the faces from source and destination videos. You’re looking for several hundred to a couple thousand high-quality images at the end. Each of DFL’s steps comes in the form of an executable batch file that presents options and runs to completion or until you abort it. Advanced usage comes from executing the python directly but you can get far using the bundled executables step by step.


Your model is only going to be as good as the data it learns from. If you want good output you need good input. This means sifting through thousands of images to make sure they are high quality and that DFL detected the faces properly. DFL comes with multiple batch files that will help you with a lot of this process. You can sort by blurriness, face similarity, histogram and more. This helps to make quick work by grouping bad frames and miscaptured faces but you’ll still benefit by manually going through what’s left. You’re going to spend a lot of time training, it’s worth putting in the extra effort here.


At the end of this step you’ll thousands of sliced up frames and normalized faces.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1920/1*Bx9Rodcd0vJx35dO01D8-A.png">

Note: these are not simple images, they have embedded alignment information in the image file. That metadata is important for future processes. Further processing of these images outside of DFL may cause problems.


## Step 2: Training


The next step is choosing the model you want to train. DFL comes with six models of differing sophistication and for different purposes. H64 is for less capable graphics cards, Avatar is for manipulating the facial expressions of a source video, and SAE is a combination of other models. The manual and online tutorials recommend SAE but I went with the only model that would run on my initial graphics card, H64. There are a slew of settings that you can tweak here but it’s hard to know their effect until you see them in action. Unfortunately that takes hours or days so you need to be patient and see what you get.


The results (posted below) were promising but it was clear that my graphics card was limiting the output quality. By upgrading to an 11GB card I was able to experiment with the other models and committed to SAE for longer durations.


You can stop the training and restart at any point so you can back up models and save “checkpoints.” After backing up you can diverge to see if new settings offer promising results. I recommend backing up at around 40,000 iterations and testing different settings from there. Always backup before you try aggressive settings. This type of machine learning can implode to the point where the model is no longer useful. This collapse is unrecoverable and you’ll have no choice but to restore from a backup.


## Step 3: Convert


After you have trained the model to a point you are happy, it’s time to convert a destination video and produce your first deepfake. The conversion process takes your model and uses it to generate an image to overlay on the destination video. You can tweak settings that contract or blur the mask, change the coloring of the output, rescale the overlaid image, and more. This is a cheaper process though still took about 30 minutes each run to convert the frames for a 46 second video.


The final step is to merge all the converted frames into a video file. This takes comparatively little time and then — voila — you are now on the bleeding edge of fake news.


## Results


The first experiments with H64 were what I used to determine if DFL had what it took to invest time in.

<iframe width="560" height="315" src="https://www.youtube.com/embed/hb6GQK02wJ0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

You’ll immediately notice the flickering and that was due to a failure on my part likely during the extraction phases. My interest was primarily around the quality of the overlay so I tolerated it without correcting it.


After determining DFL was good enough to play with further I started amassing source files for the target. The target was to be John Stackhouse, SVP at the Royal Bank of Canada and former Editor-in-Chief of the Globe & Mail. John was moderating a panel on deepfakes and election security at the University of Toronto and asked us how easy it was to create a deepfake. We decided a good destination video for the demonstration would be Simon Cowell from American Idol.


The first iteration of the SAE model at about 25k iterations looked promising…

<iframe width="560" height="315" src="https://www.youtube.com/embed/xbSCP1C_mOM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

…but getting much better turned out to be very difficult. This is after 150k iterations…

<iframe width="560" height="315" src="https://www.youtube.com/embed/5HPQruWLwhs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

That model ended up collapsing which taught me a lot about generative adversarial networks. I had to restore from an earlier version and use different settings.


This is the final iteration I landed on before calling it quits. I know it could be better but by this time I was out of runway.

<iframe width="560" height="315" src="https://www.youtube.com/embed/5HUs-t5MUoQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The processing time for this particular video is hard to pin down after all the starts, stops, and restores from backup but it was probably close to around 24–36 hours.


## What I would have done differently


### Local vs Cloud


I optimized for a local environment because I thought it would allow me to get started faster. While that probably held true, slight tweaks to the model can take hours or days to amount to anything and I wish I had bitten the bullet and figured out a cloud solution first. This would have allowed me to (presumably) run experiments in parallel and I would have iterated more rapidly. I could be wrong, but I intend to double back and rerun some early experiments on cloud solutions to compare quality and performance.


### Source dataset


I started with the impression that tens of thousands of good frames from a handful of source videos were going to be enough. After running more tests it turns out that a couple thousand is all that’s necessary and it is better to have a wider range of images from many different angles and, importantly, lighting conditions.


### DFL vs Faceswap


DFL treated me very well and I have no regrets, but I am starting to see where Faceswap is more advanced. DFL does not support multiple GPUs while Faceswap does. Faceswap has also spent more time on the GUI which is going to make this more accessible in the future. I have now started working with Faceswap and it churns along on both GPUs though I am still clumsily working through its documentation.


## Conclusion


It was not trivial to get to the point I ended at but the path to getting better is clear: better input data, more manual tweaking, and longer training. There is no doubt that this technology will get better and easier to use and this is only the tip of the iceberg. From a technical expertise perspective I had to apply very little of my ~20 years of experience in software to get started with DFL. The windows build is self-contained and dependency-free. I’m still running into problems with Faceswap but they are all user experience and dependency problems. They are important to address but problems like those are everyday software development chores, not deep machine learning problems solvable only by geniuses and scientists.


Deepfakes are here to stay. They will get much, much better and we need to live with that reality. A future where deepfakes run rampant may sound like a terrifying, dystopian nightmare but I posit that we’re already in that nightmare. What we have to look forward to is waking up. We’ve had expert graphics manipulation tools available for decades, it’s nothing new. We have incredible CGI in movies and Photoshopped pictures are literally everywhere you look. We’re already living in a world where we ask ourselves “is that real?” multiple times a day. Deepfake technology will elevate the importance of detection and validation mechanisms for images and video of all kinds. With any luck, the near future will allow us to automatically detect what’s fake and we won’t have to wonder anymore.


[Share this on Medium](https://medium.com/@jsoverson/from-zero-to-deepfake-310551e59aa3)
