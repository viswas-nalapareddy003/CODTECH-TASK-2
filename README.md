# CODTECH-TASK-2
Step 1: Create a Storage Bucket
A bucket, like its name suggests, is simply a place where all the objects (files) are stored. Here is how to create a bucket on Google Cloud.

Go to the Buckets page
Click on Create on the top bar
Give a unique name to your bucket
You can use <your name>-gfg-website, for example, ba3a-gfg-website
Click on Choose where to store data, and select the region nearest to you
For example, Asia (multiple regions in Asia)
Click on Choose how to control access to objects
Un-check the Enforce public access prevention on this bucket option
Click on Create at the end of the page
Step 2: Make The Objects Public
For everyone to be able to see your website, you have to make it public.

Open the newly created bucket by clicking on its name
Click on Permission
Click on Grant Access
Write allUsers in the New principals field
Click on Select a role under Assign Role
Select Storage Legacy Object Reader from Currently used
You can also search for it from the input box
Click on Save, and then ALLOW PUBLIC ACCESS
Step 3: Upload the Website
Make sure to name the main page of the website to index.html.

Go to the Objects tab
Click on Upload Files
Select all your website files and upload them
At this point, your website should be accessible from https://storage.googleapis.com/<your bucket name>/index.html.

However, if you notice, the website won't work if you try to remove the index.html from the address. But that is not the case in real life, right? You don't go to geeksforgeeks.org/index.html, you go to just geeksforgeeks.org. So, let's try and make our website even more professional. We will ask Google Cloud Storage to serve index.html by default when no path is specified in the URL.

Click on Buckets from the sidebar
Click on the three dots for your bucket
Click on Edit Website Configuration
Add index.html in both the input boxes
Click on Save
Step 4: Create a Load Balancer
Search for Load Balancing and click on it
Click on Create Load Balancer
Click on Start Configuration from Application Load Balancer
Leave the options as default and click Continue
Give the load balancer a name, like gfg-demo-lb
Frontend configuration
Give any name, like gfg-demo-frontend
Click on IP address
Click on Create IP address
Give any name, like gfg-demo-ip
Click Create
Click on Done
Backend configuration
Click on the dropdown that says Backend services and buckets
Click on Create a backend bucket
Give the bucket any name, like gfg-backend-bucket
Click on Browse and select the bucket that we had created earlier
Uncheck Enable cloud CDN
Click on Create
Leave the other settings as default
Click on the Create button at the bottom of the page
We have successfully created a load balancer that kind of serves your website from the bucket. We have also reserved and IP address for it. Wait for some time for all the settings to propagate and after that you will be able to browse your website using the newly reserved IP address.

The IP address will be listed under the Frontend section on the load balancer details page, you can simply click on the load balancer name (gfg-demo-lb, in our case), to open details.

create-load-balancer
At this point, if you want to browse the website from a domain name, like example.com, you can simply create an A Record from DNS configuration.

(Optional) Step 5: Enable HTTPS
It is mandatory to have a domain name to enable HTTPS. For the sake of this article, I am going to point cat.ba3a.tech to the website and enable HTTPS on it. You can follow along with your own domain name, like example.com.

Create an A record to the IP address
Go to the Load Balancer details page
Click on Edit
From Frontend configuration, click on Add Frontend IP and Port
Name it anything, like gfg-demo-frontend
Click on Protocol and select HTTPS
Click on IP address and select the existing one
Click on Certificate > Create new certificate
Name it anything, like gfg-demo-cert
Click on Google managed certificate
Add your domain name, like example.com
Finally, click on Create
Uncheck Enable HTTP to HTTPS redirect, if it is checked
Click on Update from the bottom of the page
We have now enabled HTTPS on our awesome cat website! It will likely take some time to provision the SSL certificate for our website, be patient with it. You can visit the cat website that I have created at cat.ba3a.tech. Visit the website and you will see her writing code in all her glory! BTW, what is she listening to?

Conclusion
Building a stunning website is just the first step; deciding where to host it is equally crucial. Object storage solutions like Google Cloud Storage and AWS S3 offer seamless ways to host static websites. This article delved into deploying an awesome cat website on Google Cloud Storage, showcasing how easily it can be accomplished in a few steps.

Object storage solutions simplify the process of hosting static websites and ensure their accessibility to visitors worldwide. While limitations exist regarding dynamic content due to the lack of server-side processing, these solutions excel in serving static content efficiently.

CODE:
Objective:

Host a simple HTML/CSS static website using Google Cloud Storage.

Steps to Solve:

Set Up a Google Cloud Project:

Log in to Google Cloud Console.

Create a new project.

Enable Required Services:

Enable the Cloud Storage API.

Create a Bucket:

Navigate to Cloud Storage and create a bucket.

Name the bucket and select a region.

Choose "Fine-grained" access control.

Upload Website Files:

Use the following Python script to upload files to the bucket:

from google.cloud import storage

def upload_to_bucket(bucket_name, source_file_name, destination_blob_name):
    """Uploads a file to the bucket."""
    storage_client = storage.Client()
    bucket = storage_client.bucket(bucket_name)
    blob = bucket.blob(destination_blob_name)

    blob.upload_from_filename(source_file_name)

    print(f"File {source_file_name} uploaded to {destination_blob_name}.")

# Example usage
bucket_name = "your-bucket-name"
source_file_name = "index.html"  # Path to your local file
destination_blob_name = "index.html"  # Desired file name in the bucket

upload_to_bucket(bucket_name, source_file_name, destination_blob_name)

Make the Bucket Public:

Edit bucket permissions to allow public access.

Configure Bucket for Website Hosting:

Set the default page (e.g., index.html).

Access the Website:

Use the bucket's public URL to access your website.
