# README

> 「網站未來要新加功能，讓客戶可以上傳經驗分享影片，預計儲存在 Cloud Storage，  
> 要如何設定可以在網站內，嵌入畫面就開始撥放影片，而不需要下載後從 local 播放。」

這是某個客戶的需求，有提到 GCS 上面的影片，想要在網站中可以自動撥放。  
如果只是要影片權限，大概有兩種做法。

1. 設定 public。
2. 設定 origin，多一層安全保護讓只有該網站可以存取影片。

另外，可以再加 CDN，減輕網路流量壓力

--

至於想要方便操作 GCS 的檔案，比如用 S3browser 這種工具，  
那我只能說，目前 google storage 和開源工具的相容性不夠好，  
畢竟是 AWS S3 先出來的，所以大部分的工具都是和 S3 API 整合得比較好。

--

所以就想說學一下，怎麼做在前端的網頁裡面，怎麼做可以控制影片自動撥放。  
順便科普一下每種影片類型。  
但我覺得客戶說在網路上播放不用下載到機器上，那應該只需要直接讀取 Cloud Storage 的影片就行了。

---

## target

- video format
  - AVI(Audio Video Interleave)
  - FLV(Flash Video Format)
  - WMV(Windows Media Video)
  - MOV(Apple QuickTime Movie)
  - MP4(Moving Pictures Expert Group 4)
- gif: 這應該原本就會自動撥放XD
- streaming video?
  - m3u8

mp4 轉換成 wmv 的結果失敗。  
error code 為 `too many channels got 6 need 2 or fewer. Conversion failed`。  
總之我也不懂，先這樣 XD~ 把一些 stackoverflow 紀錄一下。

- [Error using ffmpeg to convert mkv to avi on Windows 7 - Super User](https://superuser.com/questions/371389/error-using-ffmpeg-to-convert-mkv-to-avi-on-windows-7)
- [Converting 6 audio channels to 2 in ffmpeg - Stack Overflow](https://stackoverflow.com/questions/4790818/converting-6-audio-channels-to-2-in-ffmpeg)

---

## sample video

因為要找各種格式的檔案還沒麻煩的，  
所以我就找 mp4 格式，然後轉不同的 format。

- [Download Sample Videos / Dummy Videos For Demo Use](https://sample-videos.com/)
- [Sample MP4 files download | File Examples Download](https://file-examples.com/index.php/sample-video-files/sample-mp4-files/)。這個不錯，缺點是沒聲音。

--

## reference

- google keyword: video autoplay html
- [HTML video autoplay Attribute](https://www.w3schools.com/tags/att_video_autoplay.asp)
- [Free HLS m3u8 URLs for Testing HLS Players [Updated] - OTTVerse](https://ottverse.com/free-hls-m3u8-test-urls/)
- [How to animate GIFs in HTML document? - Stack Overflow](https://stackoverflow.com/questions/38309480/how-to-animate-gifs-in-html-document)
- [Amazon Interactive Video Service Player: Video.js Integration - Amazon Interactive Video Service](https://docs.aws.amazon.com/ivs/latest/userguide/player-videojs.html)。aws ivs 有文件說明如何內嵌 m3u8 串流影片檔案。

--

- MIME type
  - [MIME 類別 (IANA 媒體類別) - HTTP | MDN](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
  - [Correct MIME types for serving video files - Encoding.com HelpEncoding.com Help](https://help.encoding.com/knowledge-base/article/correct-mime-types-for-serving-video-files/)

video 的 MIME type: 有很多種影音格式，每種格式可以想像成一個影音容器，去容納不同的影像及聲音。

--

關於影音格式

- [Day02 影音檔格式、OGG 與 WebM - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10202195)。理解 OGG 和 WEBM 的差異。
- [HTML5的Video標籤(1) - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天](https://ithelp.ithome.com.tw/articles/10102831)。說明何謂編譯解碼器。

--

- [HTML Multimedia](https://www.w3schools.com/html/html_media.asp)

有些影音格式不支援 web browser，或是需要引入其他的播放器才可以播放。

---

## END
