# GDIndex

![preview](https://i.imgur.com/ENkZwCU.png)

[繁體中文](README.zhtw.md)
[简体中文](README.zh.md)

> GDIndex is similar to [GOIndex](https://github.com/donwa/goindex).
> It allows you to deploy a "Google Drive Index" on CloudFlare Workers along with many extra features
>
> By the way, instead of modify from GOIndex, this is a total rewrite

[Demo](https://gdindex-demo.maple3142.workers.dev/)

## Difference between GOIndex and GDIndex

-   Frontend is based on Vue.js
-   Image viewer doesn't require opening new page
-   Video player support subtitles(Currently only srt is supported)
-   Online PDF, EPUB reader
-   No directory-level password protection(.password)
-   Support Http Basic Auth
-   Support multiple drives(personal, team) without changing server's code
-   Support Aria2 download

## Usage

### Simple and automatic way

Go [https://gdindex-code-builder.glitch.me/](https://gdindex-code-builder.glitch.me/), and follow its instructions.

### Manual way

1. Install [rclone](https://rclone.org/)
2. Setup your Google Drive: https://rclone.org/drive/
3. Run `rclone config file` to find your `rclone.conf` location
4. Find `refresh_token` in your `rclone.conf`, and `root_folder_id` too(optionally).
5. Copy the content of [worker/dist/worker.js](worker/dist/worker.js) to CloudFlare Workers.
6. Fill `refresh_token`, `root_folder_id` and other options on the top of the script.
7. Deploy!

### Enabling download with Aria2

1. Add config `download_aria2: true` to your `worker.js`:
    ```
	default_root_id: '...',
	client_id: '...',
	client_secret: '...',
	refresh_token: '...',
    ...
	download_aria2: true
    ```
2. Redeploy, now you should see "Download with Aria2" and "Aria2 RPC Settings" beyond file list
3. Fill your aria2 connection info in "Aria2 RPC Settings"
4. Go to where you want to download and click "Download with aria2", which will add downloads for you!
