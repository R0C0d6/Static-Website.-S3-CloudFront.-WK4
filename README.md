ARCHITECTURE
![Architecture Diagram](https://i.postimg.cc/cLGJqGy9/Whats-App-Image-2025-12-17-at-15-57-45.jpg)

### Static Website

A static website is a simple type of website that delivers the same content to every visitor. Unlike dynamic websites, it does not change based on user input or interact with a backend server. Static websites are built using basic technologies such as HTML, CSS, images, and JavaScript files. They cannot handle tasks like processing form submissions or fetching data from a database.

### S3

Amazon Simple Storage Service (S3) is an object storage solution designed to store and manage large amounts of data with virtually no storage limits. One of its key features is the ability to configure an S3 bucket to host and publicly serve a static website over the internet.

### CloudFront

Amazon CloudFront is a global Content Delivery Network (CDN) that speeds up content delivery by caching files at edge locations around the world. This ensures that users can access website content quickly with minimal latency, no matter where they are located.

### Prerequisites

An AWS account
Website Files for your static website



**Step 1 – Create an Amazon S3 Bucket**

a) Sign in to your AWS Management Console. From the **Services** menu, select **All Services**, search for **S3**, and click on it to open the S3 dashboard.
b) From the S3 dashboard, click **Create bucket** to set up a new storage bucket that will hold your static website files.
c) Provide a name for your bucket. Bucket names must be globally unique, so if you see an error saying **“Bucket with the same name already exists”**, simply choose a different name and try again.

![S3 Bucket Creation](https://i.postimg.cc/W1mgC7Ks/Screenshot-2025-11-10-134912.png)

d) Because the website needs to be accessible to everyone, uncheck Block all public access. Then, confirm the change by selecting the I acknowledge… checkbox beneath it.

![S3 Bucket Creation](https://i.postimg.cc/rsS5TCsL/Screenshot-2025-11-10-134954.png)

e) Keep all other settings as they are, scroll to the bottom of the page, and click Create bucket to finish creating the bucket.

![S3 Bucket Creation](https://i.postimg.cc/qBXtk7wS/Screenshot-2025-11-10-135146.png)

f) **Prepare Your HTML File**
Before uploading files to your S3 bucket, you need to prepare your HTML script for the static website. 
Create a simple `index.html` file, as this will serve as the main entry point of your website. 
Use basic HTML to define the structure of your page and include any required CSS, images, or JavaScript files. Make sure all file names and paths are correct, since S3 is case-sensitive and incorrect naming can prevent your website from loading properly. Once your HTML file is ready, save it in a folder along with any supporting assets so it can be uploaded to the bucket in the next step.
Eg:
![HTML File Creation](https://i.postimg.cc/fbKFzm3n/Screenshot-2025-11-10-140146.png)




Step 2 – Upload Website Files to the S3 Bucket
a) After the bucket is created, click on its name to open the bucket details page.
b) A newly created bucket is empty by default. Click the Upload button to begin adding your website files.\
c) On the upload screen, select Add files to upload individual files from your computer, or choose Add folder to upload multiple files at once from a directory.
d) Keep all other settings unchanged, scroll down, and click Upload to start transferring the selected files to the bucket.
e) The upload duration will depend on your internet speed and the number of files being uploaded, so wait until the process completes.
f) Once the upload finishes, review the status to confirm that all files were uploaded successfully and check for any errors. When done, click Close to return to the bucket details page.
![HTML File Upload to S3](https://i.postimg.cc/28LS18Ft/Screenshot-2025-11-10-141251.png)




**Step 3 – Enable Static Website Hosting on the S3 Bucket**
a) From the bucket overview page, open the **Properties** tab and scroll down the page.
b) Locate the **Static website hosting** section and click **Edit**.
c) Choose **Enable** for static website hosting. Additional options will appear:
  * **Hosting type:** Select **Host a static website**.
  * **Index document:** Enter the name of the file that will act as the homepage of your website. This field is case-sensitive and is typically set to **`index.html`**.
  * **Error document:** Specify the file to be displayed when an error occurs, such as **`error.html`** or **`404.html`**.
d) Scroll to the bottom and click **Save changes** to apply the settings.
![Enable Static Website Hosting](https://i.postimg.cc/DyRdG0Vb/Screenshot-2025-11-10-140415.png)




**Step 4 – Add a Bucket Policy**
Before your website can be viewed by the public, you must explicitly allow public access to the objects stored in the S3 bucket.
a) On the bucket overview page, open the **Permissions** tab, scroll down, and find the **Bucket policy** section.
b) In the **Bucket policy** section, click **Edit**.
c) To allow public read access to your website files, copy the policy below and paste it into the bucket policy editor.
Make sure you replace **`homeworkout-aws`** with **your own bucket name** in the **Resource** field.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::homeworkout-aws/*"
    }
  ]
}
```

⚠️ **Important:** You must change `homeworkout-aws` to match your actual bucket name, otherwise the policy will not work.
d) Once done, click **Save changes** to apply the bucket policy.
![Enable Static Website Hosting](https://i.postimg.cc/43ytyHwV/Screenshot-2025-11-10-142911.png)


e) You should now be able to view your website using the Amazon S3 website endpoint.
 Go back to the **Bucket overview** page.
 Click on the **Properties** tab.
 Scroll to the bottom to find the **Static website hosting** section.
 Locate the **Bucket website endpoint** URL and click on it to open your website in a browser.
![Enable Static Website Hosting](https://i.postimg.cc/wjZx5tgs/Screenshot-2025-11-10-140210.png)






