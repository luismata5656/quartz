A firebase project can have more than one app, such as a web app, IOS app, and Android app
The initial Dev process happens solely in the Develop section on the side of firebase

When creating an app you need to initialize the firebase sdk, here is an example:
```tsx
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";

// Your web app's Firebase configuration
const firebaseConfig = {
	apiKey: "xxx",
	authDomain: "xxx",
	projectId: "xxx",
	storageBucket: "xxx",
	messagingSenderId: "xxx",
	appId: "xxx"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
```

## Firebase CLI
The firebase cli is used for managing firebase projects, it is used for deploying, testing and other functions
## User Authentication
firebase auth is essentially a Read Only DB for users, the only way to register is through the SDK
There are several ways to authenticate, including Google, Github, or just straight Email / Pwd
firebase Authenticates using JWTs

signing in is a one off action, only called when the user logs in, but the state may change over time, so you can use `auth.onAuthStateChanged()` in order to get when the user changes states
### User States
##### An Auth listener gets notified in the following situations:
- The Auth object finishes initializing and a user was already signed in from a previous session, or has been redirected from an identity provider's sign-in flow
- A user signs in (the current user is set)
- A user signs out (the current user becomes null)
- The current user's access token is refreshed. This case can happen in the following conditions:
    - The access token expires: this is a common situation. The refresh token is used to get a new valid set of tokens.
    - The user changes their password: Firebase issues new access and refresh tokens and renders the old tokens expired. This automatically expires the user's token and/or signs out the user on every device, for security reasons.
    - The user re-authenticates: some actions require that the user's credentials are recently issued; such actions include deleting an account, setting a primary email address, and changing a password. Instead of signing out the user and then signing in the user again, get new credentials from the user, and pass the new credentials to the reauthenticate method of the user object.

so `auth.onAuthStateChanged()` is called whenever:
- user signs in / out
- user comes back to session after closing the tab
- user's session expires
- user changes their password
- user re-authenticates, like Github Sudo Mode
## Data Storage
Firebase has two data storage solutions: Realtime Database, and Cloud Firestore
### Realtime Database
 Here is some info from the docs:
*The Firebase Realtime Database is a cloud-hosted database. Data is stored as JSON and synchronized in realtime to every connected client. When you build cross-platform apps with our Apple platforms, Android, and JavaScript SDKs, all of your clients share one Realtime Database instance and automatically receive updates with the newest data.*
### Cloud Firestore
This is the most common solution, it is no-sql, so there is no schema to model the data

Firestore is Document Oriented so it has a structure like this:
- Collection
	- document 1
		- field1:"xxx"
		- field2:"xxx"
	- document 2
		- field1:"xxx"
		- field3:"xxx"

And so on, notice that the documents can have different fields but still live in the same collection, this is both good and bad because you won't error out when storing the data, but the data returned can be unpredictable if not handled correctly
#### Security Rules
firestore allows anyone to query data, but using their security rules, the request can be blocked on the backend side rather than frontend.
### Cloud Storage
Cloud Storage is a completely different service which makes uploading files much easier.

# References
<iframe title="Firebase - Back to the Basics" src="https://www.youtube.com/embed/q5J5ho7YUhA?feature=oembed" height="113" width="200" allowfullscreen="" allow="fullscreen" style="aspect-ratio: 1.76991 / 1; width: 100%; height: 100%;"></iframe>