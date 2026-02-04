# Listify API Documentation

Welcome to the **Listify Backend** API documentation. This document provides a comprehensive guide for frontend developers to integrate with the Listify music platform.

## 🚀 Overview

Listify is a social music platform where users can:
- Discover songs and albums.
- Write reviews and rate music.
- Follow friends and see their music activity.
- Create and manage music collections (playlists).
- Receive notifications for social interactions.

---

## 🔐 Authentication

Listify uses **Devise** with **JWT (JSON Web Tokens)** for secure authentication. 

- **Auth Strategy**: Bearer Token
- **Header**: `Authorization: Bearer <TOKEN>`
- **Revocation**: Tokens are automatically revoked upon logout via a denylist.

### Auth Endpoints

| Endpoint | Method | Description | Body Parameters |
| :--- | :--- | :--- | :--- |
| `/api/v1/auth/registrations` | `POST` | User Sign Up | `user[email]`, `user[password]`, `user[username]`, `user[bio]` (opt), `user[profile_picture_url]` (opt) |
| `/api/v1/auth/login` | `POST` | User Login | `user[email]`, `user[password]` |
| `/api/v1/auth/logout` | `DELETE` | User Logout | (Requires Auth Header) |

---

## 👤 User Profiles

Manage user identity and social connections.

| Endpoint | Method | Auth | Description | Body / Path Params |
| :--- | :--- | :--- | :--- | :--- |
| `/api/v1/users/me` | `GET` | Yes | Get current user profile | - |
| `/api/v1/users/:id/follow` | `POST` | Yes | Follow a user | `:id` (User ID to follow) |
| `/api/v1/users/:id/unfollow` | `DELETE` | Yes | Unfollow a user | `:id` (User ID to unfollow) |
| `/api/v1/users/:id/followers` | `GET` | Yes | List followers | `:id` (User ID) |
| `/api/v1/users/:id/following` | `GET` | Yes | List following | `:id` (User ID) |

---

## 🎵 Music Library

Endpoints to browse through the music catalog.

| Endpoint | Method | Auth | Description |
| :--- | :--- | :--- | :--- |
| `/api/v1/songs` | `GET` | Yes | List all songs (includes album data) |
| `/api/v1/songs/:id` | `GET` | Yes | Get song details |
| `/api/v1/songs/:song_id/reviews` | `GET` | Yes | Get all reviews for a specific song |

---

## 📝 Reviews & Social Interaction

Users can share opinions and interact with others' content.

| Endpoint | Method | Auth | Description | Body Parameters |
| :--- | :--- | :--- | :--- | :--- |
| `/api/v1/reviews` | `POST` | Yes | Create a song review | `review[song_id]`, `review[rating]` (1-5), `review[review_text]` |
| `/api/v1/reviews/:id` | `PATCH/PUT` | Yes | Update own review | `review[rating]`, `review[review_text]` |
| `/api/v1/reviews/:id` | `DELETE` | Yes | Delete own review | `:id` (Review ID) |
| `/api/v1/reviews/:review_id/comments` | `GET` | Yes | Get comments for a review | `:review_id` |
| `/api/v1/comments` | `POST` | Yes | Post a comment | `commentable_id`, `commentable_type` (e.g., "Review"), `text` |
| `/api/v1/likes` | `POST` | Yes | Like a review | `likeable_id`, `likeable_type` (e.g., "Review") |
| `/api/v1/likes/:id` | `DELETE` | Yes | Remove a like | `:id` (Like record ID) |

---

## 🏠 Feeds

Feeds show activity from people the user follows or global highlights.

| Endpoint | Method | Auth | Description | Query Params |
| :--- | :--- | :--- | :--- | :--- |
| `/api/v1/feed/following` | `GET` | Yes | Activity feed from followed users | `before_id` (opt, for pagination) |
| `/api/v1/feed/explore` | `GET` | Yes | Global discovery feed | `before_id` (opt, for pagination) |

---

## 📂 Collections

Manage personalized music collections.

| Endpoint | Method | Auth | Description | Body Parameters |
| :--- | :--- | :--- | :--- | :--- |
| `/api/v1/collections` | `POST` | Yes | Create a new collection | `collection[title]`, `collection[description]`, `collection[public]` (bool) |
| `/api/v1/collections/:id/items` | `POST` | Yes | Add a song to a collection | `song_id` |
| `/api/v1/collections/:id/items/:song_id` | `DELETE` | Yes | Remove song from collection | `:id`, `:song_id` |

---

## 🔔 Notifications

Track interactions from other users.

| Endpoint | Method | Auth | Description |
| :--- | :--- | :--- | :--- |
| `/api/v1/notifications` | `GET` | Yes | Get recent notifications |
| `/api/v1/notifications/:id/read` | `PATCH` | Yes | Mark a notification as read |

---

## 🛠 Developer Notes

### 📊 Common Response Schema
Most resources return JSON objects wrapped in a key reflecting the model (e.g., `{ "user": { ... } }`). Error responses follow this structure:
```json
{
  "error": "Error message description"
}
```

### 🖼 Images
Listify uses **ActiveStorage** for image management. If a `profile_picture_url` or `cover_url` is provided, it will point to an public URL or a Rails service URL.

### 🧪 API Base URL (Local Development)
`http://localhost:3000` (or the IP address of your workstation if testing on mobile devices).

---

Happy Coding! 🎧
