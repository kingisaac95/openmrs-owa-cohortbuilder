[![Build Status](https://travis-ci.org/openmrs/openmrs-owa-cohortbuilder.svg?branch=master)](https://travis-ci.org/openmrs/openmrs-owa-cohortbuilder)
[![Coverage Status](https://coveralls.io/repos/github/openmrs/openmrs-owa-cohortbuilder/badge.svg?branch=master)](https://coveralls.io/github/openmrs/openmrs-owa-cohortbuilder?branch=master)
<img src="https://cloud.githubusercontent.com/assets/668093/12567089/0ac42774-c372-11e5-97eb-00baf0fccc37.jpg" alt="OpenMRS"/>

# CohortBuilder

This repository contains the CohortBuilder OpenMRS Open Web App.

> Add a description of what your app does here.

For further documentation about OpenMRS Open Web Apps see
[the wiki page](https://wiki.openmrs.org/display/docs/Open+Web+Apps+Module).

## Getting Started

### Local Setup Instructions

```
# Get the project
git clone https://github.com/openmrs/openmrs-owa-cohortbuilder.git

# Move into the project directory
cd openmrs-owa-cohortbuilder

# Install the dependencies
npm install

# Copy the webpack configuration from webpack.config.sample.js to webpack.config.js
cp webpack.config.sample.js webpack.config.js

# Locate appdata\owa folder and copy the path
pwd | pbcopy

# Open the webpack.config.js file, locate the getConfig function and update the config object with the following
{
  "LOCAL_OWA_FOLDER": "PASTE_THE_PATH_YOU_COPIED_HERE",
  "APP_ENTRY_POINT": "http://localhost:8081/openmrs-standalone/owa/cohortbuilder/index.html"
}

Note: Start your cohort builder standalone server locally. Make sure you tomcat port is 8081, if not, change the APP_ENTRY_POINT localhost port to be the same as your tomcat port.

# Run the app
npm run watch
```

## Development

### Production Build

You will need NodeJS 4+ installed to do this. See the install instructions [here](https://nodejs.org/en/download/package-manager/).

Once you have NodeJS installed, install the dependencies (first time only):

```sh
npm install
```

Build the distributable using [Webpack](https://webpack.github.io/) as follows:

````sh
npm run build:prod
````

This will create a file called `cohortbuilder.zip` file in the `dist` directory,
which can be uploaded to the OpenMRS Open Web Apps module.

### Local Deploy

To deploy directly to your local Open Web Apps directory, run:

````
npm run build:deploy
````

This will build and deploy the app to the `/home/sims01/openmrs/openmrs-server/owa`
directory. To change the deploy directory, edit the `LOCAL_OWA_FOLDER` entry in
`config.json`. If this file does not exists, create one in the root directory
that looks like:

```js
{
  "LOCAL_OWA_FOLDER": "/home/sims01/openmrs/openmrs-server/owa"
}
```

### Live Reload

To use [Browersync](https://www.browsersync.io/) to watch your files and reload
the page, inject CSS or synchronize user actions across browser instances, you
will need the `APP_ENTRY_POINT` entry in your `config.json` file:

```js
{
  "LOCAL_OWA_FOLDER": "/home/sims01/openmrs/openmrs-server/owa",
  "APP_ENTRY_POINT": "http://localhost:8080/openmrs/owa/cohortbuilder/index.html"
}
```
Run Browsersync as follows:

```
npm run watch
```

### Extending

Install [npm](http://npmjs.com/) packages dependencies as follows:

````sh
npm install --save <package>
````

To use the installed package, import it as follows:

````js
//import and assign to variable
import variableName from 'package';
````

To contain package in vendor bundle, remember to add it to vendor entry point array, eg.:

````js
entry: {
  app : `${__dirname}/app/js/owa.js`,
  css: `${__dirname}/app/css/owa.css`,
  vendor : [
    'package',
    ...//other packages in vendor bundle
  ]
},
````

Any files that you add manually must be added in the `app` directory.

### Troubleshooting

##### [HTTP access control (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)

You may experience problems due to the `Access-Control-Allow-Origin` header not
being set by OpenMRS. To fix this you'll need to enable Cross-Origin Resource
Sharing in Tomcat.

See instructions [here](http://enable-cors.org/server_tomcat.html) for Tomcat 7 and [here](https://www.dforge.net/2013/09/16/enabling-cors-on-apache-tomcat-6/) for Tomcat 6.

## License

[MPL 2.0 w/ HD](http://openmrs.org/license/)
