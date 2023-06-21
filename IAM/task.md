## What to do

### Sub-task 1 – Create 3 User Groups
Let’s imagine that we have created AWS Account that will use all members of our AWS program(Coordinator, Mentees, Mentors(Experts)). For all these users it will be better to create different groups with different permissions because, for example: Coordinator has more permissions that Mentee. Please create 3 user groups:
- CoordinatorsGroup
- MentorsGroup
- MenteesGroup

### Sub-task 2 – Create policies and roles
1. Create a policy named FullAccessPolicyEC2.
2. Configure the FullAccessPolicyEC2 to allow any actions on the EC2 resources.
3. Similarly, create policies for S3:
    - FullAccessPolicyS3 – everything’s allowed.
    - ReadAccessPolicyS3 – only get and list actions.
4. Create one role of EC2 Type (Trusted Entity) per each policy configured so far (note – these roles won’t be used right now, but might be reused in upcoming EC2 module):
    - FullAccessRoleEC2
    - FullAccessRoleS3
    - ReadAccessRoleS3
5. Create one group per each policy configured so far:
    - FullAccessGroupEC2
    - FullAccessGroupS3
    - ReadAccessGroupS3
6. Create 1 user from the 1st group, 1 user from the 2nd group, and 1 user from the 3rd group.
7. Configure named profiles for each user from the previous step to be used with AWS CLI in the subsequent modules. For more info please see https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html
