## What to do

### Sub-task 1 – create a static web site
1. Create a static web site. Feel free to do anything you like, but keep in mind that the main goal is to have a lightweight folder with multiple files in it:
   - a couple if interlinked HTMLs or an HTML page with some CSS styles is enough
   - the site should not require any additional runtime environment like JVM or Node
   - no backend is required
   - you’ll have several other tasks dedicated to creation of a fully functioning web-application in the modules 3-8
   - no heavy media resources (like large images/animations/videos) are recommended – you’ll have to upload the site to AWS multiple times
2. Create an S3 bucket which name doesn’t include uppercase characters, includes your full name, and begins with a letter. Recommendation – choose a name generic enough so that the bucket may be reused for developing a web application later.
3. Copy the static website from step 1 to the bucket from step 2 using AWS CLI and named profile with appropriate permissions from the previous module.
4. Enable static website hosting on your S3 bucket and make sure that the content of your site is available via website endpoint of the bucket.
5. Enable cross-region replication for the bucket from step 2. (! Note: please create a new role when enabling replication, it may not work properly with existing one)

### Sub-task 2 – Play with versioning
1. Create another S3 bucket which name doesn’t include uppercase characters, includes your full name + “task2”, and begins with a letter.
2. Enable versioning for the bucket from step 1.
3. Upload 2-3 files to the bucket. Make some changes to these files so that the bucket contains 2 (or more) versions of at least one file.
4. Using AWS CLI, get the latest version of a specific file.
5. _Optional: write a script to get the latest version of a specific file no newer than a given date. You are free to use Bash or BAT or use the AWS SDK for any programming language._

### Sub-task 3 – Practice more AWS CLI hacking and play with permissions
1. Using AWS CLI list all the objects in the S3 bucket from the first sub-task of this module. In the response, you'll see a lot of additional data for each object, play with the "--query" parameter to filter out only S3 object keys from the response.
2. Using different users from module 2, try to execute the following commands via AWS CLI:
   - upload new file to the S3 bucket
   - list all the objects in the S3 bucket
3. Observe the results.
4. _Optional: play with the "--output" parameter and list all the objects in the S3 bucket with their size in a "human-readable" format as a table, for example:_

| key                     | size    |
|---|---|
| index.html              | 17094   |
| assets/style.css        | 765     |
| pictures/background.png | 1017005 |

## Sub-task 4 – Think a little bit
1. Describe all the use cases for S3 you’ve seen on past/current projects.
2. Describe any other S3 use cases you see reasonable.
3. _Optionally, visualize some of the use cases using any preferred notation (UML, BPMN, AWS diagrams, etc)._
