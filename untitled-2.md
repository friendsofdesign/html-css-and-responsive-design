# HTML Video & Audio

### Audio and video on the web

Web developers have wanted to use video and audio on the Web for a long time, ever since the early 2000s, when we started to have bandwidth fast enough to support any kind of video \(video files are much larger than text or even images.\) In the early days, native web technologies such as HTML didn't have the ability to embed video and audio on the Web, so proprietary \(or plugin-based\) technologies like [Flash](https://en.wikipedia.org/wiki/Adobe_Flash) \(and later, [Silverlight](https://en.wikipedia.org/wiki/Microsoft_Silverlight)\) became popular for handling such content. This kind of technology worked ok, but it had a number of problems, including not working well with HTML/CSS features, security issues, and accessibility issues.

A native solution would solve much of this if done right. Fortunately, a few years later the [HTML5](https://developer.mozilla.org/en-US/docs/Glossary/HTML5)specification had such features added, with the [`<video>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video) and [`<audio>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio) elements, and some shiny new [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) [APIs](https://developer.mozilla.org/en-US/docs/Glossary/API) for controlling them. We'll not be looking at JavaScript here — just the basic foundations that can be achieved with HTML.

We won't be teaching you how to produce audio and video files — that requires a completely different skillset. We have provided you with [sample audio and video files and example code](https://github.com/mdn/learning-area/tree/master/html/multimedia-and-embedding/video-and-audio-content) for your own experimentation, in case you are unable to get hold of your own.

**Note**: Before you begin here, you should also know that there are a quite a few [OVPs](https://developer.mozilla.org/en-US/docs/Glossary/OVP) \(online video providers\) like [YouTube](https://www.youtube.com/), [Dailymotion](http://www.dailymotion.com/), and [Vimeo](https://vimeo.com/), and online audio providers like [Soundcloud](https://soundcloud.com/). Such companies offer a convenient, easy way to host and consume videos, so you don't have to worry about the enormous bandwidth consumption. OVPs even usually offer ready-made code for embedding video/audio in your webpages. If you go that route, you can avoid some of the difficulties we discuss in this article. We'll be discussing this kind of service a bit more in the next article.

#### The `<video>` element

The [`<video>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video) element allows you to embed a video very easily. A really simple example looks like this:

```text
<video src="rabbit320.webm" controls>
  <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.webm">link to the video</a> instead.</p> 
</video>
```

The features of note are:

* `src`

  In the same way as for the [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) element, the `src` attribute contains a path to the video you want to embed. It works in exactly the same way.

* `controls`

  Users must be able to control video and audio playback \(it's especially critical for people who have [epilepsy](https://en.wikipedia.org/wiki/Epilepsy#Epidemiology).\) You must either use the `controls` attribute to include the browser's own control interface, or build your interface using the appropriate [JavaScript API](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement). At minimum, the interface must include a way to start and stop the media, and to adjust the volume.

* The paragraph inside the `<video>` tags

  This is called **fallback content** — this will be displayed if the browser accessing the page doesn't support the `<video>` element, allowing us to provide a fallback for older browsers. This can be anything you like; in this case we've provided a directly link to the video file, so the user can at least access it some way regardless of what browser they are using.

The embedded video will look something like this:

![](https://mdn.mozillademos.org/files/12794/simple-video.png)

You can try the example live here: [http://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/simple-video.html](http://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/simple-video.html)

 \(see also the source code: [https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/video-and-audio-content/simple-video.html](https://github.com/mdn/learning-area/blob/master/html/multimedia-and-embedding/video-and-audio-content/simple-video.html)\)

#### Supporting multiple formats

There's a problem with the above example, which you may have noticed already if you've tried to access the live link above with a browser like Safari or Internet Explorer. The video won't play! This is because different browsers support different video \(and audio\) formats.

Let's go through the terminology quickly. Formats like MP3, MP4 and WebM are called **container formats**. They contain different parts that make up the whole song or video — such as an audio track, a video track \(in the case of video\), and metadata to describe the media being presented.

The audio and video tracks are also in different formats, for example:

* A WebM container usually packages Ogg Vorbis audio with VP8/VP9 video. This is supported mainly in Firefox and Chrome.
* An MP4 container often packages AAC or MP3 audio with H.264 video. This is supported mainly in Internet Explorer and Safari.
* The older Ogg container tends to go with Ogg Vorbis audio and Ogg Theora video. This was supported mainly in Firefox and Chrome, but has basically been superceded by the better quality WebM format.

An audio player will tend to play an audio track directly, e.g. an MP3 or Ogg file. These don't need containers.

**Note**: It is not quite that simple, as you can see from our [audio-video codec compatibility table](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats#Browser_compatibility). In addition, many mobile platform browsers can play an unsupported format by handing it off to the underlying system's media player to play. But this will do for now.

The above formats exist to compress video and audio into manageable files \(raw video and audio is very large\). Browsers contain different **Codecs**, like Vorbis or H.264, which are used to convert the compressed sound and video into binary digits and back. As indicated above, browsers unfortunately don't all support the same codecs, so you will have to provide several files for each media production. If you're missing the right codec to decode the media, it just won't play.

**Note:** You might be wondering why this situation exists. **MP3** \(for audio\) and **MP4/H.264** \(for video\) are both widely supported, and good quality. However, they are also patent encumbered — American patents cover MP3 until at least 2017, and H.264 until 2027 at the earliest, meaning that browsers that don't hold the patent have to pay huge sums of money to support these formats. In addition, many people avoid restricted software on principle, in favour of open formats. This is why we have to provide multiple formats for different browsers.

So how do we do this? Take a look at the following [updated example](https://github.com/mdn/learning-area/blob/gh-pages/html/multimedia-and-embedding/video-and-audio-content/multiple-video-formats.html) \([try it live here](http://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/multiple-video-formats.html), also\):

```text

<video controls>
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.mp4">link to the video</a> instead.</p>
</video>
```

Here we've taken the `src` attribute out of the actual `<video>` tag, and instead included separate [`<source>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/source) elements that point to their own sources. In this case the browser will go through the `<source>` elements and play the first one that it has the codec to support. Including WebM and MP4 sources should be enough to play your video on most platforms and browsers these days.

Each `<source>` element also has a `type` attribute. This is optional, but it is advised that you include them — they contain the [MIME types](https://developer.mozilla.org/en-US/docs/Glossary/MIME_type) of the video files, and browsers can read these and immediately skip videos they don't understand. If they are not included, browsers will load and try to play each file until they find one that works, taking even more time and [resources](http://moodle.friendsofdesign.co.za/mod/page/view.php?id=577).

**Note**: Our article on supported media formats \([https://developer.mozilla.org/en-US/docs/Web/HTML/Supported\_media\_formats](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats)\) contains some common [MIME types](https://developer.mozilla.org/en-US/docs/Glossary/MIME_type).

#### Other `<video>` features

There are a number of other features you can include on an HTML5 video. Take a look at our third example, below:

```text

<video controls width="400" height="400"
       autoplay loop muted
       poster="poster.png">
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.mp4">link to the video</a> instead.</p>
</video>
```

This will give us a output looking something like this:

![](https://mdn.mozillademos.org/files/12796/extra-video-features.png)

The new features are:

* `width` and `height`

  You can control the video size either with these attributes or with [CSS](https://developer.mozilla.org/en-US/docs/Glossary/CSS). In both cases, videos maintain their native width-height ratio — known as the **aspect ratio**. If the aspect ratio is not maintained by the sizes you set, the video will grow to fill the space horizontally, and the unfilled space will just be given a solid background color by default.

* `autoplay`

  This attribute makes the audio or video start playing right away while the rest of the page is loading. You are advised not to use autoplaying video \(or audio\) on your sites, because users can find it really annoying.

* `loop`

  This attribute makes the video \(or audio\) start playing again whenever it finishes. This can also be annoying, so only use if really necessary.

* `muted`

  This attribute causes the media to play with the sound turned off by default.

* `poster`

  This attribute takes as its value the URL of an image, which will be displayed before the video is played. It is intended to be used for a splash or advertising screen.

* `preload`

  this attribute is used in the element for buffering large files. It can take one of 3 values:

  1. `"none"` does not buffer the file

1. `"auto"` buffers the media file
2. `"metadata"` buffers only the metadata for the file

You can find the above example available to [play live on Github](http://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/extra-video-features.html) \(also [see the source code](https://github.com/mdn/learning-area/blob/gh-pages/html/multimedia-and-embedding/video-and-audio-content/extra-video-features.html).\) Note that we haven't included the `autoplay` attribute in the live version — if the video starts to play as soon as the page loads, you don't get to see the poster!

#### The `<audio>` element

The [`<audio>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio) element works in exactly the same way as the [`<video>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video) element, with a few small differences as outlined below. A typical example might look like so:

```text

<audio controls>
  <source src="viper.mp3" type="audio/mp3">
  <source src="viper.ogg" type="audio/ogg">
  <p>Your browser doesn't support HTML5 audio. Here is a <a href="viper.mp3">link to the audio</a> instead.</p>
</audio>
```

This produces something like the following in a browser:

![](https://mdn.mozillademos.org/files/12798/audio-player.png)

**Note**: You can [run the audio demo live](http://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/multiple-audio-formats.html) on Github \(also see the [audio player source code](https://github.com/mdn/learning-area/blob/gh-pages/html/multimedia-and-embedding/video-and-audio-content/multiple-audio-formats.html).\)

This takes up less space than a video player, as there is no visual component — you just need to display controls to play the audio. Other differences from HTML5 video are as follows:

* The [`<audio>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio) element doesn't support the `width`/`height` attributes — again, there is no visual component, so there is nothing to assign a width or height to.
* It also doesn't support the `poster` attribute — again, no visual component.

Other than this, `<audio>` supports all the same features as `<video>` — review the above sections for more information about them.

#### Displaying video text tracks

Now we'll discuss a slightly more advanced concept that is really useful to know about. Many people can't or don't want to hear the audio/video content they find on the Web, at least at certain times. For example:

* Many people have auditory impairments \(more commonly known as hard of hearing, or deaf\) so can't hear the audio.
* Others may not be able to hear the audio because they are in noisy environments \(like a crowded bar when a sports game is being shown\) or might not want to disturb others if they are in a quiet place \(like a library.\)
* People who don't speak the language of the video might want a text transcript or even translation to help them understand the media content.

Wouldn't it be nice to be able to provide these people with a transcript of the words being spoken in the audio/video? Well, thanks to HTML5 video you can, with the [WebVTT](https://developer.mozilla.org/en-US/docs/Web/API/Web_Video_Text_Tracks_Format) format and the [`<track>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/track) element.

**Note**: "Transcribe" and "transcript" mean to write down spoken words as text.

WebVTT is a format for writing text files containing multiple strings of text along with metadata such as what time in the video you want each text string to be displayed, and even limited styling/positioning information. These text strings are called **cues**, and you can display different types for different purposes, the most common being:

* **subtitles**

  Translations of foreign material, for people who don't understand the words spoken in the audio.

* **captions**

  Synchronized transcriptions of dialog or descriptions of significant sounds, to let people who can't hear the audio understand what is going on.

* **timed descriptions**

  Text for conversion into audio, to serve people with visual impairments.

A typical WebVTT file will look something like this:

```text
WEBVTT
​
1
00:00:22.230 --> 00:00:24.606
This is the first subtitle.
​
2
00:00:30.739 --> 00:00:34.074
This is the second.
​
  ...
```

To get this displayed along with the HTML media playback, you need to:

1. Save it as a `.vtt` file in a sensible place.
2. Link to the `.vtt` file with the [`<track>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/track) element. `<track>` should be placed within `<audio>`or `<video>`, but after all `<source>` elements. Use the `kind` attribute to specify whether the cues are `subtitles`, `captions`, or `descriptions`. Further, use `srclang` to tell the browser what language you have written the subtitles in.

Here's an example:

```text

<video controls>
    <source src="example.mp4" type="video/mp4">
    <source src="example.webm" type="video/webm">
    <track kind="subtitles" src="subtitles_en.vtt" srclang="en">
</video>
```

This will result in a video that has subtitles displayed, kind of like this:

![](https://mdn.mozillademos.org/files/7887/video-player-with-captions.png)

For more details, please read [Adding captions and subtitles to HTML5 video](https://developer.mozilla.org/en-US/Apps/Build/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video). You can [find the example](http://iandevlin.github.io/mdn/video-player-with-captions/) that goes along with this article on Github, written by Ian Devlin \(see the [source code](https://github.com/iandevlin/iandevlin.github.io/tree/master/mdn/video-player-with-captions) too.\) This example uses some JavaScript to allow users to choose between different subtitles. Note that to turn the subtitles on, you need to press the "CC" button and select an option — English, Deutsch, or Español.

**Note**: Text tracks also help you with [SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO), since search engines especially thrive on text. Text tracks even allow search engines to link directly to a spot partway through the video.

#### Active learning: Embedding your own audio and video

For this active learning, we'd \(ideally\) like you to go out into the world and record some of your own video and audio — most phones these days allow you to record audio and video very easily, and provided you can transfer it on to your computer, you can use it. You may have to do some conversion to end up with a WebM and MP4 in the case of video, and an MP3 and Ogg in the case of audio, but there are enough programs out there to allow you to do this without too much trouble, such as [Miro Video Converter](http://www.mirovideoconverter.com/) and [Audacity](https://sourceforge.net/projects/audacity/). We'd like you to have a go!

If you are unable to source any video or audio, then you can feel free to use our [sample audio and video files](https://github.com/mdn/learning-area/tree/master/html/multimedia-and-embedding/video-and-audio-content) to carry out this exercise. You can also use our sample code for reference.

We would like you to:

1. Save your audio and video files in a new directory on your computer.
2. Create a new HTML file in the same directory, called `index.html`.
3. Add `<audio>` and `<video>` elements to the page; make them display the default browser controls.
4. Give both of them `<source>` elements so that browsers will find the audio format they support best and load it. These should include `type` attributes.
5. Give the `<video>` element a poster that will be displayed before the video starts to be played. Have fun creating your own poster graphic.

For an added bonus, you could try researching text tracks, and work out how to add some captions to your video.

