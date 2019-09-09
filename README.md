# jekyll-embed-video
Embed YouTube, Vimeo, Twitch, Streamable, Mixer, Google Drive videos/clips and more in Jekyll webpages without a plugin. If you are hosting your webpage using GitHub pages, you can't use third party plugins. Here is a method to use "includes" instead of plugins.

See the raw text in `example.md` for a complete example. Remember to add in [video-embed.css](https://github.com/nathancy/jekyll-embed-video/blob/master/video-embed.css) for [responsive videos](#responsive-videos) that automatically resize with changing window dimensions. 

## Demo

http://www.nathan-lam.com/projects/jekyll-embed-video

## Table of Contents
* [Embed YouTube](#embed-youtube)
* [Embed Vimeo](#embed-vimeo)
* [Embed Twitch](#embed-twitch)
* [Embed Streamable](#embed-streamable)
* [Embed Mixer](#embed-mixer)
* [Additional support for 20Detik, Dailymotion, Metube, Vidio, or LINE Today](#additional-support)
* [Embed Google Drive](#embed-google-drive)
* [Responsive Videos](#responsive-videos)
* [Iframe Attributes](#iframe-attributes)
* [Full Example](#full-example)

## Embed YouTube 

Create a file in your `_includes` folder called `youtubePlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://www.youtube.com/embed/{{ include.id }}"
      width="700"
      height="480"
      frameborder="0"
      allowfullscreen="">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include youtubePlayer.html id=page.youtubeId %}
```

On the top of your .md file, put the YouTube video ID. You could also put the ID of the video directly.

```
---
youtubeId: putYourIDHere
---
```

## Embed Vimeo

Create a file in your `_includes` folder called `vimeoPlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://player.vimeo.com/video/{{ include.id }}"
      width="500"
      height="281"
      frameborder="0"
      webkitallowfullscreen
      mozallowfullscreen
      allowfullscreen>
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include vimeoPlayer.html id=page.vimeoId %}
```

On the top of your .md file, put the Vimeo video ID. You could also put the ID of the video directly.

```
---
vimeoId: putYourIDHere
---
```

## Embed Twitch 

Create a file in your `_includes` folder called `twitchPlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://clips.twitch.tv/embed?clip={{ include.id }}"
      height="360"
      width="640"
      frameborder="0"
      scrolling="no"
      muted="false"
      autoplay="false"
      allowfullscreen="true">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include twitchPlayer.html id=page.twitchId %}
```

On the top of your .md file, put the Twitch video ID. You could also put the ID of the video directly.

```
---
twitchId: putYourIDHere
---
```

## Embed Streamable 

Create a file in your `_includes` folder called `streamablePlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://streamable.com/s/{{ include.id }}"
      height="360"
      width="640"
      frameborder="0"
      scrolling="no"
      allowfullscreen="true">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include streamablePlayer.html id=page.streamableId %}
```

On the top of your .md file, put the Streamable video ID. You could also put the ID of the video directly.

```
---
streamableId: putYourIDHere
---
```

## Embed Mixer 

Create a file in your `_includes` folder called `mixerPlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://mixer.com/embed/player/mixer?vod={{ include.id }}"
      height="360"
      width="640"
      frameborder="0"
      scrolling="no"
      allowfullscreen="true">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include mixerPlayer.html id=page.mixerId %}
```

On the top of your .md file, put the Mixer video ID. You could also put the ID of the video directly.

```
---
mixerId: putYourIDHere
---
```

## Embed Google Drive 

Embedding Google Drive videos have additional steps. 

1. For the desired video, change the link sharing setting to `On - Anyone with the link`. This will make the video accessible to anyone who has the link as no sign-in is required. 
  
  **Important**: If you do not change the video setting to this option, your video will not show.
  
2. Double click the video to show the preview. Click the setting options and select "Open in new window". Now click on the setting option again and select "Embed item". The iframe code should appear. For example:

```
<iframe src="https://drive.google.com/file/d/1EC8BnjJMon-vqy-UhLKk9sf_oukZzEbP/preview"></iframe>
```

`1EC8BnjJMon-vqy-UhLKk9sf_oukZzEbP/preview` would be your video ID.

**Note**: Right clicking the video will not bring up the embed option. You must open the video in a new window. 

Create a file in your `_includes` folder called `googleDrivePlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      width="640"
      height="480"
      src="https://drive.google.com/file/d/{{ include.id }}"
      frameborder="0"
      allowfullscreen="">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include googleDrivePlayer.html id=page.driveId %}
```

On the top of your .md file, put the Google Drive video ID. You could also put the ID of the video directly.

```
---
driveId: putYourIDHere
---
```

## Additional support
## Embed 20Detik

Create a file in your `_includes` folder called `20detikPlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://20.detik.com/embed/{{ include.id }}"
      width="700"
      height="480"
      frameborder="0"
      scrolling="no"
      allowfullscreen="true">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include 20detikPlayer.html id=page.detikId %}
```

On the top of your .md file, put the Detik video ID. You could also put the ID of the video directly.

```
---
detikId: 190130051
---
```

## Embed Dailymotion 

Create a file in your `_includes` folder called `dailymotionPlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://www.dailymotion.com/embed/video/{{ include.id }}"
      width="700"
      height="480"
      frameborder="0"
      allowfullscreen=""
      allow="autoplay">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include dailymotionPlayer.html id=page.dailymotionId %}
```

On the top of your .md file, put the Dailymotion video ID. You could also put the ID of the video directly.

```
---
dailymotionId: x2btuie
---
```

## Embed Metube 

Create a file in your `_includes` folder called `metubePlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://www.metube.id/embed/{{ include.id }}"
      width="700"
      height="480"
      frameborder="0"
      allowfullscreen="">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include metubePlayer.html id=page.metubeId %}
```

On the top of your .md file, put the Metube video ID. You could also put the ID of the video directly.

```
---
metubeId: 11107214
---
```

## Embed Vidio 

Create a file in your `_includes` folder called `vidioPlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://www.vidio.com/embed/{{ include.id }}"
      width="700"
      height="480"
      scrolling="no"
      frameborder="0"
      allowfullscreen="">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include vidioPlayer.html id=page.vidioId %}
```

On the top of your .md file, put the Vidio video ID. You could also put the ID of the video directly.

```
---
vidioId: 1671743
---
```

## Embed LINE Today 

LINE Today contents are served in different countries so another `country` parameter (to be filled with a 2-letter country code) is needed. Here's all the supported country codes (case-insensitive)

* `hk` - Hong Kong
* `id` - Indonesia
* `th` - Thailand
* `tw` - Taiwan

Create a file in your `_includes` folder called `linetodayPlayer.html` with this code inside: 

```
<div class="embed-container">
  <iframe
      src="https://today.line.me/{{ include.country }}/embed/{{ include.id }}"
      width="700"
      height="480"
      frameborder="0"
      allowfullscreen=""
      allow="autoplay; encrypted-media">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```
{% include linetodayPlayer.html id=page.linetodayId %}
```

On the top of your .md file, put the LINE Today video ID. You could also put the ID of the video directly.

```
---
linetodayId: abcdefg 
---
```

## Responsive Videos
For responsive videos that automatically resize with changing window sizes, add in `video-embed.css`.

```
.embed-container {
  position: relative;
  padding-bottom: 56.25%;
  height: 0;
  overflow: hidden;
  max-width: 100%;
}

.embed-container iframe, .embed-container object, .embed-container embed {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

## Iframe Attributes
These attributes are defined in the [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe). You can set various additional attributes no matter what provider you use. 

| Name | Type | Description |
| :--- | --- | --- |
| `allowfullscreen` | boolean | If `true`, the player can go full screen. |
| `height` | integer | Height of the embedded window, in pixels. |
| `width` | integer | Width of the embedded window, in pixels. |
| `scrolling` | boolean | Indicates when the browser should provide a scroll bar (or other scrolling device) for the frame. Recommended: `no`. |
| `src` | string | The video/clip source URL link |
| `autoplay` | boolean | If `true`, the video starts playing automatically, without the user clicking play. The exception is mobile devices, on which video cannot be played without user interaction. Default: `true`. |
| `muted` | boolean | Specifies whether the initial state of the video is muted. Default: `false`. |
| `time` | 1h2m3s | Time in the video where playback starts. Specifies hours, minutes, and seconds. Default: 0h0m0s (the start of the video). |


## Full example

```
---
youtubeId: putYourIDHere
vimeoId: putYourIDHere
twitchId: putYourIDHere
streamableId: putYourIDHere
mixerId: putYourIDHere
driveId: putYourIDHere
---
# Embed Youtube

<!---
Include this next line in your .md for Youtube videos, make sure to put your video ID up there!

Example:     youtubeId: lDi9uFcD7XI
-->

{% include youtubePlayer.html id=page.youtubeId %}

# Embed Vimeo

<!---
Include this next line in your .md file for Vimeo videos, make sure to put your video ID up there!

Example:     vimeoID: 22439234
-->

{% include vimeoPlayer.html id=page.vimeoId %}

# Embed Twitch

<!---
Include this next line in your .md file for Twitch videos, make sure to put your video ID up there!

Example:     twitchId: GrotesqueArbitraryGullPupper
-->

{% include twitchPlayer.html id=page.twitchId %}

# Embed Streamable 

<!---
Include this next line in your .md file for Streamable videos, make sure to put your video ID up there!

Example:     streamableId: s9ijg 
-->

{% include streamablePlayer.html id=page.streamableId %}

# Embed Mixer 

<!---
Include this next line in your .md file for Mixer videos, make sure to put your video ID up there!

Example:     mixerId: -Q8g7gGquEqxTNAGaz14qA
-->

{% include mixerPlayer.html id=page.mixerId %}

# Embed Google Drive

<!---
Include this next line in your .md file for Google Drive videos, make sure to put your video ID up there!

Example:     driveId: 0B7L_dMcaZknxVTRndmdSQ0F5OFE/preview
-->

{% include googleDrivePlayer.html id=page.driveId %}

# Embed 20Detik 

<!---
Include this next line in your .md file for 20Detik videos, make sure to put your video ID up there!

Example:     detikId: 190130051
-->

{% include 20detikPlayer.html id=page.detikId %}

# Embed Dailymotion 

<!---
Include this next line in your .md file for Dailymotion videos, make sure to put your video ID up there!

Example:     dailymotionId: x2btuie
-->

{% include dailymotionPlayer.html id=page.dailymotionId %}

# Embed Metube 

<!---
Include this next line in your .md file for Metube videos, make sure to put your video ID up there!

Example:     metubeId: 11107214
-->

{% include metubePlayer.html id=page.metubeId %}

# Embed Vidio 

<!---
Include this next line in your .md file for Vidio videos, make sure to put your video ID up there!

Example:     vidioId: 1671743
-->

{% include vidioPlayer.html id=page.vidioId %}

# Embed LINE Today 

<!---
Include this next line in your .md file for LINE Today videos, make sure to put your video ID up there!

Example:     linetodayId: abcdefg 
-->

{% include linetodayPlayer.html id=page.linetodayId %}
```
