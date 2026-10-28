# Real-Time Communication Calls

Scope: Task 4 (the calling and collaboration features), not the separate
Trello/Asana-style project-board task.

## Current status

- [x] Authenticated Socket.IO signaling for incoming calls, accept/decline,
  offers, answers, ICE candidates, and call end.
- [x] One-to-one audio and video calls with mute, speaker, camera, and elapsed
  call time controls.
- [x] Local/remote video rendering and call audio routing integration.
- [x] Request up to 720p at 30 FPS where supported and leave video sender
  bitrate adaptive, while retaining a bounded audio bitrate.
- [x] Start the native call audio session before requesting WebRTC media and
  report when no microphone track is created.
- [x] Add group-call offer/answer/ICE routing and a participant video layout
  using a peer-to-peer mesh.
- [x] Add a call-screen link to the existing encrypted chat attachment
  composer, while keeping the call active in a minimized overlay.
- [x] Keep active calls connected when minimizing or using the Android back
  action, and route the in-call chat button to the existing conversation.
- [x] Show local camera preview during calls and avatar fallbacks when local or
  remote cameras are off; synchronize remote camera state through authenticated
  call signaling.
- [x] Keep call-control icons and labels high-contrast without black foreground
  controls.
- [x] Add an in-call synchronized freehand whiteboard with authenticated
  participant checks and bounded stroke payloads.
- [x] Account authentication and encrypted chat/file-sharing flows exist
  outside the call screen.
- [x] Modernize the call UI with gradient backgrounds, pulse animations for
  ringing states, circular control buttons, improved typography and spacing,
  status dot indicators, and polished minimized overlay.
- [x] Keep WebRTC quality metrics available as developer diagnostics without a
  Stats button in the normal call UI.
- [x] Implement bounded browser screen capture with getDisplayMedia, safe
  sender replacement, browser stop-sharing integration, and camera restoration.
- [x] Add automated call-flow tests covering call setup, acceptance, decline,
  ending, offer/answer exchange, ICE candidate handling, participant lifecycle,
  media toggles, and duplicate signaling events.

## Remaining work

- [ ] Verify two-way microphone audio on physical Android and iOS devices,
  including Bluetooth, speaker, earpiece, permission-denied, and app-resume
  cases.
- [ ] Verify group calls with three or more real devices, including a
  participant joining after another participant has already accepted.
- [ ] Verify minimizing a call, sending an encrypted attachment from the chat,
  and returning to the call on Android and iOS.
- [ ] Measure video frame rate, resolution, packet loss, and round-trip time on
  real devices and weak networks; tune quality from those measurements.
- [ ] Verify Android screen sharing, system consent, foreground notification,
  and track cleanup on a physical device. iOS still requires a ReplayKit
  broadcast extension and is not enabled.
- [ ] Verify whiteboard synchronization and clear behavior on multiple devices.
- [x] Document the media security model: WebRTC uses DTLS-SRTP transport
  encryption; additional app-level media E2EE is not implemented.

## Before release

- [ ] Configure and verify production TURN credentials and relay reachability.
- [ ] Test calls between Android, iOS, and web across Wi-Fi and mobile networks.
- [ ] Rebuild and reinstall native development builds after native call-module
  changes.

## Group-call scaling

Group calls use a full peer-to-peer mesh: every participant maintains a
connection to every other participant. This avoids introducing an SFU, but
each participant's upload bandwidth and device load grow with the group size.
There is no server-side participant cap; use real-device/network measurements
to decide when an SFU becomes necessary.
