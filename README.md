# AISStream (aisstream)

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
