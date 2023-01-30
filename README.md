# Hypno.exe

At its heart Hypno.exe is an easy to use, cross-platform tool for creating and sharing hypnotic audio-visual experiences. I built it with the following key points in mind:

- UX as intuitive as "drag and drop", if not literally so.
- Created experiences should be easily sharable between users of the application.
- Created experiences should be trustless: allow anyone to quickly and easily see the content of an experience in a non-hypnotic context. No sneaky triggers or undesired content/themes.
- Support as many platforms as possible: Windows, Android, Linux, as well as VR/AR for desktop, mobile, and standalone. Mac/iOS is harder, but not impossible. Take it up with Steve Jobs' ghost.

The existing vertical slice has achieved these, to a point, however some architectural choices made early on have limited what can be achieved with more advanced content, and as such I will be rebuilding it from the ground up with these more advanced capabilities in mind, namely:

- Importing of custom audio, images, and video, for playback in experiences. This is already in the current version, however it is unstable due to aforementioned foundational design choices.
- The ability to export video of experiences, both in 2D and 3D for VR playback.
- True multiplayer support: Control the experience inside a VR headset or mobile VR from a different computer over a local network.
- Integration of external tools: buttplug.io, pretty much anything open-source that I can do.
- No doubt more.

