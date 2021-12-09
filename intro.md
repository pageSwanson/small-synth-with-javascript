## audio and programming
- programming languages have historically been suplemented with libraries for computer audio
- someone figures out some code that makes requests for the computer to produce audio
  - then they make that code available as a series of possibilities for the programmer
  - i.e. you can reference the audio output of the computer using this 'stream'
- furthermore - someone also usually makes a library for generating signals that the computer can output
  - instead of forcing the programmer to painstakingly provide each piece of the audio
  - i.e. you can call this function with some parameters and a way to add to the stream to make a beep
  - this would typically be called an _engine_
- examples of 
  - for C: [portaduio](http://portaudio.com/), [libsoundio](http://libsound.io/)
  - for Python: [pyo](https://github.com/belangeo/pyo), [pydub](https://github.com/jiaaro/pydub)

## using JavaScript - the [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
- the contemporary JavaScript way of making/producing audio in the web browser
  - the browser knows how to talk to the computer to send audio to your speaker
  - the web audio api is an interface for the browser that lets you do this easily
  - it also gives you ways to work with audio like you would with a synthesizer
- most JavaScript is run in the web browser
  - browser developers try to think of common resources and needs that javascript developers might have
  - they build APIs for JavaScript, and propose that modern browsers implement them so that developers can use them 'out of the box'
  - this means that JavaScript has access to many built-in libraries within the browser
    - no need to add extra JavaScript code to your project

## the Audio Context
- for the following - open the 'console' in your web browser
  - paste in the subsequent commands as you go, and run each one at a time
  - tip: for the Web Audio context to work - you'll need to perform a gesture, like a click, on the page before starting

- the Web Audio api uses a 'context' to set you up for making sounds in the browser
- once you have a context - you can make requests for different types of audio processes
  - this is also the way we'll reference all of the different _engine_ options (oscillators, filters, effects)
  ```javascript
  var context = new AudioContext();
  ```
- we can then use one of the sources provided by the API and set them up in the context
  ```javascript
  var oscillator = context.createOscillator();
  oscillator.frequency.value = 216;
  
  ```
- when we've setup an audio source, we can connect it to the context so that we hear the audio
  - once it's connected - start it to produce the output

  ```javascript
  oscillator.connect( context.destination ); 
  oscillator.start();
  ```
- if we need to suddenly stop the audio - we can use 'suspend' and 'resume'

  ```javascript
  context.suspend();
  context.resume();
  ```

## small amount to fiddle
- the following snippet sets up a context, a node, connects it to the audio 'output', and starts to play
- then it regularly updates the properties of the oscillator to change its behavior.. randomly
  - frequency is updated randomly
  - every second or so - also changes randomly!

```javascript
var ctx = new AudioContext(); 

var o = ctx.createOscillator(); o.frequency.value = 214; o.connect( ctx.destination ); o.start(); 

var speed = 500;
var random = (max) => Math.floor(Math.random() * Math.floor(max));

var updateProperties = () => { o.frequency.value = random(1300); speed = random(1000); change = setTimeout(updateProperties, speed); }

var change = setTimeout(updateProperties, speed);
```

## references
- https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Basic_concepts_behind_Web_Audio_API
- https://github.com/zenon/MinimalWebAudio
- https://codereview.stackexchange.com/questions/203209/random-tone-generator-using-web-audio-api
