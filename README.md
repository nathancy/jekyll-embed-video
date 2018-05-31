# jekyll-embed-video
Embed YouTube, Vimeo, and Twitch videos/clips in Jekyll webpages without a plugin. If you are hosting your webpage using GitHub pages, you can't use third party plugins. Here is a method to use 'includes' instead of plugins.

See the raw text in `example.md` for a complete example.

## Demo

http://www.nathan-lam.com/projects/jekyll-embed-video

## Table of Contents
* [Embed YouTube](#embed-youtube)
* [Embed Vimeo](#embed-vimeo)
* [Embed Twitch](#embed-twitch)
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
These attributes are defined in the [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe). You can set various additional attributes on the embedded video no matter what provider you use. 

| Name | Type | Description |
| :--- | --- | --- |
| 'allowfullscreen' | boolean | If `true`, the player can go full screen. |
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
---
# Embed Youtube

Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. 

<!---
Include this next line in your .md for Youtube videos, make sure to put your video ID up there!

Example:     youtubeId: --b-9HrKK6w
-->

{% include youtubePlayer.html id=page.youtubeId %}


# Embed Vimeo

More Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. 

<!---
Include this next line in your .md file for Vimeo videos, make sure to put your video ID up there!

Example:     vimeoID: --b-9HrKK6w
-->

{% include vimeoPlayer.html id=page.vimeoId %}

# Embed Twitch

More Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. Flavor text. 

<!---
Include this next line in your .md file for Twitch videos, make sure to put your video ID up there!

Example:     twitchId: --b-9HrKK6w
-->

{% include twitchPlayer.html id=page.twitchId %}
```