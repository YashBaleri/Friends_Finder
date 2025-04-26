# Friends Connect

New to a gym and looking for workout buddies? Or always wanted to hike Mount Rainier but don’t have anyone to go with? Friends Connect helps you meet like-minded people from your gym, university, or workplace so you can plan activities together.

A web application designed to help you discover and connect with people who share your favorite venues—whether gyms, universities, or other spots you frequent. By combining content-based interest matching (e.g., shared interests like university or workplace) with geospatial proximity, Friends Connect makes it effortless to find new friends or plan group meetups. Plus, a fast chat feature lets you coordinate in real time.

---

## Technologies

- **Backend**: Node.js, Express.js, REST  
- **Database**: MongoDB  
- **Frontend**: HTML, CSS  
- **Realtime**: WebSocket  
- **Mapping**: Google Maps API (deprecated)  

---

## Prerequisites

- [Node.js](https://nodejs.org/) (v14+)
- [MongoDB](https://www.mongodb.com/) (local or Atlas)

---

## Database Indexes

To ensure fast and accurate location-based matching, create a geospatial index on your users collection:

```js
// In the Mongo shell or a migration script:
db.users.createIndex({ location: "2dsphere" });
```

This index enables efficient 2dsphere queries for finding nearby users.

---

## Installation & Setup

1. **Clone the repository**
   ```bash
   git clone <repo-url>
   cd friends-connect
   ```

2. **Configure environment variables**  
   Create a `.env` file in the project root with the following keys:
   ```dotenv
   PORT=3000
   MONGODB_URI=<your-mongodb-connection-string>
   JWT_SECRET=<your-jwt-secret>
   ```
   Ensure you never commit `.env` to version control.

3. **Install dependencies**
   ```bash
   npm install
   ```

4. **Seed the database**  
   Populates `users` collection with sample accounts:
   ```bash
   npm run seed
   ```
   > **Test credentials**  
   > Email: `alicesmith@example.com`  
   > Password: `Password1234$`

5. **Start the server**  
   ```bash
   npm start
   ```

The app will be live at:  `http://localhost:3000`

---

## Deprecated Features

- **Google Maps API integration** and **online chat server** were deprecated in **v2.3 (April 2024)**.  
- **Alternative mapping**: continue using MongoDB’s built-in geospatial queries (local or Atlas); consider community-driven map libraries like **Mapbox GL JS** for rich client-side maps.  
- **Local chat** remains fully supported; migrate away from the legacy online chat server by relying on the existing WebSocket layer.

---

## Usage

### Landing & Auth

- **Homepage** provides an overview of features and purpose, plus links to **Login** and **Register**.  
- **Login** using seeded credentials or your own account.  
- **Register** via `/register` or the on-page button.  
  - Matches only appear if other users share at least one common criterion (university, workplace, gym/class).  
  - After registering, you’ll be redirected to **Login**.

### Dashboard

After logging in, you’ll see four main cards (and nav links):  
> **Find Matches | Your Matches | Your Profile | Messages**  
> plus **Logout** and **Delete Account** in the navbar.

#### 1. Find Matches  
- Browse one user at a time; you must **Like** or **Dislike** to view the next profile.  
- Toggle to limit results to users within **5 km** of your location.  
- View any user’s full profile before making a decision.

#### 2. Your Matches  
- Lists all users you’ve mutually liked.  
- Search matches and **Unmatch** if desired.  
- From here, you can also **Message** any match (local chat only).

#### 3. Messages  
- Real-time local chat with any active match.  
- Once unmatched by either party, messaging is disabled.

#### 4. Your Profile  
- Displays your signup information.  
- **Edit Profile**: update fields as needed; unchanged fields remain the same.  
- **Pause/Unpause**: when paused, you won’t appear in **Find Matches**.

---

## Notes

- **Match criteria**: shared university, workplace, desired visit location, or gym/class.  
- If no one shares your criteria, **Find Matches** will temporarily show no results.  
- Deleting your account removes all your data permanently.

---

## License

MIT License – see [LICENSE](./LICENSE) for details.
