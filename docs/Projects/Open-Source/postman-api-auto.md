# Valentino Artisan Coffee House API

## Introduction
The Postman API Test Automation Certification Program developed by Valentin Despa is an educational program aimed at helping developers learn API testing and automation using Postman. This program, available through platforms like freeCodeCamp and Postman's API Network, offers structured lessons that guide users through the essential aspects of API test automation, including request creation, response validation, and automation scripting in Postman.

Valentin Despa, a recognized software developer and instructor in the Postman community, created this certification to cater to beginners and professionals looking to deepen their understanding of Postman’s API testing capabilities. Despa’s courses often use practical, hands-on projects, such as a coffee shop API scenario, which allow participants to practice setting up test scenarios and automating workflows in a real-world-like environment.

Upon completing the course assignments, participants can earn a digital badge to showcase their skills, which can be shared on LinkedIn or other professional networks. While some users have reported delays in badge issuance, Postman’s community and support teams are generally available to help resolve these issues​

## Role
- Quality Assurance Engineer

## Goals
1. **Establish Foundational Knowledge**
    - Train the team in fundamental Postman operations, including creating requests, managing collections, and using environment variables effectively.
    - Build confidence in using Postman as a central tool for API testing
2. **Adopt Best Practices in Test Automation**
    - Implement automation scripts within Postman collections using JavaScript for response validation, data-driven testing, and workflow automation.
    - Follow structured approaches for writing reusable and maintainable tests
3. **Simulate Real-World Scenarios**
    - Design and execute test cases using projects like the "Artisan Coffee House API", a sample API Despa uses to teach realistic automation scenarios.
    - Create scenarios to test API endpoints for functionality, reliability, and error handling
4. **Enhance Collaboration Through Postman Workspaces**
    - Share collections and environments within the team for consistent testing and review.
    - Use Postman’s collaboration features to streamline feedback and iteration during the development and testing lifecycle
5. **Integrate Postman with CI/CD Pipelines**
    - Learn to execute Postman tests through GitHub Action in CI/CD pipelines to enable continuous validation.
    - Automate regression test suites and integrate test reports with tools like GitHub Action
6. **Focus on Learning and Certification**
    - Encourage team members to complete Valentin Despa’s API Test Automation courses to build comprehensive skills.
    - Use Postman’s certification as a milestone for team development and benchmarking
7. **Expand API Test Coverage**
    - Test for functional correctness, edge cases, performance, and security to achieve comprehensive coverage.
    - Leverage data-driven testing techniques taught by Despa to simulate multiple real-world use cases
8. **Develop and Share Knowledge Resources**
    - Create internal documentation and tutorials, similar to Despa's educational style, to ensure the team’s continuous learning.
    - Organize workshops or knowledge-sharing sessions to instill best practices

## Resource Overview

### Assignment #1

#### Task

Task 1

Add to the request "Get API status" a Postman test that verifies the status is 200.
Once you have established that the test is working as expected, duplicate the request and drag it inside the "Assignment #1" collection and put it in the "API requests" folder. Ensure the name of the request remains the same.

Task 2

Add to the request "Get single product" a script that parses the JSON response body. Log the value of the property "product-description" to the Postman console.
Once you have established that the script is working as expected, duplicate the request and drag it inside the "Assignment #1" collection and put it in the "API requests" folder. Ensure the name of the request remains the same.

Task 3

Add to the request "Create a new order" a script that parses the JSON response body and sets a Postman variable named orderId with the id of the order that was just created.
Once you have established that the script is working as expected, duplicate the request and drag it inside the "Assignment #1" collection and put it in the "API requests" folder. Ensure the name of the request remains the same.


#### Solution

???+ abstract "Postman Collection"
    === "Task 1 "
        ``` JavaScript title="Get API Status"
        pm.test("Status code is 200", function () {
            pm.response.to.have.status(200);
        });
        ```
    === "Task 2"
        ``` JavaScript title="Get single product"
        const response = pm.response.json();
        console.log(response);
        console.log(response.id);
        console.log(response['product-description']);

        pm.test("Status code test: 200", function () {
            pm.expect(pm.response.code).to.eql(200);
        });
        ```
    === "Task 3"
        ``` JavaScript title="Create a new order"
        pm.test("Status code is 200", function () {
            pm.response.to.have.status(200);
        });

        const response = pm.response.json();

        pm.collectionVariables.set('orderID', response.id);
        ```
