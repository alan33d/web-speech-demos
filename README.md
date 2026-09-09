# Web Speech API Demos

A collection of interactive demonstrations and prototype implementations for proposed enhancements to the [W3C Web Speech API](https://webaudio.github.io/web-speech-api/).

## Demos

* **[Live Meeting & Recording Caption Sync Demo](https://alan33d.github.io/web-speech-demos/live_meeting_recording_demo.html)**: Demonstrates zero-delay live in-call captions paired with synchronized WebVTT caption tracks and interactive "click-to-seek" transcript navigation for post-meeting recording playback using `speechStartTime` and `speechEndTime`.
* **[WebRTC Caption Playout Delay Sync Demo](https://alan33d.github.io/web-speech-demos/webrtc_caption_sync_test.html)**: Demonstrates frame-accurate lip-sync between live camera feeds and speech recognition captions using acoustic timestamps and a playout delay buffer.

---

### 1. Live Meeting & Recording Caption Sync (`live_meeting_recording_demo.html`)

This demo illustrates Example 2 from the [SpeechRecognitionResult Timestamps Explainer](https://github.com/WebAudio/web-speech-api/blob/main/explainers/speech-recognition-result-timestamps.md):

* **Problem:** In live video conferencing (such as Google Meet), captions must appear immediately on screen with zero delay to minimize perceived conversational lag. However, to synchronize subtitles with the meeting recording afterwards, the application needs the exact acoustic boundaries of each spoken sentence.
* **Solution:** Captions display immediately upon event dispatch during the call (with a reading persistence window). Simultaneously, `speechStartTime` and `speechEndTime` are archived into the meeting transcript to create synchronized WebVTT cues (`VTTCue`) for the recorded video track.
* **Features:**
  * Real-time camera & microphone capture with live caption overlay.
  * Meeting recorder that packages video alongside transcription results.
  * Post-meeting replay player with frame-accurate WebVTT captions synchronized to speech audio.
  * Interactive **"click-to-seek" transcript navigation**: Clicking any transcript row or timestamp link instantly jumps recorded video playback to that spoken sentence with active row synchronization.

---

### 2. Live Video Caption Playout Delay Sync (`webrtc_caption_sync_test.html`)

* **Problem:** In real-time speech recognition, ASR processing latency means results arrive after speech has already ended. Without a buffer, captions cannot synchronize with the speaker's mouth in a live video stream.
* **Solution:** Video playout is buffered by a small delay (e.g. 1.5 seconds), allowing captions to appear on screen at the exact frame corresponding to the acoustic speech bounds.
* **Features:**
  * Side-by-side view comparing unbuffered live camera feed vs. buffered playout feed.
  * Captions light up on the buffered feed at the exact moment the speaker talks and clear when speech ends.

---

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
```

## Related Links

* **W3C Issue:** [WebAudio/web-speech-api#191](https://github.com/WebAudio/web-speech-api/issues/191)
* **Spec PR:** [WebAudio/web-speech-api#192](https://github.com/WebAudio/web-speech-api/pull/192)
* **Explainer PR:** [WebAudio/web-speech-api#205](https://github.com/WebAudio/web-speech-api/pull/205)
* **ChromeStatus:** [Web Speech API Timestamps (#5811907077472256)](https://chromestatus.com/feature/5811907077472256)
* **Reference Demo:** [Speech Latency Demo](https://michaelwasserman.github.io/web-speech-demos/speech_latency_h.html) (by @msw)
