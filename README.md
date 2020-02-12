[![Build Status](https://travis-ci.org/isa-group/oas-wizard.svg?branch=master)](https://travis-ci.org/isa-group/oas-wizard) 
[![Greenkeeper badge](https://badges.greenkeeper.io/isa-group/oas-wizard.svg)](https://greenkeeper.io/) 
[![Known Vulnerabilities](https://snyk.io/test/github/isa-group/oas-wizard/badge.svg?targetFile=package.json)](https://snyk.io/test/github/isa-group/oas-wizard?targetFile=package.json)
[![dependencies Status](https://david-dm.org/isa-group/oas-wizard/status.svg)](https://david-dm.org/isa-group/oas-wizard)

*oas-wizard* is a simple OpenAPI Spec generator using a (yaml) resource sample as starting point

## Usage

The command sintax is: 
`node index <OpenAPISpecFile.yaml> <ResourceSampleFile.yaml> <Prefix> <ResourceName> <IdPropertyName>`

This tool is expected to be used in combination with others; as an example we propose the following lifecycle:
 - Think about an example of resource and write it in yaml (e.g. `petSample.yaml`)
  ```yml
name: rocket
owner: paul
species: dog
breed: beagle
age: 7
```
 - Use *oas-wizard* to generate the OAS spec (`tests/pet-oas.yaml`) based on the sample file (`tests/static/petSample.yaml`) using as resouce name `pet` with the id property `name`
   ```bash
   node index tests/pet-oas.yaml tests/static/petSample.yaml pet name
   ```
 - Generate a server scaffolding with  https://www.npmjs.com/package/oas-generator (using node v8 or up) 
   ```bash
   npm install oas-generator -g
   cd tests
   oas-generator pet-oas.yaml -n pet-api
   cd pet-api
   npm start
   ```
- Now you have a fully working API server mockup up and running in port 8080. You can check the SwaggerUI API documentation `localhost:8080/docs`
- Implement the controllers for each operation (files  `controllers/*Service.js`).
- Enjoy your API!
 
