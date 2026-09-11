# jekyll-embed-video

Embed YouTube, Vimeo, Twitch, Facebook, Instagram, Twitter, TikTok, Streamable, Google Drive videos/clips and more in Jekyll webpages without a plugin. If you are hosting your webpage using GitHub pages, you can't use third party plugins. Here is a method to use "includes" instead of plugins.

See the raw text in `example.md` for a complete example. Remember to add in [video-embed.css](https://github.com/nathancy/jekyll-embed-video/blob/master/video-embed.css) for [responsive videos](#responsive-videos) that automatically resize with changing window dimensions.

## Demo

<http://www.nathan-lam.com/projects/jekyll-embed-video>

## Table of Contents

* [Embed YouTube](#embed-youtube)
* [Embed Vimeo](#embed-vimeo)
* [Embed Twitch](#embed-twitch)
* [Embed Facebook](#embed-facebook)
* [Embed Instagram](#embed-instagram)
* [Embed Twitter](#embed-twitter)
* [Embed TikTok](#embed-tiktok)
* [Embed Streamable](#embed-streamable)
* [Embed Google Drive](#embed-google-drive)
* [Additional support for 20Detik, Dailymotion, Vidio, and LINE Today](#additional-support)
* [Responsive Videos](#responsive-videos)
* [Iframe Attributes](#iframe-attributes)
* [Full Example](#full-example)

## Embed YouTube

To find the YouTube video ID, click on the desired video to embed. You will get a URL like this:

```
https://www.youtube.com/watch?v=lDi9uFcD7XI
```

The YouTube video ID would be `lDi9uFcD7XI`

Next create a file in your `_includes` folder called `youtubePlayer.html` with this code inside:

```html
<div class="embed-container">
  <iframe
      src="https://www.youtube.com/embed/{{ include.id }}"
      width="700"
      height="480"
      frameborder="0"
      allowfullscreen="true">
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

To find the Vimeo video ID, click on the desired video to embed. You will get a URL like this:

```
https://vimeo.com/22439234
```

The Vimeo video ID would be `22439234`

Next create a file in your `_includes` folder called `vimeoPlayer.html` with this code inside:

```html
<div class="embed-container">
  <iframe
      src="https://player.vimeo.com/video/{{ include.id }}"
      width="700"
      height="480"
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

To find the Twitch video ID, click on the desired clip to embed. You will get a URL like this:

```
https://clips.twitch.tv/StylishChillyTubersDancingBaby
```

The Twitch video ID would be `StylishChillyTubersDancingBaby`

Create a file in your `_includes` folder called `twitchPlayer.html` with this code inside:

```html
<!-- Used to embed Twitch videos -->

<div class="embed-container" id="twitch-{{ include.id }}"></div>
<script>
  (function() {
    var hostname = window.location.hostname || 'localhost';
    var iframe = document.createElement('iframe');
    iframe.src = "https://clips.twitch.tv/embed?clip={{ include.id }}&parent=" + hostname;
    iframe.frameBorder = "0";
    iframe.scrolling = "no";
    iframe.width = "700";
    iframe.height = "480";
    iframe.allowFullscreen = true;
    document.getElementById("twitch-{{ include.id }}").appendChild(iframe);
  })();
</script>
```

Place this snippet inside your .md file where you want to embed your video:

```liquid
{% include twitchPlayer.html id=page.twitchId %}
```

On the top of your .md file, put the Twitch video ID. You could also put the ID of the video directly.

```yaml
---
twitchId: putYourIDHere
---
```

**Note**: If you are running your website on a `localhost` server, you might get a `clips.twitch.tv refused to connect` error depending on your local setup. But it should properly display on the live production site.

See the [embedding Twitch clips documentation](https://dev.twitch.tv/docs/embed/video-and-clips/#non-interactive-iframes-for-clips) for more details.

## Embed Facebook

To embed a Facebook video, you first need the video ID. You can find this by clicking on the desired video. The URL will look something like this:

```
https://www.facebook.com/watch/?v=1243061482783766
```

Or a direct post link like this:

```
https://www.facebook.com/pokergo/videos/1243061482783766/
```

In both of these cases, the video ID would be `1243061482783766`.

Next create a file in your `_includes` folder called `facebookPlayer.html` with this code inside:

```html
<!-- NOTE: We don't use the CSS embed-container for Facebook because it handles its own sizing. -->
<iframe 
  src="https://www.facebook.com/plugins/video.php?href=https%3A%2F%2Fwww.facebook.com%2Ffacebook%2Fvideos%2F{{ include.id }}%2F&show_text=0&width=700" 
  width="700" 
  height="394" 
  style="border:none;overflow:hidden; display:block; margin:auto;" 
  scrolling="no" 
  frameborder="0" 
  allowTransparency="true" 
  allowFullScreen="true"
  allow="autoplay; clipboard-write; encrypted-media; picture-in-picture; web-share">
</iframe>
```

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

For more information take a look at the [Embedded Video & Live Video Player](https://developers.facebook.com/docs/plugins/embedded-video-player/) documentation.

## Embed Instagram

To find the Instagram video/reel/post ID, click on the desired post to embed. You will get a URL like this:

```
https://www.instagram.com/p/CgdzCoMoUBJ/
```

The Instagram ID would be `CgdzCoMoUBJ`

Next create a file in your `_includes` folder called `instagramPlayer.html` with this code inside:

```html
<!-- Used to embed Instagram videos, reels, or standard posts -->

<iframe 
  src="https://www.instagram.com/p/{{ include.id }}/embed/captioned/" 
  class="instagram-media instagram-media-rendered" 
  allowtransparency="true" 
  allowfullscreen="true" 
  frameborder="0" 
  height="700" 
  style="background: white; border: 1px solid #dbdbdb; border-radius: 3px; box-shadow: none; display: block; margin: 0; min-width: 326px; padding: 0; width: 100%; max-width: 540px;" 
  scrolling="no">
</iframe>
```

Place this snippet inside your .md file where you want to embed your video:

```liquid
{% include instagramPlayer.html id=page.instagramId %}
```

On the top of your .md file, put the Instagram video/reel/post ID. You could also put the ID of the source directly.

```yaml
---
instagramId: putYourIDHere
---
```

**Note**: This is an extremely stripped down version of the built-in Instagram embed link they automatically generate when you click the `•••` then `Embed` on a post. Any tracking/information they tried to harvest has been attempted to be removed as much as possible without affecting the embed behavior.

## Embed Twitter

To find the Twitter video/post ID, click on the desired tweet to embed. You will get a URL like this:

```
https://twitter.com/SJosephBurns/status/1555282591665848320
```

The Twitter tweet ID would be `SJosephBurns/status/1555282591665848320`

Next create a file in your `_includes` folder called `twitterPlayer.html` with this code inside:

```html
<!-- NOTE: Twitter requires you to import their script. Also note, we don't 
           use the custom CSS container which we used for other providers such as
           Youtube since Twitter handles it on their own -->

<blockquote class="twitter-tweet">
  <a href="https://twitter.com/{{ include.id }}"></a>
</blockquote> 

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
```

Place this snippet inside your .md file where you want to embed your tweet:

```liquid
{% include twitterPlayer.html id=page.twitterId %}
```

On the top of your .md file, put the Twitter tweet ID. You could also put the ID of the source directly.

```yaml
---
twitterId: putYourIDHere
---
```

**Note**: This is a stripped down barebones embed method which removes unnecessary code and should work for both videos and regular Twitter text posts. For [full customization options](https://publish.twitter.com/#) you can use Twitter's embed generator to set color themes, default language, conversation toggles and much more. 

## Embed TikTok

To find the TikTok video ID, click on the desired video to embed. You will get a URL like this:

```
https://www.tiktok.com/@honeycutepet/video/7032659446199274757?lang=en
```

The TikTok ID would be `7032659446199274757`

Next create a file in your `_includes` folder called `tiktokPlayer.html` with this code inside:

```html
<!-- NOTE: TikTok requires you to import their script. Also note, we don't 
           use the custom CSS container which we used for other providers such as
           Youtube since TikTok handles it on their own -->

<blockquote 
  class="tiktok-embed" 
  data-video-id="{{ include.id }}"
  style="border-left: 0px; padding-left: 0px;"> 
  <a href="https://www.tiktok.com/"></a> 
</blockquote>

<script async src="https://www.tiktok.com/embed.js"></script>
```

Place this snippet inside your .md file where you want to embed your tweet:

```liquid
{% include tiktokPlayer.html id=page.tiktokId %}
```

On the top of your .md file, put the TikTok video ID. You could also put the ID of the source directly.

```yaml
---
tiktokId: putYourIDHere
---
```

**Note**: This is a stripped down barebones embed method which removes unnecessary code. 

## Embed Streamable

To find the Streamable video ID, click on the desired video to embed. You will get a URL like this:

```
https://streamable.com/s9ijg
```

The Streamable video ID would be `s9ijg`

Next create a file in your `_includes` folder called `streamablePlayer.html` with this code inside:

```html
<div class="embed-container">
  <iframe
      src="https://streamable.com/s/{{ include.id }}"
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
{% include streamablePlayer.html id=page.streamableId %}
```

On the top of your .md file, put the Streamable video ID. You could also put the ID of the video directly.

```yaml
---
streamableId: putYourIDHere
---
```

You could also find the embed video ID with [Streamable's free online tool](https://streamable.com/embed-video)

## Embed Google Drive

**Recommendation:** Upload your video to YouTube instead and use the [embed YouTube method](#embed-youtube) since it has better built in video player functionality.

Embedding Google Drive videos have additional steps.

1. For the desired video, change the link sharing setting to `On - Anyone with the link`. This will make the video accessible to anyone who has the link as no sign-in is required.
  
   **Important**: If you do not change the video setting to this option, your video will not show.
  
2. Look at the URL of the video or click the setting options and select "Get link". You will see a URL similar to:

```
https://drive.google.com/file/d/1EC8BnjJMon-vqy-UhLKk9sf_oukZzEbP/view?usp=sharing
```

The string between `/d/` and `/view` is your video ID: `1EC8BnjJMon-vqy-UhLKk9sf_oukZzEbP`.

Create a file in your `_includes` folder called `googleDrivePlayer.html` with this code inside:

```html
<div class="embed-container">
  <iframe
      width="700"
      height="480"
      src="https://drive.google.com/file/d/{{ include.id }}/preview"
      frameborder="0"
      allowfullscreen="true">
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
      allowfullscreen="true">
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
      allowfullscreen="true"
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
facebookId: putYourIDHere
instagramId: putYourIDhere
twitterId: putYourIDHere
tiktokId: putYourIDHere
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
Include this next line in your .md file for Twitch videos, make sure to put your video ID up there!

Example:     twitchId: GrotesqueArbitraryGullPupper
-->

{% include twitchPlayer.html id=page.twitchId %}

## Embed Facebook

<!---
Include this next line in your .md file for Facebook videos, make sure to put your video ID up there!

Example:     facebookId: 1243061482783766 
-->

{% include facebookPlayer.html id=page.facebookId %}

## Embed Instagram

<!---
Include this next line in your .md file for Instagram videos/reels/posts, make sure to put your video ID up there!

Example:     instagramId: CgdzCoMoUBJ 
-->

{% include instagramPlayer.html id=page.instagramId %}

## Embed Twitter

<!---
Include this next line in your .md file for Twitter videos/posts, make sure to put your video ID up there!

Example:     twitterId: SJosephBurns/status/1555282591665848320 
-->

{% include twitterPlayer.html id=page.twitterId %}

## Embed TikTok

<!---
Include this next line in your .md file for TikTok videos, make sure to put your video ID up there!

Example:     tiktokId: 7101489125244652806 
-->

{% include tiktokPlayer.html id=page.tiktokId %}

## Embed Streamable

<!---
Include this next line in your .md file for Streamable videos, make sure to put your video ID up there!

Example:     streamableId: s9ijg 
-->

{% include streamablePlayer.html id=page.streamableId %}

## Embed Google Drive

<!---
Include this next line in your .md file for Google Drive videos, make sure to put your video ID up there!

Example:     driveId: 0B7L_dMcaZknxVTRndmdSQ0F5OFE
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

## Contributing 

Feel free to open an issue or pull request ticket if any of the existing video embed methods break or if there are any other requests to support new video stream providers