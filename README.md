 # Hashnode Clone – MERN Developer Blogging Platform

Every file is already in the right folder. You do NOT need to copy-paste anything.

 ## Folder map (what each file is for)

```
hashnode-clone/
├── server/                      <- BACKEND (Node + Express + MongoDB)
│   ├── .env.example             -> copy to ".env" and edit
│   ├── package.json             -> dependencies + npm scripts
│   ├── server.js                -> starts the server, connects MongoDB
│   ├── seed.js                  -> optional demo data (users + posts)
│   ├── models/User.js           -> user schema (bio, following)
│   ├── models/Post.js           -> post schema (tags, likes, comments, draft/publish)
│   ├── middleware/auth.js       -> JWT protect middleware
│   └── routes/
│       ├── auth.js              -> register / login / me
│       ├── posts.js             -> feed, search, tags, CRUD, like, comments
│       └── users.js             -> profile, follow, top authors
└── client/                      <- FRONTEND (React + Vite)
    ├── .env.example             -> copy to ".env"
    ├── index.html, vite.config.js, package.json
    └── src/
        ├── main.jsx             -> app entry (Router + Auth provider)
        ├── App.jsx              -> all page routes + protected routes
        ├── api.js               -> Axios instance + JWT header
        ├── utils.js             -> read time, date format helpers
        ├── index.css            -> the whole Hashnode-style design
        ├── context/AuthContext.jsx   -> login state
        ├── components/
        │   ├── Layout.jsx       -> sidebar + topbar + page + right column
        │   ├── Sidebar.jsx      -> Home / Explore / My Blogs / Drafts / Profile / Settings
        │   ├── Topbar.jsx       -> search bar, login / avatar
        │   ├── RightRail.jsx    -> Trending Topics, Top Authors, Start your journey
        │   ├── PostCard.jsx     -> blog card (thumbnail, tags, like, comments)
        │   ├── Thumb.jsx        -> React / Node / MongoDB thumbnails
        │   └── Markdown.jsx     -> Markdown + syntax-highlighted code
        └── pages/
            ├── Home.jsx         -> hero, filter chips, sort, feed (also used for Explore)
            ├── Login.jsx, Register.jsx
            ├── Editor.jsx       -> write/edit with live preview, draft or publish
            ├── PostView.jsx     -> full post, like, comments, edit/delete
            ├── MyBlogs.jsx      -> published posts, and Drafts (same file)
            ├── Profile.jsx      -> author page + follow
            └── Settings.jsx     -> edit name/bio, light/dark theme
```

## Step-by-step

### Step 1 – Install the tools (one time)
1. Node.js 18 or newer: https://nodejs.org
2. MongoDB Community Server (local) OR a free MongoDB Atlas cluster.
3. VS Code.

### Step 2 – Open the project
Unzip, then in VS Code: File > Open Folder > `hashnode-clone`.
Open the terminal with Ctrl + ` (backtick). You will use TWO terminals.

### Step 3 – Backend (Terminal 1)
```
cd server
npm install
```
Create the env file:
- Windows: `copy .env.example .env`
- Mac/Linux: `cp .env.example .env`

Open `server/.env`. If you use Atlas, replace MONGO_URI with your Atlas string.
Change JWT_SECRET to any long random text.

Optional demo data (4 authors + 6 posts, login `ovinea@demo.com` / `password123`):
```
npm run seed
```
Start the server:
```
npm run dev
```
You should see: `MongoDB connected` and `Server on port 5000`.

### Step 4 – Frontend (Terminal 2)
```
cd client
npm install
```
Create the env file (same copy command as above): `.env.example` -> `.env`.
```
npm run dev
```
Open http://localhost:5173

### Step 5 – Test the full flow
1. Sign up (or log in with the demo user).
2. Click "Write a Blog", write Markdown with a ```js code block, press "Save draft".
3. Go to Drafts, Publish it. It appears on Home.
4. Like it, comment, search in the top bar, click tag chips, switch Latest/Popular.
5. Open an author's profile and press Follow.

### Step 6 – Deploy (optional)
- Database: MongoDB Atlas.
- Backend: Render. Root dir `server`, build `npm install`, start `npm start`. Add the 4 env variables. Set CLIENT_URL to your frontend URL.
- Frontend: Vercel or Netlify. Root dir `client`, build `npm run build`, output `dist`. Set `VITE_API_URL=https://YOUR-BACKEND.onrender.com/api`.
- For Vercel/Netlify add a rewrite of all paths to `/index.html` so page refresh works.

### Step 7 – Submit
Push to GitHub (do NOT upload `.env` or `node_modules`), add screenshots to this README.

## Common errors
- CORS error: CLIENT_URL in server/.env must be exactly http://localhost:5173
- MongoDB connection failed: start the MongoDB service, or check your Atlas string / IP allow-list.
- 401 errors: log out and log in again.
- `npm run dev` not found: you are in the wrong folder (use server or client).
