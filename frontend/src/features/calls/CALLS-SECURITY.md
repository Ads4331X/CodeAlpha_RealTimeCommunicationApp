# Call Media Security

## Transport Encryption

WebRTC mandates **DTLS-SRTP** for all media streams. Every audio and video
packet exchanged between peers is encrypted at the transport layer. This is
handled entirely by the WebRTC stack — neither the app nor the signaling
server can read the media content.

## Signaling Security

- Socket.IO connections are authenticated with JWT tokens verified on the
  server (see `socket.ts` middleware).
- The server validates conversation membership (`ensureMember`) before allowing
  call initiation, acceptance, decline, and ending.
- Offer/answer/ICE forwarding checks that the sender is a valid call
  participant (`callerId` or `acceptedBy` member) and that neither the sender
  nor receiver has left the call.
- Whiteboard stroke payloads are validated server-side: stroke ID length,
  hex color format, point count bounds (1–500), and coordinate ranges (0–1).

## TURN Credentials

- STUN/TURN server URLs and TURN credentials are loaded from environment
  variables (`EXPO_PUBLIC_STUN_URLS`, `EXPO_PUBLIC_TURN_URLS`,
  `EXPO_PUBLIC_TURN_USERNAME`, `EXPO_PUBLIC_TURN_CREDENTIAL`).
- The `.env` file is gitignored and never committed.
- Invalid URL schemes are ignored. TURN is only added when at least one TURN
  URL, a username, and a credential are all configured.
- `hasTurnCredentials()` is used to explain relay failures to users; it does
  not prevent calls from proceeding with STUN/host candidates.

## What is NOT implemented

- **Application-level media E2EE**: WebRTC's DTLS-SRTP encrypts media in
  transit, but a malicious TURN server or compromised network intermediary
  could theoretically inspect relayed traffic. True end-to-end media
  encryption (e.g., WebRTC Insertable Streams / SFrame) is not implemented.
- **Call metadata persistence**: Active calls are stored in-memory on the
  server. Call history, duration, and participant records are not written to
  the database.
- **Rate limiting on signaling**: There is no per-user rate limit on call
  signaling events. A misbehaving client could flood the server with events.

## Diagnostics Privacy

The WebRTC diagnostics (`call-diagnostics.ts`) collect only technical metrics
(resolution, frame rate, packet loss, ICE candidate type, codec info). No
media content, user identifiers, or conversation data is included in the
diagnostic output. Stats are logged to the local console only.
