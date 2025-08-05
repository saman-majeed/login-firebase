# Firebase Setup Instructions

## 1. Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" or "Add project"
3. Enter your project name (e.g., "login-firebase")
4. Follow the setup wizard

## 2. Enable Authentication

1. In your Firebase project console, go to "Authentication"
2. Click "Get started"
3. Go to the "Sign-in method" tab
4. Enable "Email/Password" authentication
5. Save the changes

## 3. Get Your Firebase Configuration

1. In the Firebase console, click the gear icon (Settings)
2. Go to "Project settings"
3. Scroll down to "Your apps" section
4. Click the web icon (`</>`) to add a web app
5. Register your app with a nickname (e.g., "Login App")
6. Copy the Firebase configuration object

## 4. Update Your Configuration

Replace the placeholder values in both `index.html` and `home.html`:

```javascript
const firebaseConfig = {
  apiKey: "your-actual-api-key",
  authDomain: "your-project-id.firebaseapp.com",
  projectId: "your-actual-project-id",
  storageBucket: "your-project-id.appspot.com",
  messagingSenderId: "your-actual-sender-id",
  appId: "your-actual-app-id"
};
```

## 5. Configure Email Verification (Optional)

1. In Firebase Console, go to Authentication > Templates
2. Customize the email verification template if needed
3. Set your authorized domains in Authentication > Settings

## 6. Test Your Application

1. Open `index.html` in a web browser
2. Try creating a new account
3. Check your email for the verification link
4. After verification, try logging in

## Security Notes

- Never commit your Firebase configuration to a public repository if it contains sensitive data
- Consider using Firebase Security Rules for additional protection
- For production, set up proper domain restrictions in Firebase Console

## Features Included

✅ User registration with email/password  
✅ Email verification required before login  
✅ Secure login with Firebase Authentication  
✅ Session management  
✅ Logout functionality  
✅ Error handling with user-friendly messages  
✅ Real-time form validation  
✅ Password strength indicator  
✅ Responsive design  

## Troubleshooting

- **"Firebase: Error (auth/operation-not-allowed)"**: Make sure Email/Password authentication is enabled in Firebase Console
- **"Firebase: Error (auth/invalid-api-key)"**: Check that your API key is correct
- **Email verification not working**: Check your spam folder and ensure your domain is authorized in Firebase
