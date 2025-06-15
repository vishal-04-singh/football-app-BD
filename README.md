# Football Tournament Management System - Backend API

A comprehensive backend API for managing football tournaments, teams, players, and matches. Built with Node.js, Express, and MongoDB.

## 🚀 Features

- **User Management**: Registration, authentication, and role-based access control
- **Team Management**: Create, update, and manage football teams
- **Player Management**: Add players to teams with position and jersey number tracking
- **Match Management**: Schedule matches, track scores, and record match events
- **Tournament Management**: Handle tournament data and statistics
- **Real-time Match Updates**: Live scoring and match statistics
- **Image Upload**: Support for base64 image uploads for team logos and player photos
- **Role-based Access**: Management, Captain, and Spectator roles with different permissions

## 🛠 Tech Stack

- **Backend**: Node.js, Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: bcryptjs
- **File Upload**: Multer with Cloudinary integration
- **Security**: Helmet, CORS, Express Rate Limit
- **Development**: Nodemon for hot reloading

## 📦 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/vishal-04-singh/football-app-BD.git
   cd football-app-BD
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   Create a `.env` file in the root directory:
   ```env
   MONGODB_URI=mongodb://localhost:27017/football-tournament
   JWT_SECRET=your-super-secret-jwt-key
   PORT=3000
   NODE_ENV=development
   ```

4. **Start the server**
   ```bash
   # Development mode
   npm run dev
   
   # Production mode
   npm start
   ```

## 🔧 Available Scripts

- `npm start` - Start the production server
- `npm run dev` - Start development server with hot reload
- `npm test` - Run API tests
- `npm run seed` - Seed database with initial data
- `npm run backup` - Backup database
- `npm run restore` - Restore database from backup

## 📊 Database Schema

### User Schema
- `name`: String (required)
- `email`: String (required, unique)
- `password`: String (required, hashed)
- `role`: Enum ['management', 'captain', 'spectator']
- `teamId`: Reference to Team (optional)

### Team Schema
- `name`: String (required)
- `logo`: String (base64 image)
- `captainId`: Reference to User
- `matchesPlayed`, `wins`, `draws`, `losses`: Numbers
- `goalsFor`, `goalsAgainst`, `points`: Numbers

### Player Schema
- `name`: String (required)
- `position`: String (required)
- `jerseyNumber`: Number (required, unique per team)
- `teamId`: Reference to Team
- `isSubstitute`: Boolean
- `photo`: String (base64 image)

### Match Schema
- `homeTeamId`, `awayTeamId`: References to Teams
- `date`, `time`, `venue`: Strings
- `status`: Enum ['upcoming', 'live', 'completed']
- `homeScore`, `awayScore`: Numbers
- `events`: Array of match events (goals, cards, substitutions)
- `minute`: Current match minute
- `possession`, `shots`, `corners`, `fouls`: Match statistics

## 🔐 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login
- `POST /api/auth/social` - Social media authentication
- `GET /api/auth/me` - Get current user info

### Teams
- `GET /api/teams` - Get all teams
- `POST /api/teams` - Create new team (Management only)
- `PUT /api/teams/:id` - Update team (Management only)
- `DELETE /api/teams/:id` - Delete team (Management only)
- `POST /api/teams/:teamId/assign-captain` - Assign captain to team
- `GET /api/teams/:teamId/players` - Get team players

### Players
- `GET /api/players` - Get all players
- `POST /api/players` - Add new player
- `PUT /api/players/:id` - Update player (Management only)
- `DELETE /api/players/:id` - Delete player (Management only)

### Matches
- `GET /api/matches` - Get all matches
- `POST /api/matches` - Schedule new match (Management only)
- `PUT /api/matches/:id` - Update match (Management only)
- `PUT /api/matches/:id/stats` - Update match statistics

### Tournament
- `GET /api/tournament` - Get tournament data with teams and matches

## 🎯 User Roles & Permissions

### Management
- Full access to all endpoints
- Can create, update, and delete teams
- Can manage players across all teams
- Can schedule and manage matches
- Can update match statistics and events

### Captain
- Can add players to their own team
- Can view all tournament data
- Cannot modify other teams or matches

### Spectator
- Read-only access to tournament data
- Can view teams, players, and matches
- Cannot modify any data

## 🏗 Project Structure

```
football-app-BD/
├── server.js              # Main server file
├── package.json           # Dependencies and scripts
├── .env                   # Environment variables
├── scripts/
│   ├── seed-data.js      # Database seeding
│   ├── backup-db.js      # Database backup
│   └── restore-db.js     # Database restore
└── test-api.js           # API testing
```

## 🚦 Getting Started

1. **Default Users**: The system creates default users on first run:
   - Manager: `manager@football.com` (password: `password`)
   - Captain: `captain@team1.com` (password: `password`)
   - Spectator: `fan@football.com` (password: `password`)

2. **Team Limits**: Maximum 8 teams per tournament

3. **Player Limits**: Maximum 11 players per team (7 main + 4 substitutes)

4. **Jersey Numbers**: Must be unique within each team (1-1000)

## 🔍 API Testing

Test the API using the provided test script:

```bash
npm test
```

Or use tools like Postman/Insomnia with the following base URL:
```
http://localhost:3000/api
```

## 📝 Example API Requests

### Register a New User
```bash
curl -X POST http://localhost:3000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "role": "captain"
  }'
```

### Create a New Team
```bash
curl -X POST http://localhost:3000/api/teams \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -d '{
    "name": "Barcelona FC",
    "logo": "data:image/png;base64,..."
  }'
```

## 🔒 Security Features

- JWT-based authentication
- Password hashing with bcrypt
- CORS enabled for cross-origin requests
- Rate limiting to prevent abuse
- Input validation and sanitization
- Role-based access control

## 🐛 Error Handling

The API includes comprehensive error handling:
- Validation errors with detailed messages
- Authentication and authorization errors
- Database constraint errors
- Proper HTTP status codes
- Development vs production error responses

## 🚀 Deployment

The application is ready for deployment to platforms like:
- Heroku
- Railway
- Render
- DigitalOcean App Platform

Make sure to set the environment variables in your deployment platform.

## 📄 License

This project is licensed under the MIT License.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📞 Support

For support and questions, please open an issue in the repository or contact the development team.

---

**Built with ❤️ for football enthusiasts**