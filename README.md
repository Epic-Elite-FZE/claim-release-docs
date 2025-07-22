# Claim Release API Endpoints

This document describes the usage of the `/claim-release` and `/claim-release/list` endpoints for integrating with our claim release service.

---

## 1. `POST /claim-release`

**Purpose:**  
Register or update a video URL and associate it with claims in the system.

**Query Parameters:**

- `token` (string, required): Authorization token.
- `url` (string, required): The full YouTube video URL (must contain a `v` parameter for the video ID).

**Request Example:**

```
POST /claim-release?token=YOUR_TOKEN&url=https://www.youtube.com/watch?v=VIDEO_ID
```

**Response Example:**

```json
{
  "videoId": "VIDEO_ID",
  "videoUrl": "https://www.youtube.com/watch?v=VIDEO_ID",
  "createdAt": "2024-06-10T12:34:56.789Z",
  "claims": [
    {
      "status": "Active",
      "claimId": "12345",
      "claimCreatedAt": "2024-06-01T10:00:00.000Z",
      "claimReleasedAt": null,
      "isReleased": false,
      "videoId": "VIDEO_ID",
      "url": "https://www.youtube.com/watch?v=VIDEO_ID"
    }
    // ... more claims if present
  ]
}
```

**Error Responses:**

- `403 Forbidden`: If the token is missing or invalid.
- `400 Bad Request`: If the video ID cannot be extracted from the URL.

---

## 2. `GET /claim-release/list`

**Purpose:**  
Retrieve claims associated with a video by `videoId` or `url`.

**Query Parameters:**

- `token` (string, required): Authorization token.
- `videoId` (string, optional): The YouTube video ID.
- `url` (string, optional): The full YouTube video URL.

> **Note:** Either `videoId` or `url` must be provided.

**Request Example:**

```
GET /claim-release/list?token=YOUR_TOKEN&videoId=VIDEO_ID
```

or

```
GET /claim-release/list?token=YOUR_TOKEN&url=https://www.youtube.com/watch?v=VIDEO_ID
```

**Response Example:**

```json
{
  "videoId": "VIDEO_ID",
  "videoUrl": "https://www.youtube.com/watch?v=VIDEO_ID",
  "createdAt": "2024-06-10T12:34:56.789Z",
  "claims": [
    {
      "status": "Active",
      "claimId": "12345",
      "claimCreatedAt": "2024-06-01T10:00:00.000Z",
      "claimReleasedAt": null,
      "isReleased": false,
      "videoId": "VIDEO_ID",
      "url": "https://www.youtube.com/watch?v=VIDEO_ID"
    }
    // ... more claims if present
  ]
}
```

**Error Responses:**

- `403 Forbidden`: If the token is missing or invalid.
- `404 Not Found`: If neither `videoId` nor `url` is provided.

---

## Sequence Diagram

Below is a visual overview of the flow for both endpoints:

---

## Permissions

Tokens must be obtained from your system administrator or integration contact.

---

## Contact

For further questions or to request access, please contact your integration manager or the API support team.
