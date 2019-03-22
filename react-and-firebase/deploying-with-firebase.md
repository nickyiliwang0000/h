<!-- Student takeaway: -->
<!--Student will be able to:
- Run the build command to create a set of production files for a React app
- Follow these instructions to deploy their Firebase project
- Know to re-run build and re-deploy if they make changes to their app
 -->

# Deploying with Firebase

In the past, when we've wanted to launch our sites on the web, we have needed to rely on FTP. Not so with Firebase!

## Running the build script

When we are using `create-react-app`, we will want to run the `build` script before deploying in order to generate a version of our project that is optimized for performance.

To do this, go into the root folder of your React application in the terminal, run `npm run build`. When this is complete, there will be a new `/build` folder in your project's root directory. Always ensure there are no fatal errors that exist in your codebase or else the `build` process will not finish successfully. 

Firebase has its own _command line interface_ (CLI) that will take care of deploying our app for us.

## Firebase deployment steps

### New project

1. Open the terminal, and navigate to your project folder.

2. Install the Firebase Tools: `npm install -g firebase-tools` (If you get an error try running `sudo npm install -g firebase-tools`)

3. Login using `firebase login` - this should open your browser. Follow the web prompts to continue to log in. You should see something in your command prompt that looks like this: `✔ Success! Logged in as youremail@hackeryou.com`

4. In your project folder, type `firebase init`. This will begin the setup to deploy your Firebase project.

5. Next, it will ask you what Firebase CLI features you want to set up. Use the arrow keys to move down to **hosting**. note: **Make sure you hit spacebar to select your option before hitting enter - the circle should be filled in!**

6. Next, it will ask you to select a default Firebase project for this directory - pick the name of the Firebase database currently attached to your project. If you're not sure, check the config object inside the `firebase.js` file within your app.

** If you don't see your Firebase project as an option to select, follow the steps [here](#When-the-default-project-is-not-available).

7. When it asks you for your directory, specify `build` for create-react-app.

8. For `configure as a single page app`, select 'yes'.

9. It will say that `index.html` already exists, and asks you if you want to overwrite. 🚨Select **no**!🚨

10. We're almost done - select `firebase deploy` to launch your app!

```bash
=== Deploying to 'movie-catalogue-6f972'...

i  deploying database, hosting
✔  database: rules ready to deploy.
i  hosting: preparing ./ directory for upload...
Uploading: [========================================] 99%✔  hosting: ./ folder uploaded successfully
✔  hosting: 13338 files uploaded successfully
i  starting release process (may take several minutes)...

✔  Deploy complete!

Project Console: https://console.firebase.google.com/project/movie-catalogue-6f972/overview
Hosting URL: https://movie-catalogue-6f972.firebaseapp.com
```

And that's all there is to it! 🔥Firebase app deployed🔥

#### When the default project is not available

- Select the `create a new project` option.
- For `Hosting Setup,` specify `build`.
- Type `Y` for configuring as a single-page app.

1. From here, your firebase initialization will be complete. Following the prompt, enter `firebase use --add` to see a list of all available Firebase projects you have stored. *HERE* you should see your desired project. Select it.

2. It will ask you to choose an alias for this project. Conventional choices are `staging`, `production` or `development`. For our purposes this doesn't really matter so we can default to `staging`. If desired, more information can be found [here](https://firebase.googleblog.com/2016/07/deploy-to-multiple-environments-with.html).

3. Run `firebase deploy` to launch your app! 

### Updating an existing project

For create-react-app: If you want to make updates to your project, do so. Then, when you're ready to re-deploy , run `npm run build` again, and then run `firebase deploy`.
