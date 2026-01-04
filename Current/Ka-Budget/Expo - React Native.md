File Structure
-  app
	- app's navigation, file-based
	- layout.tsx sets up the tab navigator
- assets
	- adaptive-icon.png for Android
	- splash.png for app's splash screen
	- favicon.png if the app runs in the browser
- components
	- react native components
- constants
	- contains colors.ts, which contains a list of color values throughout the app
- hooks
	- React Hooks, which allows sharing common behavior between components
- scripts
	- can be run with npm run
- app.json
	- config options for the project and is called the app config
- package.json
	- contains the project's dependencies, scripts, and metadata
- tsconfig.json
	- rules that Typescript will use to enforce type safety throughout the project

Expo  CLI
-  `npx expo start`
	- starts the development server
- `npx expo prebuild`
	- generate native Android and iOS directories using Prebuild
- `npx expo run:android | ios`
	- Compiles native Android/iOS app locally
- `npx expo install <package-name>`
	- used to install new library or update using `--fix`
- `npx expo lint`
	- setup and configure ESLint
- `npx expo-doctor`
	- diagnose issues in the project
	- check for common issues in app config and `package.json` files
	- dependency compatibility, config files, and the overall health of the project

**Expo Router**
- All screens/pages are files inside of app directory
	- navigation routes in the app are defined by the files and sub-directories inside the app
	- every files has  a default export that defines a distinct page in the app (except for the special `_layout.tsx` files)
- All pages have a URL
	- the IRL matches the file's location in the app directory
- First `index.tsx` is the initial route
	- you might put  all of the tab pages inside the app/(tabs) directory and define the default tab as `index.tsx` with this arrangement, the / URL will take the user directory to `app/(tabs)/index.tsx` file
- Root `_layout.tsx` replaces `App.jsx/tsx`
	- this files is rendered before any other route in the app and is where we would put the initialization code that may have previously gone inside an `App.tsx` file, such  as loading fronts or interacting with the splash screen.
- Non-navigation components live outside of app directory
	- In Expo router, the app directory is exclusively for defining the app's routes.

**App Routing**
- app
	- (tabs)
		- Home
		- Budget
		- Add (+ icon)
		- Finsights
		- Profile