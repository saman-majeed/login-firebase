# Real-time Chat Application with Firebase

This is a complete real-time chat application built with Firebase Authentication and Firestore. Users can log in, see other active users, and chat with them in real-time.

## Features

✅ **Authentication**
- Email/password registration and login
- Email verification required
- Google Sign-in support
- Session management

✅ **Real-time Chat**
- Live user list with online status
- Real-time messaging between users
- Message timestamps
- Auto-scroll to new messages
- Responsive design for mobile devices

✅ **User Experience**
- Modern UI with clean design
- User avatars with initials
- Online/offline status indicators
- Message input with auto-resize
- Send messages with Enter key or button click

## Setup Instructions

### 1. Firebase Configuration

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project or use existing one
3. Enable the following services:
   - **Authentication** (Email/Password and Google providers)
   - **Firestore Database**

### 2. Firestore Security Rules

Set up the following security rules in Firestore:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users can read/write their own user document
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
      allow read: if request.auth != null; // Allow reading other users for chat list
    }
    
    // Chat messages - users can only access chats they're part of
    match /chats/{chatId} {
      allow read, write: if request.auth != null && 
        (request.auth.uid in resource.data.participants || 
         request.auth.uid in request.resource.data.participants);
      
      match /messages/{messageId} {
        allow read, write: if request.auth != null && 
          (request.auth.uid == resource.data.senderId || 
           request.auth.uid == resource.data.recipientId);
      }
    }
  }
}
```

### 3. Required Firebase Services

Make sure these services are enabled in your Firebase project:

- **Authentication**: Email/Password provider
- **Firestore Database**: In production mode
- **Hosting** (optional): For deployment

### 4. File Structure

```
login-firebase/
├── index.html          # Login/Registration page
├── home.html           # Chat application
├── styles.css          # Styles for login page
├── verify.html         # Email verification page
├── firebase-setup.md   # Firebase setup guide
└── README.md          # This file
```

### 5. Usage

1. **Registration**: Create a new account with email and password
2. **Email Verification**: Check your email and verify your account
3. **Login**: Sign in with your verified credentials
4. **Chat**: 
   - View list of registered users on the left sidebar
   - Click on any user to start chatting
   - Send messages in real-time
   - See online/offline status of other users

## Technical Implementation

### Database Structure

**Users Collection** (`/users/{userId}`)
```javascript
{
  uid: "user-id",
  displayName: "User Name",
  email: "user@example.com",
  online: true,
  lastActive: timestamp,
  createdAt: timestamp,
  emailVerified: true
}
```

**Chats Collection** (`/chats/{chatId}`)
```javascript
{
  participants: ["userId1", "userId2"],
  lastMessage: "Last message text",
  lastMessageTime: timestamp
}
```

**Messages Subcollection** (`/chats/{chatId}/messages/{messageId}`)
```javascript
{
  text: "Message content",
  senderId: "sender-user-id",
  recipientId: "recipient-user-id",
  timestamp: timestamp
}
```

### Key Features Implementation

1. **Real-time Updates**: Using Firestore's `onSnapshot()` listeners
2. **Chat ID Generation**: Consistent chat IDs using sorted user IDs
3. **Online Status**: Updated on login/logout and page unload
4. **Message Ordering**: Messages sorted by timestamp
5. **Responsive Design**: Mobile-friendly layout with CSS Grid/Flexbox

### Security Features

- Email verification required before chat access
- Firestore security rules prevent unauthorized data access
- User session management with Firebase Auth
- Real-time listeners automatically clean up on logout

## Browser Compatibility

- Chrome 60+
- Firefox 55+
- Safari 11+
- Edge 79+

## Deployment

For production deployment:

1. Use Firebase Hosting for optimal performance
2. Configure custom domain if needed
3. Set up proper Firebase security rules
4. Enable Firebase Analytics (optional)

## Troubleshooting

### Common Issues

1. **"No users found"**: Make sure other users have registered and verified their emails
2. **Messages not sending**: Check Firestore security rules and network connection
3. **Users not showing as online**: Verify the `updateUserOnlineStatus` function is working
4. **Real-time updates not working**: Ensure Firestore listeners are properly set up

### Development Tips

- Use browser dev tools to monitor Firestore operations
- Check console for any JavaScript errors
- Verify Firebase configuration is correct
- Test with multiple browser windows/tabs for real-time functionality

## Next Steps

Possible enhancements:
- Message read receipts
- Group chat functionality
- File/image sharing
- Push notifications
- Message search
- Dark mode theme
- Emoji support
- Message encryption
