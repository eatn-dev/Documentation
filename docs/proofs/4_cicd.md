# Continuous integration and continuous development

---

- [Continuous integration and continuous development](#continuous-integration-and-continuous-development)
  - [Intro](#intro)
    - [Design and implement](#design-and-implement)
  - [What is continuous integration and development?](#what-is-continuous-integration-and-development)
  - [What does "CI/CD" mean encompass in regards to learning outcomes?](#what-does-cicd-mean-encompass-in-regards-to-learning-outcomes)
  - [My achievements](#my-achievements)
    - [Unit testing](#unit-testing)
    - [Integration testing](#integration-testing)
    - [Pipeline setup](#pipeline-setup)


## Intro

*You design and implement a (semi)automated software release process that matches the needs of the project context.*

### Design and implement

*You design a release process and implement a continuous integration and deployment solution (using e.g. Gitlab CI and Docker).*

## What is continuous integration and development?

Continuous Integration (CI) is a software development practice where developers regularly merge their code changes into a shared repository. The main goal of CI is to automate the process of integrating code changes from multiple developers, ensuring that the changes are merged smoothly and without conflicts. It involves setting up a CI pipeline that automatically builds and tests the code whenever changes are pushed to the repository. This allows developers to detect issues early on and ensure that the codebase is always in a releasable state.

Continuous Deployment (CD), on the other hand, is an extension of CI that takes the automation further by automatically deploying the tested and approved code changes to production environments. With CD, every successful code change that passes through the CI pipeline is automatically deployed to staging or production environments, reducing the manual effort required for releases. CD enables faster and more frequent releases, providing organizations with the ability to deliver new features and bug fixes to end-users in a reliable and efficient manner.

## What does "CI/CD" mean encompass in regards to learning outcomes? 


In regards to learning outcomes, "CI/CD" encompasses the understanding and proficiency in implementing Continuous Integration (CI) and Continuous Deployment (CD) practices. This includes knowledge of setting up CI pipelines, automating code integration, build processes, writing and running automated tests. It also involves understanding CD principles, automating deployment processes, managing environments, and ensuring the smooth release of software changes. Mastery of CI/CD learning outcomes entails the ability to establish efficient and reliable software delivery pipelines, improving collaboration, code quality, and the speed at which software is deployed and delivered to end-users.

## My achievements

I will split my achievements in 3 chunks: [unit testing](#unit-testing), [integration testing](#integration-testing) and [setting up pipelines](#pipeline-setup).

### Unit testing

To see this in more detail, visit [code quality proof](./2_code_quality.md).

### Integration testing

To see this in more detail, visit [code quality proof](./2_code_quality.md).

### Pipeline setup

To guarantee customer/users are interacting with working code, frequent code testing, integrating and deployment are necessary. Automated tests are the best way to ensure exactly that.

I used Github's Actions to create an environment which executes said test on every commit and merge request. These pipelines not only ensure code is tested, but make sure it build properly, enforce code style and statically analyse code for any imperfections that escape human eye.

```yaml
# pipeline for integration testing
# This workflow will do a clean installation of node dependencies, cache/restore them, build the source code and run tests across different versions of node
# For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

name: Cashier frontend CI/CD
run-name: Build, lint, test and deploy coverage

env:
  GATEWAY_URL : "http://localhost:54321"

on:
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      max-parallel: 1
      matrix:
        node-version: [18.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
    - uses: actions/checkout@v3
      with:
          fetch-depth: 0
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
        
    - name: Install depenencies
      run: npm ci --legacy-peer-deps
        
    - name: Build and compile website
      run: npm run build
    
    - name: Lint
      run: npm run lint
    
    - name: Run tests and collect coverage
      run: npm run test
      
    - name: SonarCloud Scan
      uses: sonarsource/sonarcloud-github-action@master
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}

```

```yaml
# pipeline for unit tests
# This workflow will do a clean installation of node dependencies, cache/restore them, build the source code and run tests across different versions of node
# For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

name: Menu API CI/CD
run-name: Build, lint, test and deploy coverage

env:
  DB_URI : "sqlite::memory:"

on:
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]

jobs:
  menu:
    runs-on: ubuntu-latest

    strategy:
      max-parallel: 1
      matrix:
        # node-version: [18.x, 19.x]
        node-version: [18.x]
        
    steps:
    - uses: actions/checkout@v3
      with:
        fetch-depth: 0
    - name: Build
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
    
    - name: Install depenencies
      run: npm ci
    
    - name: Lint
      run: npm run lint
    
    - name: Run tests and collect coverage
      run: npm run test
    
    - name: SonarCloud Scan
      uses: sonarsource/sonarcloud-github-action@master
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```