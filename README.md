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

```yml
name: CICD for Serverless Application
run-name: ${{ github.actor }} is doing CICD for serverless application

on:
  push:
    branches: [ main, "*"]

jobs:
  pre-deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event"
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."

  install-dependencies:
    runs-on: ubuntu-latest
    needs: pre-deploy
    steps:
      - name: Check out repository code
        uses: actions/checkout@v3
      - name: Run Installation of Dependencies Commands
        run: npm install
```

Further update main.yml to:

```yml
name: CICD for Serverless Application
run-name: ${{ github.actor }} is doing CICD for serverless application

on:
  push:
    branches: [ main, "*"]

jobs:
  pre-deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event"
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."

  install-dependencies:
    runs-on: ubuntu-latest
    needs: pre-deploy
    steps:
      - name: Check out repository code
        uses: actions/checkout@v3
      - name: Run Installation of Dependencies Commands
        run: npm install

  deploy:
    name: deploy
    runs-on: ubuntu-latest
    needs: install-dependencies
    strategy:
      matrix:
        node-version: [18.x]
    steps:
    - uses: actions/checkout@v3
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm ci
    - name: serverless deploy
      uses: serverless/github-action@v3.2
      with:
        args: deploy
      env:
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```