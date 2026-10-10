# Week 6: Lambda Proof of Concept

## HarborTech Ticket Summary

Bright Path Community Services runs a short departmental report for approximately 20 seconds once per day. The current EC2-based approach leaves a server idle for most of the day.

HarborTech requested a low-risk proof of concept to evaluate whether a serverless compute model would be more appropriate. The authorized work included environment discovery, selecting a compute model, preparing and attempting to deploy one small AWS Lambda function, testing the supplied application logic if deployment succeeded, documenting failures, and cleaning up resources created during the lab.

I was not authorized to migrate the production workload or create or modify IAM users or roles.

## Workload and Compute Recommendation

I recommend AWS Lambda for the Bright Path daily report.

The first reason is that the workload runs for only approximately 20 seconds once per day and does not require a continuously running server. Lambda is designed for short, event-driven execution and avoids leaving compute capacity idle for the remainder of the day.

The second reason is operational simplicity. Lambda removes the need to maintain a continuously running EC2 operating system for this type of workload. The report can run only when invoked while AWS manages the underlying compute environment.

I would reconsider this recommendation if the workload became continuously running, required persistent local state, required specialized operating-system access, exceeded Lambda execution constraints, or depended on software that was more appropriate for a container or server environment.

For a continuously running containerized process, ECS/Fargate could be more appropriate. EC2 could be justified if full operating-system control or persistent server processes were required.

## Learner Lab Guardrails

The lab required:

- Region: `us-east-1`
- AWS CloudShell
- Existing IAM role: `LabRole`
- No creation of IAM users or roles
- No EC2 deployment
- No ECS or EKS deployment
- No API Gateway deployment
- No production migration
- No credentials, account IDs, access keys, or session tokens in the public submission

Because the lab specifically prohibited creating or modifying IAM roles, I did not attempt to create a replacement role when the Lambda deployment failed.

## Discovery Evidence

Before executing the discovery commands, I predicted that the operations would make no changes to AWS resources because they were read-only inspection commands.

Commands executed:

```bash
aws sts get-caller-identity \
  --region us-east-1 \
  --output json
```

Submitted identity evidence was redacted:

```json
{
    "UserId": "[REDACTED_ID]",
    "Account": "[REDACTED_ACCOUNT]",
    "Arn": "arn:aws:iam::[REDACTED_ACCOUNT]:root"
}
```

Lambda discovery:

```bash
aws lambda list-functions \
  --region us-east-1 \
  --query '{Functions:Functions[].{FunctionName:FunctionName,Runtime:Runtime}}' \
  --output json
```

Result:

```json
{
    "Functions": []
}
```

ECS discovery:

```bash
aws ecs list-clusters \
  --region us-east-1 \
  --output json
```

Result:

```json
{
    "clusterArns": []
}
```

The empty Lambda list means the discovery request succeeded but no Lambda functions were present or visible in `us-east-1` at that time.

The empty ECS cluster list means the ECS discovery request also succeeded but no ECS clusters were present or visible in the Region.

An empty list is valid AWS evidence and does not indicate that the command failed.

## AI Audit A: Permission Awareness

A suggestion to create a new IAM administrator role would be rejected.

The Learner Lab explicitly required the use of the existing `LabRole` and prohibited creating IAM users or roles. The supported approach was therefore to attempt the Lambda proof of concept with `LabRole` and stop if the AWS environment rejected the operation.

## AI Audit B: Command Verification

AI suggested using the following read-only discovery operations:

```bash
aws sts get-caller-identity
aws lambda list-functions
aws ecs list-clusters
```

I executed the commands myself in my Learner Lab.

AWS confirmed that the commands were valid by returning my authenticated identity and successful empty results for both Lambda functions and ECS clusters.

The actual AWS responses were treated as the source of truth rather than the AI prediction.

## Lambda Starter Code

The supplied starter code was used without changing the application logic:

```python
import json

def lambda_handler(event, context):
    department = event.get("department")
    if not isinstance(department, str) or not department.strip():
        return {"statusCode": 400, "body": json.dumps({"error": "department is required"})}
    return {"statusCode": 200, "body": json.dumps({"report": "ready", "department": department.strip()})}
```

The function was intended to accept a nonempty `department` field.

A valid department should return an application-level `statusCode` of `200`.

A missing or empty department should return an application-level `statusCode` of `400`.

## Build Evidence

Function name selected:

```text
ht-w6-adnan06-event
```

Region:

```text
us-east-1
```

Runtime:

```text
python3.12
```

Handler:

```text
lambda_function.lambda_handler
```

Memory:

```text
128 MB
```

Timeout:

```text
10 seconds
```

Role:

```text
LabRole
```

The deployment package was created with:

```bash
python3 -m zipfile -c function.zip lambda_function.py
```

Result:

```text
Command exit code: 0
```

This confirmed that the local ZIP package was created successfully.

## Deployment Attempt

I attempted to create the Lambda function using the required existing `LabRole`.

