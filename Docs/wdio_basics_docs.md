# WebdriverIO Documentation

**@author: Saksham Varshney**

### Introduction:
	1. Built on Node.js engine
	2. It uses JS to code the automation
	3. It uses Selenium under hood

### Pre-requisite:
	1. Install Node.js (Reason: it requires some engine to run)
	2. Set Node Home in Environment
	3. node -v (To check the node version)
	4. Install VS code

### Create NPM Project:
	1. It is a package manager (Central Repo) just like Maven
	2. To initialize the new project: npm init
	3. To agree with the default values: npm init -y
	4. It will create package.json

### Install Wdio cli dependencies:
	npm i --save-dev @wdio/cli

### Why install WDIO CLI Options / Dependencies:
	1. WebdriverIO comes with its own test runner to help you start testing as quickly as possible
	2. Starting with v5 (WebdriverIO version), WebdriverIO's testrunner is bundled separately in the NPM package @wdio/cli

### Launch URL:
	browser.url(url)

### Launch URL in New tab:
	browser.newWindow(url)

### How to Get single locator:
	${locator}

### How to Get multiple locators:
	$${locator}

### Switch to new window (Parent to child Window):
	var handles= browser.getWindowHandles() // 0th index: for parent window, 1st index: for child window
	browser.switchToWindow(handles[index])

### Switch tab
	browser.switchWindow(url or index)

### Switch Frame:
	browser.switchToFrame(loctor or index)
	browser.switchToFrame(null): It will switch to the page's default content

### Close browser:
	browser.closeWindow()
	
### Maximize Window:
	browser.maxmizeWindow()

### Scroll an element:
	${locator}.scrollIntoView()

### Wait for an element to exist:
	locator.waitForExist()
	locator.waitForExist({reverse:true}) // It is for not exist element

### Split an element:
	element.split('.')

### Trim an element:
	element.trim()

### Convert String to Integer:
	parseInt(element)

### Fat arrow function:
	1. Introduced in ES6
	2. Symbol: ()=>{}
	3. Sample code:
		describe(description, ()=>{
			it(description, ()=>{})
		})

### Sample code for test scripts:
**First way: (After ES6):**

	describe(description, ()=>{
		it(description, ()=>{})
	})	

**Second way: (Before ES6):**

	describe(description, function(){
		it(description, function(){})
	})

### How to Iterate the it block:
	const fs= require('fs')
	let data= JSON.parse(fs.readFileSync(json file path))

	describe(Title, ()=>{
		data.forEach(({arguments})=>{
			it(Title, ()=>{})
		})
	})

### WDIO Assertions:
	expect(locator).toHaveTextContaining(expectValue)

### Filter & Map & Reduce:
**Example of Filter & Map:**

	elements= $${locator}
	elements.filter(tempVar=>tempVar.getText() === expectedText).map(tempVar2=>tempVar2.click())

**Example of Fiter & Map with array:**

	var products= ['productA', 'productB']
	elements= $${locator}
	elements.filter(tempVar=>products.includes(tempVar.getText())).map(tempVar2=>tempVar2.click())

**Example of Reduce:**

	.reduce((acc,price)=> acc + price,0)

### Retry Flaky tests:
Retry Flaky tests are those tests which can Fail at once but pass on retry

Put the below code in it block:

	this.retries(2)

**Disadvantage:** In order to use this retry function the suite / test block must use unbound function **function(){}** instead of a fat arrow function **()=>{}**

### Execute only Selected it blocks:
e.g. Execute scripts for Smoke testing

Put Smoke or any keyword in **it block description** 

**Command to execute:** npx wdio run wdio.conf.js --mochaOpts.grep **Keyword**

**Alternative:**

Make the below changes in wdio config file as:

	mochaOpts: {
		ui:'bdd'
		timeout: 60000,
		grep: "Keyword Name suppose Sanity"
	}

### Execute test scripts without wdio config spec property:
	npx wdio run wdio.conf.js --spec testFilePath

### Exclude any test script:
Put exclude property below specs property as

	specs: [],
	exclude: ['test/specs/testFileName.js']

### Suites in WDIO:
	suites: {
		suite01: [test file path, test file path],
		suite02: [test file path]
	}
	
**Command to execute:** npx wdio run wdio.conf.js --suite suiteName

### Execute test via scripts in package.json file:
	"Scripts": {
		"scriptName": "npx wdio run wdio.conf.js --suite suiteName"
	}

**Command to execute:** npm run scriptName

### How to Scripts run in Headless Mode:
Put this code after browser config property in wdio config file, or enable the args argument if already exists

	goog:chromeOptions': {
        // to run chrome headless the following flags are required
        // (see https://developers.google.com/web/updates/2017/04/headless-chrome)
        args: ['--headless', '--disable-gpu'],
    }

### Bail in WDIO config file:
	bail:0 : By default: It will run all tests
	bail:3 : It will stop the script execution after 3 tests failure

### New wdio conf file:
**Requirement:** If need to override some wdio config property for different different environments

**File Name:** e.g: wdio.uat.conf.js

	const merge = require('deepmerge')
	const wdioConf= require('./wdio.conf.js')

	exports.config= merge(wdioConf.config, {
		baseUrl: 'New base url'
		waitforTimeout: 5000
	})

**Command to execute:** npx wdio run wdio.uat.conf.js

### Allure report:
	npm install @wdio/allure-reporter --save-dev // Importing Allure Library
	npm install -g allure-commandline --save-dev // Installing Allure Commandline globally in system, it will generate xml files
	allure generate allure-results && allure open // It will convert xml files to HTML ones and can show the report in their servers
---
