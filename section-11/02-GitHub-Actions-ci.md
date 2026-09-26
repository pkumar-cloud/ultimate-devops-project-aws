# Github Action
- GitHub actions is basically the CI orchestrator that is provided by GitHub.
- When you have your repo in GitHub, create a folder **".github/workflows/<xyz.yaml>"**. This YAML file provides all the instructions (github actions) on what needs to be run and defines a workflow.
- GitHub provides 1000's of actions are like plugins or the modules.
  <img width="1397" height="590" alt="image" src="https://github.com/user-attachments/assets/394891f5-bb9c-4194-bef2-7f4a56c7b9e6" />
- Sample: https://github.com/pkumar-cloud/ultimate-devops-project-demo/edit/main/.github/workflows/ci.yaml
- Structure:
```
name: product-catalog-ci
on: 
   pull_request:
     branches:
       - main
   push:
     branches:
       - main
jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        run go test src/product-catalog/...
```
# Test/Execute Github Actions CI
- Update the source code e.g. src/product-catalog/main.go, so that github ci triggers on pull-request.
```
cd ultimate-devops-project-demo
git checkout -b githubcicheck
Update the source code src/product-catalog/main.go
git status
git add .
git commit -am "chore: verify github actions"
git push origin githubcicheck
copy PR URL and launch in browser and create a PR
Will run all 4 jobs from ci.yaml
```
- This completes CI part. 
