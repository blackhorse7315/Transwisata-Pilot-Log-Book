TRANSWISATA PILOT LOGBOOK — FIREBASE SPARK USERNAME/PASSWORD

1. Enable Firebase Authentication > Email/Password.
2. Firestore > Rules: publish firestore.rules. Existing admin must already have userAccess/{ADMIN_UID} role=admin (create manually in Firebase Console).
3. Upload index.html, icons, manifest.webmanifest and sw.js to GitHub Pages.
4. Log in as Admin using Firebase email and password. Go to Pilot Directory > Set Pilot Login. Enter unique username and password (>=8 chars). App creates a secondary Firebase Auth user and writes userAccess/{UID} with role=pilot and pilotId.
5. Copy Login Link and share privately. Pilot logs in with assigned username/password. Login session persists in browser; later visits can enter automatically while signed in.
6. To disable pilot: delete userAccess/{UID} in Firestore (immediately blocks Firestore), and disable/delete user in Firebase Authentication. To reset pilot password use Firebase Authentication Console reset flow; this frontend cannot securely change another user's password.

IMPORTANT: Firebase Email/Password sign-up endpoint is publicly callable when enabled; an attacker can create unprivileged orphan Authentication accounts, but cannot create authorized userAccess documents under these rules. Use Firebase App Check and account-creation abuse monitoring where available. This is not a substitute for server-side account provisioning at scale.

IMPORTANT: No Blaze plan or Cloud Functions required. No plaintext passwords are stored in Firestore. Personal URL identifies intended pilot, NOT an authentication token. Users must authenticate at least once on each device/browser. For continued auto-login Firebase persists their session.

IMPORTANT: Flight records currently stored as arrays per pilot; concurrent edits can overwrite each other. Test and harden before operational use. PDF validation is not an electronic signature system.
