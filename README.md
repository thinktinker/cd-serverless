# cd-serverless
CD-serverless - updated on 15 Nov

```
git clone
git add .
git commit -m "commit message"
git push
```

To initialise the node application
```
npm init
```

Install serverless and serverless-offline
```
npm install serverless
npm install serverless-offline --save-dev
```

Added new files
- index.js
- serverless.yml
- .gitignore (node_modules, .serverless)

To test the serverless application using the installed plugin serverless-offline
Ensure that is serverless.yml, the framework version value is wrapped between single quote '...'
```
sls offline start
```

Test the serverless package (to check if the application is ready to deploy)
```
serverless package
```


Test the serverless service deployed to aws lambda

```
sudo serverless deploy
```

Check that the deployment is succesful to Lamda
In AWS Console
- Cloud Formation > Se the infrastructure
- AWS Lamda > deployed serverless application

In AWS Lamda:
- Function
- Application Name
- Configuration
- Triggers
- API Endpoint


Create a .github/workflows folder and > create new file in it called main.yml
Update the main.yml to run the jobs in github actions.


