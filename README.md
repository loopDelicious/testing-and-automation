![[postman](https://assets.getpostman.com/common-share/postman-logo-horizontal-320x132.png)](https://assets.getpostman.com/common-share/postman-logo-horizontal-320x132.png)]

Follow this example of API testing and automation in [Postman](https://www.getpostman.com/).

## Pre-requisites
1. Download the [Postman app](https://www.getpostman.com/downloads/) for Mac, Windows, or Linux. Make sure you have a Postman account, and you're logged in.
1. To run Newman, [download and install Node.js](http://nodejs.org/download/), and then [install Newman](https://www.npmjs.org/package/newman). This step is optional.

## Getting Started

### Writing an API test

There are many types of API tests that you can write using Postman.

* API unit tests
* Integration tests
* End-to-end or scenario tests
* Etc.

The basic [syntax of a test in the Postman app](https://learning.getpostman.com/docs/postman/scripts/test_scripts) looks like this:

```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
})
```

For more tutorials and interactive examples of the types of API tests that you can write using Postman, you can reference community-contributed [templates](https://learning.getpostman.com/docs/postman/launching_postman/newbutton/#templates). For example, in the Postman app, go to the orange **+New** button > **Templates** tab > import the **Intro to Writing Tests - with Examples** template.

### Running API tests

There's a few options to run API tests in Postman.

* Run API tests associated with a request by [sending a single request](https://learning.getpostman.com/docs/postman/launching_postman/sending_the_first_request)
* Run API tests associated with multiple requests by [running a collection](https://learning.getpostman.com/docs/postman/collection_runs/intro_to_collection_runs) containing the requests using the collection runner
* Use [Newman](https://github.com/postmanlabs/newman) to run your collection from the command line

Once you're done writing your API tests, use the [Postman API](https://docs.api.getpostman.com/) to [GET the latest version of your collection](https://docs.api.getpostman.com/?version=latest#647806d5-492a-eded-1df6-6529b5dc685c) (and [environment](https://docs.api.getpostman.com/?version=latest#96c34392-1e36-d1cb-af89-1c95365184ab) if you're using one). In this example, `{{collection_uid}}` is the uid of the collection you want to retrieve and `{{postman-api-key}}` is your [Postman API key](https://docs.api.getpostman.com/?version=latest#authentication).

    $ newman run https://api.getpostman.com/collections/{{collection_uid}}?apikey={{postman-api-key}}

If you don't anticipate making any changes to your API requests and tests, you can also [export your collection](https://learning.getpostman.com/docs/postman/collections/data_formats/#exporting-postman-data) (and environment if you're using one). Then run your collection by referring to a local version of the collection. In this example, `myCollection.json` is a JSON file located within the directory from which the command is being executed.

    $ newman run myCollection.json
    $ newman run myCollection.json -e myEnvironment.json // if you're using an environment

You can also [configure a reporter](https://github.com/postmanlabs/newman#reporters) to customize the output of your results. In this example, the collection run results will be output in the command line interface as well as generating a new JSON file.

    $ newman run myCollection.json -r cli,json

### Automating API testing

There's a few options to automate API testing in Postman. Just like running a single or a couple API tests, you can choose your level of automation.

* Run a script that uses [Newman as a package](https://github.com/postmanlabs/newman#using-newman-as-a-library)
* Schedule a collection run [using a monitor from Postman servers](https://learning.getpostman.com/docs/postman/monitors/intro_monitors)
* Use [Newman along with your Continuous Integration / Continuous Deployment (CI/CD) pipeline tool](https://learning.getpostman.com/docs/postman/collection_runs/integration_with_jenkins) to run your tests prior to deploying any code to a server environment
