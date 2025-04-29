# Dual HD server demo
This is an example server setup demonstrating real-time cropping of a [Dual HD](https://dualhd.org/) stream using [Mediamtx](https://github.com/bluenviron/mediamtx).

## What is Dual HD?
Dual HD is a video standard that contains both horizontal and vertical view within a single frame. Dual HD 2640, used in this example, contains Full HD (1920×1080) video for horizontal and 720p (720x1280) for vertical video.

Dual HD is designed for streaming across platforms like Twitch/YouTube (horzontal) and TikTok/Instagram (vertical).

For more on the Dual HD format, visit [dualhd.org](https://dualhd.org/).

## Purpose of this repository
This repo is useful for testing and demonstrating Dual HD and it provides a working example of:

- Simulating a Dual HD livestream from a PNG image to Mediamtx server using FFmpeg
- Automatically cropping the Dual HD video into horizontal and vertical outputs, that can be read via RTMP

## Prerequisites
Docker Desktop (or Docker CLI + Docker Compose)

## How to run this example

**1\. Clone this repository and start the server**

```sh
docker compose up
```
This will start a MediaMTX server with routing rules for horizontal and vertical crops.


**2\. Simulate a live Dual HD stream**

```sh
ffmpeg -loop 1 -framerate 30 -i dualhd2640.png \
    -c:v libx264 -preset veryfast -r 30 -f flv rtmp://localhost:1935/dualhd2640
```
This turns dualhd2640.png into a 30fps live stream.


**3\. Watch the output streams**

You can view the output streams using [VLC](https://www.videolan.org/vlc/) or similar software:
  - Horizontal view: rtmp://localhost:1935/horizontal
  - Vertical view: rtmp://localhost:1935/vertical