```bash
aws lambda create-function \
  --function-name ht-w6-adnan06-event \
  --runtime python3.12 \
  --role arn:aws:iam::[REDACTED_ACCOUNT]:role/LabRole \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://function.zip \
  --timeout 10 \
  --memory-size 128 \
  --region us-east-1
```

AWS returned:

```text
InvalidParameterValueException:
The role defined for the function cannot be assumed by Lambda.

Command exit code: 254
```

The scripted workflow then stopped and did not continue with additional AWS write operations.

## Deployment Analysis

The Lambda function was not successfully created.

The local build stage succeeded, but the AWS `CreateFunction` request failed because AWS reported that the specified `LabRole` could not be assumed by Lambda.

I did not create a replacement role or modify IAM permissions because those actions were outside the Learner Lab guardrails.

The AWS error indicates a role-assumption problem involving the required `LabRole`. However, I did not treat a specific IAM trust-policy configuration as verified root cause because I did not independently modify or fully validate the role configuration.

The verified fact is that AWS rejected `CreateFunction` because the role supplied to Lambda could not be assumed.

## Baseline Prediction

The intended valid event was:

```json
{"department":"operations"}
```

Based on the supplied starter code, my prediction was:

```json
{
  "statusCode": 200,
  "body": "{\"report\": \"ready\", \"department\": \"operations\"}"
}
```

The intended invocation command was:

```bash
printf '%s' '{"department":"operations"}' > valid.json

aws lambda invoke \
  --function-name "$FUNCTION_NAME" \
  --cli-binary-format raw-in-base64-out \
  --payload fileb://valid.json \
  response-valid.json \
  --region us-east-1

cat response-valid.json
```

The prediction could not be verified in AWS because the function had not been successfully deployed.

Therefore, the expected `200` result remained a prediction based on the supplied application code rather than observed AWS evidence.

## Incident Prediction

The required incident event was:

```json
{}
```

Based on the starter code, my hypothesis was that the request would fail application validation because the required `department` field was missing.

The expected application response was:

```json
{
  "statusCode": 400,
  "body": "{\"error\": \"department is required\"}"
}
```

The intended reproduction command was:

```bash
printf '%s' '{}' > invalid.json

aws lambda invoke \
  --function-name "$FUNCTION_NAME" \
  --cli-binary-format raw-in-base64-out \
  --payload fileb://invalid.json \
  response-invalid.json \
  --region us-east-1

cat response-invalid.json
```

I could not obtain actual invocation metadata or a `response-invalid.json` result because the Lambda function did not exist.

Therefore, the application-level validation failure is supported by the supplied Python logic but was not independently verified through an AWS invocation.

## Root-Cause Reasoning

There were two different issues that must not be confused.

The first was the actual AWS deployment failure. AWS rejected `CreateFunction` because `LabRole` could not be assumed by Lambda. This prevented the proof-of-concept function from being deployed.

The second was the deliberately invalid `{}` event described by the assignment. According to the supplied application logic, that event would fail because the `department` field is required.

Because the function was never deployed, I could not reproduce the second condition in AWS.

I therefore did not claim that the application validation response was observed.

## AI Audit C: Diagnose, Do Not Guess

The statement that a Lambda CLI `StatusCode` of `200` automatically means that the report succeeded is not sufficient.

Lambda invocation metadata and the application response returned by the function represent different layers.

The supplied Python function can return an application-level `statusCode` of `400` when the required `department` field is missing.

Therefore, the response payload must be inspected before determining whether the application completed successfully.

In my environment, I could not perform this comparison because deployment failed before any invocation occurred.

I rejected any suggestion to invent successful invocation output.

## Recovery Prediction

The corrected event was intended to be:

```json
{"department":"student-services"}
```

Based on the supplied starter code, this should satisfy the required `department` validation.

The expected application result was:

```json
{
  "statusCode": 200,
  "body": "{\"report\": \"ready\", \"department\": \"student-services\"}"
}
```

The intended recovery invocation was:

```bash
printf '%s' '{"department":"student-services"}' > corrected.json

aws lambda invoke \
  --function-name "$FUNCTION_NAME" \
  --cli-binary-format raw-in-base64-out \
  --payload fileb://corrected.json \
  response-corrected.json \
  --region us-east-1

cat response-corrected.json
```

The recovery behavior could not be tested because the function had not been deployed.

The correction is therefore an application-code prediction and not an observed AWS result.

## Cleanup Evidence

No successfully deployed Lambda function existed as a result of this work.

The `CreateFunction` request failed before AWS created `ht-w6-adnan06-event`.

Therefore, there was no successfully created Lambda function from this attempt that required deletion.

I did not delete, modify, or attempt to clean up resources belonging to another user.

## AI Audit D: Architecture Judgment

I reject the recommendation that Lambda should automatically be used for a process that runs continuously without stopping.

Lambda is well suited to short, event-driven work such as Bright Path's approximately 20-second daily report.

