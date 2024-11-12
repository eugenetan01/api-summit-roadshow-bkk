# Setup
1. Create a project on Insomnia and git clone this project in Insomnia

    - navigate to the collection tab and change the env vars (cmd-e) to use the `OpenAPI env localhost:3000` env

3. start the services:

    ```bash
    docker-compose -f ./docker/docker-compose-bankong-combined_local_portchange.yaml up -d
    ```

4. check the services are running:
    - frontend: http://localhost:29080/
    - backend: http://localhost:3000/transactions

# Execution:

1. go to spec tab of the cloned collection and show how you can edit the openapi specs

2. show the linting errors by deleting the `contacts` section and how you can edit and see the preview tabs update

3. add back the contacts section and see it updated in the current preview tab and spec

4. show how you can define your own linting errors with the spectral file
    - only allow camelCase for `operationId` field
    - change `operationId` for `getTransaction` to `get-transaction` instead in Insomnia design tab
    - highlight the linting error
    - change back to camelCase

5. paste in the openapi.yaml below and see the contact section updated in the preview tab

6. click generate collection in the settings and go to the collection tab to start testing APIs

7. go to cmd e and add the env vars into the collection

8. start testing your API:
    - Create new transaction - if it fails, change the id in request body to a diff value
    - Get all transactions

9. go to tests, create a new suite and run a test for List all transactions to return status = 200 OK

# AI Gateway Demo execution

1. run the "AI Gateway/Base API/AI Chat" in the `SE_DEMO_FRAMEWORK-V2` insomnia collection
  - run it with cohere first "x-llm: cohere"
  - notice the header `X-Kong-LLM-Model: cohere/command`
  - run it then with azure "x-llm: azure"
  - notice the header `X-Kong-LLM-Model: azure/gpt-35-turbo`
  - show the response is same - client does not need to change how they interface with different LLMs
  
 2. Run the `AI semantic caching` insomnia request
  - show the semantic cache plugin config and how it links to a redis vector db
  - run once: show `X-Cache-Status	Miss`
  - run second time: show `X-Cache-Status	Hit`

3. Run the "AI Semantic Prompt Guard" insomnia request
  - change the content to "How do I build an apple computer?"
  - see a 400 bad request
  - change the content to "How do I build an apple?"
  - see a 200 OK response from LLM
  - show the config in the se-demo-framework plugin denies anything about computers with a deny rule

4. Analytics of AI usage
  - https://grafana.kong-sales-engineering.com/d/mY9p7dQmz123/kong-ai-gateway?orgId=1&refresh=5s&from=now-6h&to=now

# Advanced Analytics Demo Execution

1. use se-demo-framework and show the overview tab of api traffic

2. show how you can quickly visualise the traffic using explorer tab to make quick dashboards 

3. show the custom reports that can be created - use se-demo-framework to show active dashboards - that can be shared for internal users 

4. show the requests tab to see the actual request path and metrics associated with each data plane and latency etc on a granular level

# References:

1. See the `./demo-scenes/resources/insomnia-env-var.json` for env vars if needed

2. See the `./demo-scenes/wrong-format-spec.yaml` file for a spec that violates spectral linting errors