### Assignment #2

#### Task

Using pm.expect() write a status code test for all the requests in the collection.

#### Solution

???+ abstract "Postman Collection"
    === "Task "
        ``` JavaScript title="add to all endpoint Post-res"
        pm.test("Status code test: 200", function () {
            pm.expect(pm.response.code).to.eql(200);
        });
        ```

### Assignment #3

#### Task

All of the following tasts refer to the request "Get an order by ID".

Task 1

Write an assertion to verify that the response is in JSON format.

Task 2

Write a test with two assertions to verify the following:
The existence of the property "id" in the response.
The value of the "id" property matches the regular expression pattern: ^[A-Z0-9]{9}$.

Task 3

Write a test with two assertions to verify the following:
The existence of the property "products" in the response.
The value of the "products" property is an array.

#### Solution

???+ abstract "Postman Collection"
    === "Task 1 "
        ``` JavaScript title="Get an order by ID"
        let response;

        pm.test("Response body is JSON", function(){
            pm.response.to.be.json;
            response = pm.response.json();
        });
        ```
    === "Task 2"
        ``` JavaScript title="Get an order by ID"
        pm.test("Get Property ID on JSON", function(){
            pm.expect(response).to.have.property('id');
                pm.expect(response.id).to.match(/^[A-Z0-9]{9}$/);
                });
        ```
    === "Task 3"
        ``` JavaScript title="Get an order by ID"
        pm.test("Get Property products on JSON", function(){
                pm.expect(response).to.have.property('products');
            pm.expect(response.products).to.be.a('array');
        });
        ```

### Assignment #4

#### Task

For the request "Get single product" you will need to write a JSON schema and test with an assertion that verifies if the response body matches the JSON schema.

Task 1

The JSON schema expects that the response is an object.

Task 2

Expand the JSON schema and ensure that all properties present in the response body are required.

Task 3

Expand the JSON schema and ensure that no additioanl properties are allowed.

#### Solution

???+ abstract "Postman Collection"
    === "Task 1 "
        ``` JavaScript title="Get single product"
        let response;
        pm.test("Response body is JOSN", function(){
            pm.response.to.be.json;
            response = pm.response.json();
            console.log(response['product-description']);
        });
        ```
    === "Task 2"
        ``` JavaScript title="Get single product"
        pm.test("JSON Schema are valid", function(){
            const schema = {
                'type': 'object',
                'properties': {
                    'id': {
                        'type': 'integer'
                    },
                    'category': {
                        'type': 'string'
                    },
                    'name': {
                        'type': 'string'
                    },
                    'isAvailable': {
                        'type': 'boolean'
                    },
                    'product-description': {
                        'type': 'string'
                    },
                    'additionalText': {
                        'type': 'string'
                    }                      
                },
                'required': ['id','category','name','isAvailable','product-description','additionalText']
            };
            pm.response.to.have.jsonSchema(schema);
        });   
        ```
    === "Task 3"
        ``` JavaScript title="Get single product"
        'additionalProperties': false
        ```

### Assignment #5

#### Task

Task 1

Create a public GitHub project and configure a GitHub Actions workflow. Ensure the workflow is stored in the following location:

``` PowerShell title="PowerShell"
.github/workflows/postman.yml

```

Task 2

Once you have created the Postman workflow, ensure that the Postman collection run is successful.

#### Solution

