# jekyll-embed-video

Embed YouTube, Vimeo, Twitch, Facebook, Streamable, Google Drive videos/clips and more in Jekyll webpages without a plugin. If you are hosting your webpage using GitHub pages, you can't use third party plugins. Here is a method to use "includes" instead of plugins.

See the raw text in `example.md` for a complete example. Remember to add in [video-embed.css](https://github.com/nathancy/jekyll-embed-video/blob/master/video-embed.css) for [responsive videos](#responsive-videos) that automatically resize with changing window dimensions.

## Demo

<http://www.nathan-lam.com/projects/jekyll-embed-video>

## Table of Contents

* [Embed YouTube](#embed-youtube)
* [Embed Vimeo](#embed-vimeo)
* [Embed Twitch](#embed-twitch)
* [Embed Facebook](#embed-facebook)
* [Embed Streamable](#embed-streamable)
* [Embed Google Drive](#embed-google-drive)
* [Additional support for 20Detik, Dailymotion, Vidio, and LINE Today](#additional-support)
* [Responsive Videos](#responsive-videos)
* [Iframe Attributes](#iframe-attributes)
* [Full Example](#full-example)

## Embed YouTube

Create a file in your `_includes` folder called `youtubePlayer.html` with this code inside:

```html
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

```liquid
{% include youtubePlayer.html id=page.youtubeId %}
```

On the top of your .md file, put the YouTube video ID. You could also put the ID of the video directly.

```yaml
---
youtubeId: putYourIDHere
---
```

## Embed Vimeo

Create a file in your `_includes` folder called `vimeoPlayer.html` with this code inside:

```html
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

```liquid
{% include vimeoPlayer.html id=page.vimeoId %}
```

On the top of your .md file, put the Vimeo video ID. You could also put the ID of the video directly. Take a look at [accessing and editing embed codes](https://vimeo.zendesk.com/hc/en-us/articles/360000710167-Accessing-and-editing-embed-codes) to find your video's embed code ID.

```yaml
---
vimeoId: putYourIDHere
---
```

## Embed Twitch

Embedding Twitch clips requires an additional "Domain" parameter. Create a file in your `_includes` folder called `twitchPlayer.html` with this code inside:

```html
<div class="embed-container">
  <iframe
      src="https://clips.twitch.tv/embed?clip={{ include.id }}&parent={{ include.domain }}"
      height="360"
      width="640"
      frameborder="0"
      scrolling="no"
      allowfullscreen="true">
  </iframe>
</div>
```

Place this snippet inside your .md file where you want to embed your video:

```liquid
{% include twitchPlayer.html id=page.twitchId domain=page.twitchDomain %}
```

On the top of your .md file, put the Twitch video ID and domain name. You could also put the ID of the video directly.

```yaml
---
twitchId: putYourIDHere
twitchDomain: putYourDomainHere
---
```

See the [embedding Twitch clips documentation](https://dev.twitch.tv/docs/embed/video-and-clips/#non-interactive-iframes-for-clips) for more details.

## Embed Facebook

There are two types of Facebook videos/clips that you can embed: videos from the facebook feed using `<iframe>` or the newer Facebook Watch clips using the JavaScript SDK. 

#### Standard Facebook feed videos

The raw `<iframe>` method works but is buggy since its non-standard and rips out the tracking they do. This method may be preferred if you absolutely don't want Facebook to have any tracking. The raw version works but it is very buggy. There's also no easy to way extract the video ID, it's very ugly. 

Click the video until it's fullscreen which will give you the option to press the `...` settings button. Next click on `Embed`. This will open up a dialog which will show you the `<iframe>` video code.

**Note:** If you don't fullscreen the video, it will not give you the `Embed` option.

Here's an example of what the non-standard `<iframe>` may look like:

```html
<iframe src="https://www.facebook.com/plugins/video.php?href=https%3A%2F%2Fwww.facebook.com%2Falmost.co%2Fvideos%2F986032852221964%2F&width=500&show_text=false&height=500&appId" width="500" height="500" style="border:none;overflow:hidden" scrolling="no" frameborder="0" allowfullscreen="true" allow="autoplay; clipboard-write; encrypted-media; picture-in-picture; web-share" allowFullScreen="true"></iframe>
```

Instead of using a template, it may be better to manually insert the code. For this method, you would simply copy/paste that code similar to all the other `_include` files. Due to the difficulty, hassle, and weird embed behavior, there will no example of this method here. The recommendation is to use the newer Facebook Watch clips method.

#### Facebook Watch clips

**Very Important**: The newer Facebook Watch clips method requires you to import a JavaScript SDK script which very very likely does some tracking in the background but automatically handles video resizing and has smooth playback using their own CSS. If you are not okay with this then you would have to use the non-standard version.

Facebook pushed out their Watch feature on [https://www.facebook.com/watch](https://www.facebook.com/watch). This method can be used to embed any video from there. First choose a video you want to embed, then click on `Share` -> `Embed` -> `Advanced Settings`. This will open a new link. In the "Embedded Video Player Configurator", there will be a "URL of video" section which may look something like this:

```
https://www.facebook.com/pokergo/videos/1243061482783766/
```

If you already know the link of the specific video, the URL would look like this:

```
https://www.facebook.com/watch/?v=1243061482783766
```

In both of these cases, the video ID would be `1243061482783766`. 

Next create a file in your `_includes` folder called `facebookPlayer.html` with this code inside:

```html
<!-- Load Facebook SDK for JavaScript -->
<div id="fb-root"></div>
<script async defer src="https://connect.facebook.net/en_US/sdk.js#xfbml=1&version=v3.2"></script>

<!-- Your embedded video player code -->
<div 
    class="fb-video" 
    data-href="https://www.facebook.com/watch/?v={{ include.id }}"
    data-width="auto" 
    data-allowfullscreen="false">
</div>
```

**Note:** This is a ripped out version of the original JavaScript SDK code that Facebook provides which removes many unnecessary additions. If you want the original, click on `Get Code` on the advanced settings page. 

Place this snippet inside your .md file where you want to embed your video:

```liquid
{% include facebookPlayer.html id=page.facebookId %}
```

On the top of your .md file, put the Facebook video ID. You could also put the ID of the video directly.

```yaml
---
facebookId: 1243061482783766 
---
```

Facebook uses their own video parameters, for more information take a look at the [Embedded Video & Live Video Player](https://developers.facebook.com/docs/plugins/embedded-video-player/) documentation.

## Embed Streamable

Create a file in your `_includes` folder called `streamablePlayer.html` with this code inside:

```html
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

```liquid
{% include streamablePlayer.html id=page.streamableId %}
```

On the top of your .md file, put the Streamable video ID. You could also put the ID of the video directly.

```yaml
---
streamableId: putYourIDHere
---
```

To find your embed video ID use [Streamable's free online tool](https://streamable.com/embed-video)

## Embed Google Drive

**Recommendation:** Upload your video to [YouTube instead](#embed-youtube) since it has better built in video player functionality.

Embedding Google Drive videos have additional steps.

1. For the desired video, change the link sharing setting to `On - Anyone with the link`. This will make the video accessible to anyone who has the link as no sign-in is required.
  
   **Important**: If you do not change the video setting to this option, your video will not show.
  
2. Double click the video to show the preview. Click the setting options and select "Open in new window". Now click on the setting option again and select "Embed item". The iframe code should appear. For example:

```html
<iframe src="https://drive.google.com/file/d/1EC8BnjJMon-vqy-UhLKk9sf_oukZzEbP/preview"></iframe>
```

`1EC8BnjJMon-vqy-UhLKk9sf_oukZzEbP/preview` would be your video ID.

**Note**: Right clicking the video will not bring up the embed option. You must open the video in a new window.

Create a file in your `_includes` folder called `googleDrivePlayer.html` with this code inside:

```html
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

```liquid
{% include googleDrivePlayer.html id=page.driveId %}
```

On the top of your .md file, put the Google Drive video ID. You could also put the ID of the video directly.

```yaml
---
driveId: putYourIDHere
---
```

## Additional support

### Embed 20Detik

Create a file in your `_includes` folder called `20detikPlayer.html` with this code inside:

```html
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

```liquid
{% include 20detikPlayer.html id=page.detikId %}
```

On the top of your .md file, put the Detik video ID. You could also put the ID of the video directly.

```yaml
---
detikId: 190130051
---
```

### Embed Dailymotion

Create a file in your `_includes` folder called `dailymotionPlayer.html` with this code inside:

```html
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

```liquid
{% include dailymotionPlayer.html id=page.dailymotionId %}
```

On the top of your .md file, put the Dailymotion video ID. You could also put the ID of the video directly.

```yaml
---
dailymotionId: x2btuie
---
```

### Embed Vidio

Create a file in your `_includes` folder called `vidioPlayer.html` with this code inside:

```html
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

```liquid
{% include vidioPlayer.html id=page.vidioId %}
```

On the top of your .md file, put the Vidio video ID. You could also put the ID of the video directly.

```yaml
---
vidioId: 1671743
---
```

### Embed LINE Today

LINE Today contents are served in different countries so another `country` parameter (to be filled with a 2-letter country code) is needed. Here's all the supported country codes (case-insensitive)

* `hk` - Hong Kong
* `id` - Indonesia
* `th` - Thailand
* `tw` - Taiwan

Create a file in your `_includes` folder called `linetodayPlayer.html` with this code inside:

```html
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

```liquid
{% include linetodayPlayer.html id=page.linetodayId country=page.countryId %}
```

On the top of your .md file, put the LINE Today video and country ID. You could also put the IDs directly.

```yaml
---
linetodayId: abcdefg 
countryId: hk
---
```

## Responsive Videos

For responsive videos that automatically resize with changing window sizes, add in `video-embed.css`.

```css
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

Name              | Type    | Description
:---------------- | :------ | :----------
`allowfullscreen` | boolean | If `true`, the player can go full screen.
`height`          | integer | Height of the embedded window, in pixels.
`width`           | integer | Width of the embedded window, in pixels.
`scrolling`       | boolean | Indicates when the browser should provide a scroll bar (or other scrolling device) for the frame. Recommended: `no`.
`src`             | string  | The video/clip source URL link.
`autoplay`        | boolean | If `true`, the video starts playing automatically, without the user clicking play. The exception is mobile devices, on which video cannot be played without user interaction. Default: `true`.
`muted`           | boolean | Specifies whether the initial state of the video is muted. Default: `false`.
`time`            | 1h2m3s  | Time in the video where playback starts. Specifies hours, minutes, and seconds. Default: 0h0m0s (the start of the video).

## Full example

```markdown
---
youtubeId: putYourIDHere
vimeoId: putYourIDHere
twitchId: putYourIDHere
twitchDomain: putYourDomainHere
facebookId: putYourIDHere
streamableId: putYourIDHere
driveId: putYourIDHere
detikId: putYourIDHere
dailymotionId: putYourIDHere
vidioId: putYourIDHere
linetodayId: putYourIDHere
countryId: putYourIDHere
---

## Embed Youtube

<!---
Include this next line in your .md for Youtube videos, make sure to put your video ID up there!

Example:     youtubeId: lDi9uFcD7XI
-->

{% include youtubePlayer.html id=page.youtubeId %}

## Embed Vimeo

<!---
Include this next line in your .md file for Vimeo videos, make sure to put your video ID up there!

Example:     vimeoID: 22439234
-->

{% include vimeoPlayer.html id=page.vimeoId %}

## Embed Twitch

<!---
Include this next line in your .md file for Twitch videos, make sure to put your video ID and domain up there!

Example:     twitchId: GrotesqueArbitraryGullPupper
             twitchDomain: www.nathan-lam.com
-->

{% include twitchPlayer.html id=page.twitchId domain=page.twitchDomain %}

## Embed Facebook

<!---
Include this next line in your .md file for Facebook videos, make sure to put your video ID up there!

Example:     facebookId: 1243061482783766 
-->

{% include facebookPlayer.html id=page.facebookId %}

## Embed Streamable

<!---
Include this next line in your .md file for Streamable videos, make sure to put your video ID up there!

Example:     streamableId: s9ijg 
-->

{% include streamablePlayer.html id=page.streamableId %}

## Embed Google Drive

<!---
Include this next line in your .md file for Google Drive videos, make sure to put your video ID up there!

Example:     driveId: 0B7L_dMcaZknxVTRndmdSQ0F5OFE/preview
-->

{% include googleDrivePlayer.html id=page.driveId %}

## Embed 20Detik

<!---
Include this next line in your .md file for 20Detik videos, make sure to put your video ID up there!

Example:     detikId: 190130051
-->

{% include 20detikPlayer.html id=page.detikId %}

## Embed Dailymotion

<!---
Include this next line in your .md file for Dailymotion videos, make sure to put your video ID up there!

Example:     dailymotionId: x2btuie
-->

{% include dailymotionPlayer.html id=page.dailymotionId %}

## Embed Vidio

<!---
Include this next line in your .md file for Vidio videos, make sure to put your video ID up there!

Example:     vidioId: 1671743
-->

{% include vidioPlayer.html id=page.vidioId %}

## Embed LINE Today

<!---
Include these next lines in your .md file for LINE Today videos, make sure to put your video and country ID up there!

Example:     linetodayId: abcdefg 
             countryId: hk
-->

{% include linetodayPlayer.html id=page.linetodayId country=page.countryId %}
```
