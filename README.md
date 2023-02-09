# Lab 1: Introduction to Amazon Simple Storage Service (Amazon S3)
## Lab overview and objectives
This lab teaches you the basic feature functionality of Amazon Simple Storage Service (Amazon S3) using the AWS Management Console.

Amazon S3 is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means customers of all sizes and from all industries can use it to store and protect any amount of data for a range of use cases, such as websites, mobile applications, backup and restore, archive, enterprise applications, Internet of Things (IoT) devices, and big data analytics. Amazon S3 provides easy-to-use management features so you can organize your data and configure finely tuned access controls to meet your specific business, organizational, and compliance requirements. Amazon S3 is designed for 99.999999999 percent (11 9's) of durability and stores data for millions of applications for companies all around the world.

After completing this lab, you will know how to:

- Create a bucket in Amazon S3
- Add an object to a bucket
- Manage access permissions on an object and a bucket
- Create a bucket policy
- Use bucket versioning

## Duration
This lab requires approximately 60 minutes to complete. You will have a total time of 240 minutes to complete this lab.

## AWS service restrictions
In this lab environment, access to AWS services and service actions might be restricted to the ones that are needed to complete the lab instructions. You might encounter errors if you attempt to access other services or perform actions beyond the ones that are described in this lab.

## Accessing the AWS Management Console
At the top of these instructions, choose Start Lab to launch your lab.

A Start Lab panel opens, and it displays the lab status.

**Tip:** If you need more time to complete the lab, choose the Start Lab button again to restart the timer for the environment. Once you have consumed the total lab time that is allowed, you will no longer be able to extend the lab or start a new one. You can find the total time available for this lab in the Duration section of these instructions.

Wait until you see the message Lab status: ready, and then close the Start Lab panel by choosing the X.

At the top of these instructions, choose AWS

This opens the AWS Management Console in a new browser tab. The system automatically logs you in.

**Tip:** If a new browser tab does not open, a banner or icon is usually at the top of your browser with a message that your browser is preventing the website from opening pop-up windows. Choose the banner or icon, and then choose Allow pop ups.

Arrange the AWS Management Console tab so that it displays along side these instructions. Ideally, you will be able to see both browser tabs at the same time so that you can follow the lab steps more easily.

## Task 1: Creating a bucket

You are new to Amazon S3 and want to test the features and security of Amazon S3 as you configure the environment to hold the Amazon Elastic Compute Cloud (Amazon EC2) report data. You know that every object in Amazon S3 is stored in a bucket, so creating a new bucket to hold the reports is the first thing on your task list. 

In this task, you create a bucket to hold your Amazon EC2 report data and then examine the different bucket configuration options.

1. At the upper left of the AWS Management Console, on the Services menu, choose S3.
2. Choose Create bucket.

Bucket names must be 3–63 characters long and consist of only lowercase letters, numbers, or hyphens. The bucket name must be globally unique across all of Amazon S3 regardless of account or Region, and you cannot change a bucket name after creating the bucket. As you enter a bucket name, a help box displays showing any violations of the naming rules. Refer to the Amazon S3 bucket naming rules in the Additional resources section at the end of the lab for more information.

3. In the General configuration section, enter the following as the Bucket name: `reportbucket(NUMBER)`. Replace (NUMBER) with a random number so that your bucket has a unique name.

Example bucket name: `reportbucket987987`

4. Leave Region at its default value. 

By selecting a particular Region, you can optimize latency, minimize costs, or address regulatory requirements. Objects stored in a Region never leave that Region unless you explicitly transfer them to another Region.

5. Choose Create bucket.

## Task 2: Uploading an Object to the Bucket

Now that you have created a bucket for your report data, you are ready to work with objects. An object can be any kind of file: a text file, a photo, a video, a .zip file, and so on. When you add an object to Amazon S3, you have the option to include metadata with the object and set permissions to control access to the object.

1. Right-click the following link: new-report.png. Choose Save link as, and save the file to your desktop.
2. In the S3 Management Console, find and select the bucket name that starts with `reportbucket`.
3. Choose `Upload`
4. Choose `Add files`
5. Browse to and select the `new-report.png` file that you downloaded previously.
6. At the bottom of the page, choose `Upload`
7. Your file is successfully uploaded when the green bar indicating `Upload succeeded` appears.
8. In the `Upload: status` section in the upper right, choose `Close`

## Task 3: Making an Object Public

Security is a priority in Amazon S3, and before connecting an EC2 instance to the `reportbucket`, you want to test the bucket and object settings for security.

1. Confirm that the object is private by default
    - Go to the `reportbucket` overview page and click on the `Objects` tab.
    - Locate the `new-report.png` object and click on the file name to open the `new-report.png` overview page.
    - In the `Object overview` section, locate and copy the `Object URL` link.
    - Open a new browser tab, paste the object URL link into the address field and press Enter.
    - You should receive an `Access Denied` error because objects in Amazon S3 are private by default.

2. Make the object publicly accessible
    - Return to the web browser tab with the S3 Management Console. You should still be on the `new-report.png` Object overview tab.
    - In the upper right, choose the `Object actions` dropdown menu. You will notice that `Make public via ACL` is greyed out.
    - Go back to the main `reportbucket` overview page by choosing the reportbucket name in the navigation.
    - Choose the `Permissions` tab.
    - Under `Object Ownership`, choose `Edit`.
    - Enable `ACLs` and choose `Bucket owner preferred`.
    - Check the box next to "I acknowledge that ACLs will be restored".
    - Choose `Save Changes`.
    - Under `Block public access (bucket settings)`, choose `Edit` to change the settings.
    - Clear the check box for the `Block all public access` option and leave all other options cleared. 

Note: In a production environment, it is recommended to use the least permissive settings possible. Refer to the Amazon S3 block public access for more information.

- Choose Save changes
- A dialogue box opens asking you to confirm your changes. Enter "confirm" in the field, and then choose Confirm
- A message saying "Successfully edited Block Public Access settings for this bucket." should display at the top of the window.

- Choose the Objects tab.
- Choose the `new-report.png` file name.
- At the upper right on the `new-report.png` overview page, choose the Object actions dropdown menu, and select "Make public".
- Note the warning: "When public read access is enabled and not blocked by Block Public Access settings, anyone in the world can access the specified objects." This warning reminds you that making the object public means that everyone in the world can read it. 

- Choose "Make public" and you should see a green banner saying "Successfully edited public access" at the top of the window.
- In the upper right, choose "Close" to return to the `new-report.png` object overview.
- Return to the browser tab that displayed "Access Denied" for the `new-report.png` object and refresh the page.
- The `new-report.png` object should now display properly because it is publicly accessible.

- Close the web browser tab that displays the `new-report.png` image and return to the tab with the Amazon S3 Management Console.
- Note that in this example, you granted read access to only one specific object. If you want to grant access to the entire bucket, you need to use a bucket policy, which will be covered later in the lab.

- In the next task, you will work with your EC2 instance to confirm connectivity to the S3 bucket.

## Task 4: Testing Connectivity from the EC2 instance

In this task, you will connect to your EC2 instance to test connectivity and security to the Amazon S3 reportbucket.

### Prerequisites

- You should already be signed in to the AWS Management Console. If not, follow the steps in the "Start Lab" section to sign in to the AWS Management Console.

### Steps

1. On the Services menu, choose EC2.
2. On the EC2 Dashboard, under the Resources section, choose Instances (running).
3. Select the check box for Bastion Host and choose Connect.
4. In the Connect to instance window, select the Session Manager tab for the connection method.
   - With AWS Systems Manager Session Manager, you can connect to the bastion host instance without the need for specific ports to be open on your firewall or Amazon Virtual Private Cloud (Amazon VPC) security group. Refer to AWS Systems Manager Session Manager in the Additional resources section at the end of this lab for more information.
5. Choose Connect.
   - A new browser tab or window opens with a connection to the bastion host instance.
6. In the bastion host session, enter the following command to change to the home directory (/home/ssm-user/):
cd ~
- The output returns you to the command prompt.
7. Enter the following command to verify that you are in the home directory:
pwd
- The output should be as follows:
/home/ssm-user
8. Enter the following command to list all of your S3 buckets:
aws s3 ls
- The output should look similar to the following:
2020-11-11 22:34:46 reportbucket987987
- You see the reportbucket you created and lab auto-generated buckets.
9. Enter the following command to list all the objects in your reportbucket:
aws s3 ls s3://reportbucket(NUMBER)
- The command looks similar to the following: 
aws s3 ls s3://reportbucket987987
- The output should look like the following:
2020-11-11 15:46:34 86065 new-report.png
10. Enter the following command to change directories into the reports directory:
cd reports
- The output returns you to the command prompt.
11. Enter the following command to list the contents of the directory:
ls
- The output shows some files created in your reports directory to test the application:
dolphins.jpg files.zip report-test.txt report-test1.txt report-test2.txt report-test3.txt whale.jpg
12. Enter the following command to see if you can copy a file to the S3 bucket:
aws s3 cp report-test1.txt s3://reportbucket(NUMBER)
- The command looks similar to this:
aws s3 cp report-test1.txt s3://reportbucket987987

- The output indicates an upload failed error. This error occurs because you have read-only rights to the bucket and do not have the permissions to perform the PutObject action.

- Leave this window open. and go back to browser tab with the AWS console.
- In the next task, you create a bucket policy to add the PutObject permission.
