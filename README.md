# Listify Backend 🎧

Listify is a powerful, scalable backend API designed for the next generation of social music applications. Built with **Ruby on Rails 8**, it provides a rich suite of features for music discovery, social interaction, and content management.

This backend is specifically optimized for **mobile integration**, with a focus on **React Native** compatibility.

---

## 🚀 Features

### 🔐 Authentication & Security
- **JWT-based Auth**: Stateless authentication using `devise-jwt`.
- **Token Revocation**: Denylist strategy for secure logout.
- **Protected Routes**: Granular authorization for user-specific data.

### 👥 Social Graph
- **Follow System**: Follow/Unfollow users to build a personal network.
- **Discovery**: List followers and following counts with ease.

### 🎵 Music Database
- **Albums & Songs**: Comprehensive metadata for tracks and albums.
- **Search & Filter**: Optimized queries for music discovery.

### 💬 Engagement & Interactions
- **Reviews**: Rate and review songs (1-5 stars).
- **Social Loop**: Like and comment on reviews to drive engagement.
- **Activities**: Automated logging of user actions for discovery feeds.

### 📢 Real-Time Engine
- **Notifications**: Instant alerts for follows, likes, and comments.
- **Feeds**: Personal "Following" feed and global "Explore" feed with **cursor-based pagination**.

### 📦 Media Support
- **ActiveStorage**: Integrated support for profile pictures and album cover art.
- **Cloud Ready**: Standardized attachments ready for S3/Cloud Storage.

---

## 🛠 Tech Stack

- **Framework**: Ruby on Rails 8.0
- **Database**: PostgreSQL (Production-ready)
- **Auth**: Devise + JWT
- **Storage**: ActiveStorage
- **Image Processing**: ImageProcessing (libvips/ImageMagick)

---

## 📡 API Reference

| Endpoint | Method | Description |
| :--- | :--- | :--- |
| `/api/v1/auth/login` | POST | Authenticate and receive JWT |
| `/api/v1/feed/following` | GET | Your personal discovery feed |
| `/api/v1/notifications` | GET | Activity alerts |
| `/api/v1/songs` | GET | List available tracks |
| `/api/v1/users/:id/follow`| POST | Follow a user |


---

## 📱 Mobile Integration (React Native)

This backend is prepared for seamless integration with React Native. Key tips:

### 1. Handling Authentication
Tokens are returned in the `Authorization` header during login.
```javascript
// Example: Storing token in React Native
const token = response.headers.get('Authorization');
await AsyncStorage.setItem('userToken', token);
```

### 2. Request Headers
Include the JWT in every protected request:
```javascript
const response = await fetch('YOUR_API_URL/api/v1/users/me', {
  headers: {
    'Authorization': await AsyncStorage.getItem('userToken'),
    'Content-Type': 'application/json'
  }
});
```

### 3. Image Loading
ActiveStorage URLs are provided in the responses. Use them directly in `<Image />` tags. For variants (thumbnails), you can request specific sizes via the backend API.

---

## 🏁 Getting Started

1. **Install Dependencies**:
   ```bash
   bundle install
   ```
2. **Setup Database**:
   ```bash
   rails db:create db:migrate db:seed
   ```
3. **Run Server**:
   ```bash
   rails s
   ```

---

## 🏆 Development & Quality
The codebase is fully verified with automated integration scripts ensuring that all social, music, and notification flows are bug-free.
