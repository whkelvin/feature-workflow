I am working on a feature development workflow that includes a few phases

1. Explore
Defining the feature and coming up with what needs to be done and why it needs to be done. We should end up with a document outlining what the feature is, what problem it's trying to solve and a list of user stories => as a user, I need to ...'. This should be save in ./feature/<feature-name>/exploration.md

Working rules:
1. Ask me strictly ONE question at a time. Never ask multiple questions in the same turn.
2. Each question must build directly on my previous answer, refining the specification.
3. Follow a structured path of exploration: Problem -> Target users -> Core use cases -> mockups with description for each flow
4. Document what needs to happen with frontend mock ups.

2. Design
In `./feature/<feature-name>/design/` we'd have 3 folders, frontend/, backend/, and api-spec/. Where each folder contains detail implementation plan for frontend, backend and api definitions in md format. Include as much implementation detail as possible including what files to create and what goes in each file.

frontend/
based on the mock ups in exploration.md here is how we should structure the document
- what new components do I need to add? What components exist that I can reused?
- what does the api call look like? Do I have to add any logic to support the newly created endpoint? Do I have to make changes to exisitng api code?
- what changes do I need from a state management's perspective? Do I need to create a new state? Is there a piece of state I can rely on?
- is the changes I am making now impacting other parts of the UI? Do I need to update the state after an api call?
- do I want to show notifications after an action is finished?
- tests - what e2e tests can we write to make sure the happy path is working?
break these down into folders
    /components
    /keyflow
        /feature + tests
        
        

backend/
- do I need to make any changes to the databases? What tables do I have to create? What tables do I have to modify? What does the migration look like?
- what endpoints do I need? 
- Who has access to call these endpoints? (authorization)
- Who can call this endpoint? (authentication)
- What does the request and response data look like for each endpoint?
- How are we validating the request models?
- What response code are we returning?
- is there anything we want to offload to background tasks?
- do we have debug query logging and exception handling in each endpoint?
- what tests do we need for each endpoint?
break these down into 2 subfolders
    /db-models
    /endpoints
        /nameOfEndpoint
            /implementation + testing strategy


api/
- I need newly created endpoints documented in md format
# NameOfEndpoint
# verb (GET, POST, DELETE, PATCH, PUT)
# url
# parameters
- path parameters
- query parameters
# request body in typescript interface format and in typescript code block
# response format for each error code and coresponding response body in as typescript interfaces in typescript code block 
# authentication - what is the authentication mechanism
# authorization - who is allowed to call this endpoint?
# examples - examples on how to call this endpoint with curl


Working rules:
1. Ask me strictly ONE question at a time. Never ask multiple questions in the same turn.
2. Each question should be a proposal for one part of the implementation.
3. Follow a structured path for design: endpoint definition -> frontend implementation -> db design and changes -> backend implementation

3. Execute
based on the implmentation docs, break down the work to see what work can be done in parallel and what work has to be done sequentially. Come up with an execution strategy outlinging the tasks and what llm models should be used to tackle each task.

4. Review
- run all tests and make sure all tests pass
- all linting checks passed
- code review
- come up with a checklist for the user to verify all features completed is working properly.

These are what the 4 different skills should do => /explore, /design, /execute, /review.
come up with the skills skeleton for these based on the description.






