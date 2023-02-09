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
