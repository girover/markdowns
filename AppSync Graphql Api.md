
## Implementation Plan for AppSync GraphQL API

### Step 1: Create a GitHub Repository

I will create a new GitHub repository named `intern-mfa-appsync-graphql`. The repository will follow a well-structured folder organization to ensure maintainability and scalability. It will include:

- **`/src`**: This folder will contain the core TypeScript code, including:
  - Resolvers (queries, mutations, subscriptions)
  - The GraphQL schema definition (`schema.graphql`)
  - Types used across the project
- **`/cdk`**: This folder will host the AWS CDK project responsible for defining and managing the infrastructure as code. The CDK stack will include:
  - The AppSync API and schema configuration
  - DynamoDB table references
  - IAM roles and policies
  - Resolvers

### CI/CD Workflow with GitHub Actions

I will set up a GitHub Actions workflow for automated CI/CD, ensuring smooth deployments and type safety. The key steps include:

#### GraphQL Type Generation:
On every code commit, if there are changes to the GraphQL schema, the corresponding TypeScript types will be automatically generated using the `graphql-codegen` package. This ensures type safety and reduces potential errors.

#### Building the Code:
After type generation, the TypeScript files`(resolvers and types)` will be transpiled to JavaScript using the TypeScript compiler. This step ensures the code is ready for deployment.

#### Automated Deployment to AWS:
Once the code is built, the API and all resources defined in the CDK stack will be deployed to AWS using the `cdk-cli`.


### Step 2: Write the GraphQL Schema

I will define the initial GraphQL schema in a file named `schema.graphql`. The schema will be designed to align with the existing database structure, ensuring that the types, queries, mutations, and subscriptions match the data retrieved from these endpoints:

- `GET /mes/batches`
- `GET /mes/workcenters/{workCenterId}/batches/{batchId}/itemoperations`
- `PATCH /mes/itemoperations/{itemOperationId}/complete`
- `PATCH /mes/itemoperations/{itemOperationId}/reorder`

#### The schema will include:

- **Queries:**
  - Fetch batch data: `batches`
  - Fetch item operations: `itemOperations`
  
- **Mutations:**
  - Update operation status: `completeItemOperation`
  - Reorder an item operation: `reorderItemOperation`
  
- **Subscriptions:**
  - Listen for status updates: `onOperationStatusUpdate`



### Step 3: Implement Resolvers in TypeScript
I will write TypeScript resolvers in the `/src/resolvers` folder:
- **Queries:** `getBatchesResolver.ts`, `getItemOperationsResolver.ts`
- **Mutations:** `completeItemOperationResolver.ts`, `reorderItemOperationResolver.ts`
- **Subscription:** `onOperationStatusUpdateResolver.ts`

The resolvers will connect to the existing DynamoDB tables using the AWS SDK.

### Step 4: Implement Queries, Mutations and Subscriptions
I will implement the resolvers for the `batches`, `itemOperations`, `completeItemOperation` and `reorderItemOperation`.

These resolvers will interact with existing DynamoDB tables based on the provided API specifications.

### Step 5: Set Up Authentication and Authorization
I will integrate a custom lambda authorizer to handle authentication.
