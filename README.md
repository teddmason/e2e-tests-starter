# e2e-tests-starter

## Starter project for stand-alone nightwatch e2e tests

Note that the drivers in the /bin directory will need to be updated when cloning.

The tests are set up using [page objects](http://nightwatchjs.org/guide#page-objects) within [pages](./pages/).

#### Seperation of concerns is as follows:

Tests are driven in a page structure from [tests](./tests/)

Pages are constructed within [pages](./pages), consisting of the page's elements and interations/commands, and initialised using `client.page.home()`

Page assertions are held in [assertions](./assertions/)

### Setup
The e2e tests are designed to be stored as their own project, so that they can be run stand alone or included in your build CI.

* Clone the repository into your own e2e-test repository
* `npm i` Note that nightwatchjs and chrome drivers are included in the npm install, but selenium driver and the tunnels need to be updated manually.
* Update the default urls in the config
* Code your tests

### Running tests with local selenium server
Using default url in config `npm run test-e2e-local`

Or you can provide a url parameter `npm run test-e2e-local -- --url https://www.gov.uk`

Environments can be set, such as `default`, `chrome` or `phantomjs` within the `package.json` script's command for `test-e2e-local`, the default is set to `chrome` but `phantomjs` is also included in the package.

## Setting up remote selenium testing through browserstack or saucelabs.

note some work needs performing on the browserstack/saucelabs config files to convert to js files to enable url parameterisation

### Remote test (BROWSERSTACK)

Need environment variables for, BS user and key:

`export BS_USER=
export BS_KEY=`

Browserstack tunnel then needs setting up, either download the latest binary [from here](https://www.browserstack.com/automate/node#setting-local-tunnel) and go to /bin and run `./BrowserStackLocal $BS_KEY`

With this running in a terminal you'll then be able to run tests against your localhost or a private domain ie dev/test

To setup bespoke environments for testing use the tool at https://www.browserstack.com/automate/node#firefox-profile to select browser/os/screensize and it gives the config options

### Remote test (Sauce labs)

In your environment variable location add, populated with the saucelabs connection details:

`export SAUCE_USERNAME=
export SAUCE_ACCESS_KEY=`

If you are wanting to test your localhost using sauce labs then a tunnel will need to be created for the remote to access your local.  This is done through Sauce Connect.  See https://wiki.saucelabs.com/display/DOCS/Setting+Up+Sauce+Connect

In the terminal run:

`/bin/sc -u ${SAUCE_USERNAME} -k ${SAUCE_ACCESS_KEY} -B all`

This will need to be left running whilst the remote tests are run:

`npm run test-e2e-remote`
