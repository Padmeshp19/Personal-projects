# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

This is a static Firebase-hosted web application with no build steps required.

**Local Development:**
- Serve files locally: `firebase serve` (requires Firebase CLI)
- Deploy to Firebase: `firebase deploy` (requires Firebase CLI)
- No linting, testing, or build tools configured

**Firebase Setup:**
1. Install Firebase CLI: `npm install -g firebase-tools`
2. Login: `firebase login`
3. Initialize project (if needed): `firebase init` (already configured)
4. Deploy: `firebase deploy`

## Code Architecture & Structure

**Core Technologies:**
- Firebase Authentication (email/password, Google)
- Firestore Database for file metadata and storage references
- Firebase Storage for actual file storage (via data URLs in Firestore)
- Vanilla HTML/CSS/JS (no frameworks)

**File Structure:**
- `index.html`: Login/signup page
- `home.html`: Main application interface after authentication
- `firebase.json`: Firebase hosting configuration
- `.firebaserc`: Firebase project alias configuration

**Key Features:**
1. **Authentication Flow**: 
   - `onAuthStateChanged` listeners redirect between index.html and home.html
   - Email/password signup/login with Firebase Auth
   - Google login with automatic display name fallback

2. **File Upload/Storage**:
   - Files converted to data URLs via FileReader and stored in Firestore
   - Metadata includes: userId, file (data URL), fileName, title, subject, timestamp
   - Upload triggers automatic refresh of file list

3. **File Display & Management**:
   - Grid layout showing user's files (admin sees all files)
   - Each file card shows: title, subject, download button
   - Hover effects: purple glow + reveal delete button (trash icon)
   - Delete functionality with confirmation prompt
   - Download via anchor tag with download attribute

4. **UI/UX Features**:
   - Custom cursor glow effect (follows mouse movement)
   - Responsive grid layout for file display
   - Dark theme with purple accents
   - Modal-free interactions (alerts for simplicity)

**Security Notes:**
- Firestore security rules NOT present in codebase (rely on client-side checks)
- Admin bypass: hardcoded email check (`padmeshp19@gmail.com`) for full access
- Files accessible via direct data URL links (no signed URLs)

**Common Tasks:**
- To modify authentication: edit auth functions in `<script>` tags
- To change file storage: modify upload() and loadNotes() functions
- To adjust UI: edit CSS variables and HTML structure
- To update Firebase config: modify firebaseConfig objects in both HTML files

**Important Files to Understand:**
1. `home.html`: Contains 90% of application logic (auth, upload, delete, display)
2. `index.html`: Simplified version focusing only on auth