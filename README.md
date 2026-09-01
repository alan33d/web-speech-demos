# Web Speech API Demos

A collection of interactive demonstrations and prototype implementations for proposed enhancements to the [W3C Web Speech API](https://webaudio.github.io/web-speech-api/).

## Demos

* **[WebRTC Caption Playout Delay Sync Demo](https://alan33d.github.io/web-speech-demos/webrtc_caption_sync_test.html)**: Demonstrates frame-accurate lip-sync between live camera feeds and speech recognition captions using acoustic timestamps (`speechStartTime` / `speechEndTime`) and a playout delay buffer.

### Live Video Caption Playout Delay Sync (`webrtc_caption_sync_test.html`)

This demo illustrates Example 2 from the [SpeechRecognitionResult Timestamps Explainer](https://github.com/WebAudio/web-speech-api/blob/main/explainers/speech-recognition-result-timestamps.md):

* **Problem:** In real-time speech recognition, ASR processing latency means results arrive after speech has already ended. Without a buffer, captions cannot synchronize with the speaker's mouth in a live video stream.
* **Solution:** Video playout is buffered by a small delay (e.g. 1.5 seconds), allowing captions to appear on screen at the exact frame corresponding to the acoustic speech bounds.
* **Features:**
  * Side-by-side view comparing unbuffered live camera feed vs. buffered playout feed.
  * Captions light up on the buffered feed at the exact moment the speaker talks and clear when speech ends.

## Testing with Chrome Canary

To test with native Chromium timestamp support:

```bash
# macOS:
"/Applications/Google Chrome Canary.app/Contents/MacOS/Google Chrome Canary" \
  --enable-blink-features=WebSpeechTimestamps \
  --enable-features=OnDeviceSpeechRecognition,Soda

# Linux:
google-chrome-canary \
  --enable-blink-features=WebSpeechTimestamps \
  --enable-features=OnDeviceSpeechRecognition,Soda
