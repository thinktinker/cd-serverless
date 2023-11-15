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
- .gitignore

To test the serverless application using the installed plugin serverless-offline
Ensure that is serverless.yml, the framework version value is wrapped between single quote '...'
```
sls offline start
```