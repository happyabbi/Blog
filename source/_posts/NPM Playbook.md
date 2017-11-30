---
title: NPM Playbook
categories:
- NPM
tags:
- NPM
---

# NPM Playbook
## NPM Help
- npm help install
- npm install -h
- npm -h
- npm help-search remove
- npm apihelp prune
- npm help prune

## NPM Shortcuts
- npm install = npm i

## Creating a Package.json
- npm init
- npm init -y

## Setting Defaults
- npm set init-author-name 'Abraham Chen'
- npm set init-license 'MIT'
- npm get init-author-name
- npm config delete init-author-name

## Installing Packages
- npm install XXX
- npm install XXX --save
- npm install XXX -S
- npm i XXX -S
- npm i karma -D

## Listing Installed Packages
- ls node_modules/
- npm list
- npm list --depth 1
- npm list --depth 0
- npm list --global true
- npm list --global true --depth 0
- npm list --depth 0 --long true
- npm list --depth 0 --j
- npm list --depth 0 --parseable true
- npm list --depth 0 --dev true
- npm list --depth 0 --prod true
- npm ls

## Installing Global Packages
- npm i gulp -g
- npm list -g --depth 0
- 

## Removing a Package
- npm uninstall underscore
- npm uninstall underscore --save
- npm rm underscore
- npm un underscore
- npm r underscore
- npm r underscore -g
- 