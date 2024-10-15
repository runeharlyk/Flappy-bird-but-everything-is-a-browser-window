# 🐦 Flappy bird, but everything is a browser window

I mean it pretty self explanatory - Every object is its own browser window.

You play by clicking on the bird or background. Though by using background a flicker might occur when the windows regain focus.

## 🎮 [Demo](https://developer.runeharlyk.dk/Explore/files/flappy-bird/)

<a href="https://developer.runeharlyk.dk/Explore/files/flappy-bird/">
<img src="images/demo.gif" />
</a>

> [!TIP]
> Browser permission for "Popups and redirects" are required

## 🤔 How does it work?

When a new game it started 3 browser windows are opened. One for:

- Bird
- Top pipe
- Bottom pipe

They get initialized with a id, xy position, width, height, parent width, parent height and size of non viewport screen real estate.
This is passed using their url [hash](https://developer.mozilla.org/en-US/docs/Web/API/Location/hash).

### 💬 Cross window communication

The four window now all connect to the same [broadcast channel](https://developer.mozilla.org/en-US/docs/Web/API/Broadcast_Channel_API), where position data is shared.

These updates includes the id of the receiver and their new xy position, width and height.

### 🧭 Coordinate synchronization

To ensure the background in the same coordinate system between windows a fusion of
[screenLeft](https://developer.mozilla.org/en-US/docs/Web/API/Window/screenLeft),
[screenTop](https://developer.mozilla.org/en-US/docs/Web/API/Window/screenTop),
[outerHeight](https://developer.mozilla.org/en-US/docs/Web/API/Window/outerHeight),
[innerHeight](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerHeight) is used.

A popup does not include all the usual browser toolbar stuff and is thereby a bit taller. We offset this by calculating this height using
`outerHeight - innerHeight`.
