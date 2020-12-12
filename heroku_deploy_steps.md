=======
Deploy to Heroku
============
1.ng new demo-deploy
2.cd demo-deploy
3.ng serve
4.reate its GitHub repo and Push
5.git remote add origin <new_github_repository_url>
6.git add .
7.git commit -m "initial commit"
8.git push -u origin master
9.Login to heroku dashboard
10.Click Create app
11.In the Deploy menu, under Deployment method, select GitHub. 
12.Enter the name of the GitHub repository and click Search. 
13.Once the repo is shown below, click Connect
14.Under Automatic Deploys, select the master branch and click Enable Automatic Deploys.
15.Under Manual Deploys, click Deploy Branch. This is to push our fresh code to heroku.
16.npm install @angular/cli@latest @angular/compiler-cli --save-dev
17.In your package.json, copy
"@angular/cli”: “1.4.9”,
"@angular/compiler-cli": "^4.4.6", from devDependencies to dependencies
18.Under “scripts”, add a “heroku-postinstall” command like so:
"heroku-postbuild": "ng build --prod"
19.Add Node and NPM engines(run node -v and npm -v)
20. "engines": {
    "node": "12.20.0",
    "npm": "6.14.8"
  }

21.Copy "typescript": "~2.3.3" from devDependencies to dependencies
22.Run the command npm install enhanced-resolve@3.3.0 --save-dev
23.Install Server to run your app
Locally we run ng serve from terminal to run our app on local browser. But we will need to setup an Express server that will run our production ready app (from dist folder created) only to ensure light-weight and fast loading.
Install Express server by running:
24.npm install express path --save
25.Create a server.js file in the root of the application and paste the following code.
//Install express server
const express = require('express');
const path = require('path');

const app = express();

// Serve only the static files form the dist directory
app.use(express.static(__dirname + '/dist/deploy-demo'));

app.get('/*', function(req,res) {

  res.sendFile(path.join(__dirname+'/dist/<name-of-app>/index.html'));
});

// Start the app by listening on the default Heroku port
app.listen(process.env.PORT || 8080);

26.Change start command
In package.json, change the “start” command to node server.js so it becomes:
"start": "node server.js"

27. Push changes to GitHub:
git add .
git commit -m "updates to deploy to heroku"
git push

=========
