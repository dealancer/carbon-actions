# Carbon Actions

Carbon Actions is an experimental vibe coding GitHub actions that work in pair with [Carbon CLI](https://github.com/dealancer/carbon-cli). It uses OpenAI API to generate code and AWS S3 bucket to store data.

## Usage

### Issue creation
Create a new issue in your repository telling what you want to do and mention @BOT_NAME.

### PR updates
Review PR changes and ask @BOT_NAME to update the PR with the changes you want to make.

## Setup

### Bot setup

1. Create a bot user in your GitHub organization.
2. Create a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) for the bot user and save it for later use.

### S3 Bucket setup

1. Create a new S3 bucket in AWS.
2. Create a new IAM user with programmatic access.
3. Attach a custom policy to the IAM user with the following minimal permissions:
   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "s3:PutObject",
                   "s3:GetObject",
                   "s3:ListBucket"
               ],
               "Resource": [
                   "arn:aws:s3:::YOUR-BUCKET-NAME",
                   "arn:aws:s3:::YOUR-BUCKET-NAME/*"
               ]
           }
       ]
   }
   ```
4. Save the IAM user's access key ID and secret access key for later use.

### Repository setup

1. Add the following secrets to the repository:
   - `PAT_TOKEN`: The personal access token for the bot user.
   - `AWS_ACCESS_KEY`: The access key ID for the IAM user.
   - `AWS_SECRET_KEY`: The secret access key for the IAM user.
   - `OPENAI_API_KEY`: The API key for the OpenAI API.

2. Add the following variables to the repository:
   - `CARBON_BOT_NAME`: The username of the bot user.
   - `CARBON_BOT_EMAIL`: The email of the bot user.
   - `CARBON_MODEL`: The AI model to use for the Carbon CLI, e.g. `gpt-4o`.
   - `CARBON_INSTRUCTIONS`: Additional instructions to use for the Carbon CLI.
   - `AWS_BUCKET`: The name of the S3 bucket to use for the Carbon CLI.

3. Copy the `.github.example/workflows/*.yml` files to your repository.

4. Add the bot user to the repository as a collaborator.