An always-running workload has different operational requirements.

ECS/Fargate could be more appropriate for a continuously running containerized process because it supports persistent container workloads without requiring the customer to manage the underlying EC2 operating system.

EC2 could be more appropriate when full server control, persistent processes, specialized software, or operating-system-level access are required.

For the current Bright Path workload, Lambda remains my preferred architecture because the workload is short and infrequent. However, the proof of concept must be successfully deployed and tested before recommending a production migration.

## HarborTech Handoff

### Recommendation

Continue evaluating AWS Lambda as the preferred compute model for Bright Path's short daily departmental report.

Its event-driven execution model better matches a workload that runs for approximately 20 seconds once per day than an EC2 instance that remains idle for most of the day.

### Verified Evidence

I verified that:

- CloudShell was authenticated to the Learner Lab.
- The Region used was `us-east-1`.
- No Lambda functions were present during initial discovery.
- No ECS clusters were present during initial discovery.
- The supplied Python starter code was packaged successfully.
- The Lambda deployment attempt used the required `LabRole`.
- AWS rejected `CreateFunction` with `InvalidParameterValueException`.
- AWS specifically reported that the role defined for the function could not be assumed by Lambda.
- No successful Lambda deployment or invocation occurred.

### Remaining Risks and Unknowns

The following behaviors were not verified through an actual Lambda invocation:

- successful `operations` baseline
- application-level `400` response for the empty event
- successful `student-services` recovery
- deployed Lambda runtime configuration
- production workload compatibility

These results must not be treated as verified until the authorized role issue is resolved and the proof of concept is executed successfully.

### Approval Required

An authorized instructor or AWS Learner Lab administrator should review the pre-existing `LabRole` or the lab environment.

I am not authorized to create or modify IAM roles to bypass the error.

No production migration should occur based only on the architecture recommendation. A working proof of concept and successful verification should be completed first.

## AI-Use Disclosure

I used AI to help interpret the assignment, complete AWS CLI command templates, distinguish read-only operations from write operations, explain the difference between Lambda invocation metadata and application-level responses, and organize the evidence for the HarborTech handoff.

I independently executed the AWS commands in my own Learner Lab.

Actual AWS output was treated as the source of truth.

I did not use predicted AI output as evidence of a successful Lambda deployment or invocation.

When AWS returned the `LabRole` assumption error, I documented the actual failure instead of inventing successful results or making an unauthorized IAM change.

## Lessons Learned

This exercise demonstrated that architecture selection and deployment verification are separate tasks.

Lambda appears appropriate for the workload based on its short duration and low execution frequency, but a reasonable architecture recommendation does not prove that a specific AWS deployment is currently operational.

AWS errors must be treated as evidence rather than bypassed.

The local Lambda package built successfully, but AWS rejected the deployment because the required role could not be assumed.

The Learner Lab guardrails were also part of the technical decision-making process. Creating or modifying IAM resources to bypass the failure would have violated the assignment restrictions.

Another important lesson is the distinction between Lambda service-level invocation metadata and an application's own response. A successful Lambda invocation does not automatically mean that the application accepted the input.

Finally, predictions from AI or source code should remain clearly labeled as predictions until verified with actual AWS evidence.

## Professional Vocabulary

### AWS Lambda

AWS Lambda is a serverless compute service that runs code in response to events without requiring the customer to manage a continuously running server.

### Amazon EC2

Amazon Elastic Compute Cloud provides virtual server instances and greater operating-system-level control than Lambda.

### Amazon ECS

Amazon Elastic Container Service is an AWS service for running and managing containerized applications.

### AWS Fargate

AWS Fargate provides serverless compute capacity for containers used with services such as ECS.

### Function

A Lambda function contains executable application code and its runtime configuration.

### Runtime

The runtime provides the language execution environment for a Lambda function. The planned proof of concept used Python 3.12.

### Handler

The handler is the function entry point Lambda calls when an event is received.

The planned handler was:

```text
lambda_function.lambda_handler
```

### Event

An event is the input supplied to a Lambda invocation.

### Payload

The payload contains the event data supplied to the Lambda function.

### IAM Role

An IAM role provides permissions that an AWS service or workload can assume when properly configured.

### LabRole

`LabRole` was the pre-existing role required by the Learner Lab assignment.

### Application Validation

Application validation checks whether supplied input meets the requirements defined by the application.

In the starter code, `department` must be a nonempty string.

### Application-Level Status

The `statusCode` returned inside the Python response represents the application's result and should not automatically be confused with Lambda service invocation metadata.

### Proof of Concept

A proof of concept is a limited implementation used to test feasibility before a production decision.

### Root Cause

A root cause is the underlying reason a failure occurred.

### Guardrail

A guardrail is a restriction intended to keep an operation within authorized and supported boundaries.

### Handoff

A handoff communicates findings, evidence, risks, recommendations, and remaining work to the next responsible person or team.