???+ abstract "GitHub Action Setup & Collection Runner"
    === "Task 1 "
        ``` PowerShell title="postman.yml"
        name: Automated API tests using Postman CLI

        on: push

        jobs:
        automated-api-tests:
            runs-on: windows-latest
            steps:
            - uses: actions/checkout@v4
            - name: Install Postman CLI
                run: |
                powershell.exe -NoProfile -InputFormat None -ExecutionPolicy AllSigned -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://dl-cli.pstmn.io/install/win64.ps1'))"
            - name: Login to Postman CLI
                run: postman login --with-api-key ${{ secrets.POSTMAN_API_KEY }}
            - name: Run API tests
                run: |
                postman collection run "36196810-3064f937-caa2-4035-bcda-b75336216fc5"
        ```
    === "Task 2"
        ``` JavaScript title="GitHub Action Run API Test Log"
        Run postman collection run "36196810-3064f937-caa2-4035-bcda-b75336216fc5"
        
        Running your collection...
        postman

        Valentino Artisan Coffee House API

        □ status
        └ Get API status

        ┌
        │ 
        └
        GET https://valentinos-coffee.herokuapp.com/status [200 OK, 783B, 329ms]
        √  Status code is 200
        √  Headers Test

        □ products
        └ Get all products

        GET https://valentinos-coffee.herokuapp.com/products?category=pastry [200 OK, 1.31kB, 77ms]
        √  Status code test: 200

        └ Get single product

        ┌
        │ 
        └
        GET https://valentinos-coffee.herokuapp.com/products/1001 [200 OK, 954B, 75ms]
        √  Status code test: 200
        ┌
        │ 'A rich, dark, and full-bodied coffee with a bold flav
        │ or and intense aroma.'
        └
        √  Response body is JOSN
        √  JSON Schema are valid

        □ clients
        └ Register a new client

        POST https://valentinos-coffee.herokuapp.com/clients [200 OK, 809B, 78ms]
        √  Status code test: 200
        √  Response body is JOSN

        □ orders
        └ Create a new order

        POST https://valentinos-coffee.herokuapp.com/orders [201 Created, 937B, 76ms]
        √  Status code test: 201
        √  Response body is JOSN
        √  Customer name
        √  Schema is valid

        └ Get all orders

        GET https://valentinos-coffee.herokuapp.com/orders [200 OK, 847B, 74ms]
        √  Status code test: 200

        └ Get an order by ID

        GET https://valentinos-coffee.herokuapp.com/orders/AF_86H4A1R [200 OK, 932B, 74ms]
        √  Status code test: 200
        √  Response body is JSON
        √  Get Property ID on JSON
        √  Get Property products on JSON

        ┌─────────────────────────┬────────────────────┬───────────────────┐
        │                         │           executed │            failed │
        ├─────────────────────────┼────────────────────┼───────────────────┤
        │              iterations │                  1 │                 0 │
        ├─────────────────────────┼────────────────────┼───────────────────┤
        │                requests │                  7 │                 0 │
        ├─────────────────────────┼────────────────────┼───────────────────┤
        │            test-scripts │                  7 │                 0 │
        ├─────────────────────────┼────────────────────┼───────────────────┤
        │      prerequest-scripts │                  3 │                 0 │
        ├─────────────────────────┼────────────────────┼───────────────────┤
        │              assertions │                 17 │                 0 │
        ├─────────────────────────┴────────────────────┴───────────────────┤
        │ total run duration: 1431ms                                       │
        ├──────────────────────────────────────────────────────────────────┤
        │ total data received: 1.28kB (approx)                             │
        ├──────────────────────────────────────────────────────────────────┤
        │ average response time: 111ms [min: 74ms, max: 329ms, s.d.: 88ms] │
        └──────────────────────────────────────────────────────────────────┘

        Uploading Postman CLI run data to Postman Cloud...
        Uploaded successfully! View on Postman: https://go.postman.co/workspace/31bc1449-6088-4d03-81e4-0c06a421919d/run/36196810-05386d57-d98a-4408-b33b-cc40fc4cb220

        ```


## Reference and Attachment 
- **Youtube Tutorials**: [Postman API Test Automation for Beginners](https://www.youtube.com/watch?v=zp5Jh2FIpF0)
- **Course Notes**: [Postman Course Notes](https://github.com/vdespa/automation-with-postman-course)
- **Postman Collection Workspaces**: [Fahmi's API Test Automation](https://www.postman.com/fahmi-wiradika/freecodecamp-api-test-automation-with-postman/overview)
- **GitHub Action**: [Collection Runner Job Repository](https://github.com/fahmiwazu/Postman-API)