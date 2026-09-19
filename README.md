# Ivan Music - update channel

Release-assets-only repository. The app polls two FIXED urls:

- manifest: https://github.com/IvanXxxxyyuffff/ivan-music/releases/latest/download/update.json
- package : https://github.com/IvanXxxxyyuffff/ivan-music/releases/latest/download/ivan-music.apk

Asset names repeat every release on purpose -- that is what makes
`releases/latest/download/<name>` resolve. Version lives in the tag.
