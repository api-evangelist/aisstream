# AISStream (aisstream)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AISStream.io is a **free** service that streams global **real-time AIS**
(Automatic Identification System) vessel-tracking data over a **WebSocket**.

**Access model, up front:**

- **WebSocket-only.** There is **no REST API**. The single product surface is a
  secure WebSocket at `wss://stream.aisstream.io/v0/stream`.
- **Free.** The stream is provided at no cost. You obtain a free **API key** by
  registering at [aisstream.io](https://aisstream.io/).
- **How it works.** Connect, then send one JSON **subscription message** within
  3 seconds. It carries your `APIKey`, one or more geographic `BoundingBoxes`,
  and optional `FiltersShipMMSI` and `FilterMessageTypes`. The server then
  pushes a continuous stream of AIS messages until you close the socket.
- **API key placement.** The key goes in the `APIKey` field of the subscription
  **message body** - not in an HTTP header.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/aisstream/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/aisstream/refs/heads/main/apis.yml)

## Tags

- Vessel Tracking
- AIS
- Maritime
- Ship Tracking
- Real-Time Data
- WebSocket
- Streaming
- Ships
- Maritime Data
- Location

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### AISStream AIS Stream API

Real-time global AIS vessel-tracking stream delivered over a single WebSocket at
`wss://stream.aisstream.io/v0/stream`. The client connects, sends a JSON
subscription message (`APIKey` plus `BoundingBoxes` and optional
`FiltersShipMMSI` and `FilterMessageTypes`), and receives a continuous feed of
AIS messages - each an envelope with `MessageType`, a free-form `MetaData`
object, and the decoded `Message` keyed by its type (`PositionReport`,
`ShipStaticData`, and the rest of the ITU-R M.1371 message set).

- **Human URL:** [https://aisstream.io/documentation](https://aisstream.io/documentation)
- **Base URL (WebSocket):** `wss://stream.aisstream.io/v0/stream`

#### Tags

- AIS
- Vessel Tracking
- WebSocket
- Streaming
- Real-Time Data

#### Properties

- [Documentation](https://aisstream.io/documentation)
- [API Reference](https://aisstream.io/documentation)
- [AsyncAPI](asyncapi/aisstream-asyncapi.yml) — [AsyncAPI Specification](https://www.asyncapi.com/docs/reference/specification/latest)
- [Postman Collection](collections/aisstream.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/aisstream.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Source Code](https://github.com/aisstream/ais-message-models) — official AIS message models
- [SDK / Examples](https://github.com/aisstream/example) — example clients in many languages

## Subscription message

```json
{
  "APIKey": "<YOUR API KEY>",
  "BoundingBoxes": [[[-90.0, -180.0], [90.0, 180.0]]],
  "FiltersShipMMSI": ["368207620", "367719770"],
  "FilterMessageTypes": ["PositionReport", "ShipStaticData"]
}
```

Each bounding box is two `[latitude, longitude]` corner pairs. `APIKey` and
`BoundingBoxes` are required; `FiltersShipMMSI` and `FilterMessageTypes` are
optional.

## Received message envelope

```json
{
  "MessageType": "PositionReport",
  "MetaData": { "MMSI": 368207620, "ShipName": "EXAMPLE VESSEL", "latitude": 25.702, "longitude": -80.101, "time_utc": "..." },
  "Message": { "PositionReport": { "UserID": 368207620, "Latitude": 25.702, "Longitude": -80.101, "Sog": 12.3, "Cog": 180.5 } }
}
```

Check `MessageType` to know which decoded payload is present under `Message`.

## AIS message types

`PositionReport`, `UnknownMessage`, `AddressedSafetyMessage`,
`AddressedBinaryMessage`, `AidsToNavigationReport`, `AssignedModeCommand`,
`BaseStationReport`, `BinaryAcknowledge`, `BinaryBroadcastMessage`,
`ChannelManagement`, `CoordinatedUTCInquiry`, `DataLinkManagementMessage`,
`DataLinkManagementMessageData`, `ExtendedClassBPositionReport`,
`GroupAssignmentCommand`, `GnssBroadcastBinaryMessage`, `Interrogation`,
`LongRangeAisBroadcastMessage`, `MultiSlotBinaryMessage`,
`SafetyBroadcastMessage`, `ShipStaticData`, `SingleSlotBinaryMessage`,
`StandardClassBPositionReport`, `StandardSearchAndRescueAircraftReport`,
`StaticDataReport`.

## Common Properties

- [GitHub Organization](https://github.com/aisstream)
- [Website](https://aisstream.io)
- [Documentation](https://aisstream.io/documentation)
- [Plans](plans/aisstream-plans-pricing.yml)
- [Rate Limits](rate-limits/aisstream-rate-limits.yml)
- [Fin Ops](finops/aisstream-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
