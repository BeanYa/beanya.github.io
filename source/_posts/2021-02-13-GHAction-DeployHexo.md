---
title: Deploy Demo
categories:
  - Note
tags:
  - Note
date: 2021-02-13 00:00:00
---

# Github Action script

name: Build and Display

on:
  push:
    # 配置分支
    branches: [source]
  workflow_dispatch:

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Check out
      uses: actions/checkout@v2.3.4
    - name: set up node
      uses: actions/setup-node@v2.1.4
      with:
        node-version: 14.x
    - name: Install hexo
      run: |
        npm install hexo-cli -g
        npm install hexo --no-optional
    - name: Build
      run: hexo g
    - name: Commit
      run: |
        git config --local user.email "beanya@github.github.com"
        git config --local user.name "beanya"
        git add .
        git commit -m "Commit by Github Action" -a
    - name: Push
      uses: ad-m/github-push-action@master
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        branch: ${{ github.ref }}