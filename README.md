# Jaylas-projects
# IT Documentation: Hosting a Static Website on AWS S3 with Route 53

## 📄 Overview
This document outlines the steps to host a static website using Amazon S3 and configure DNS settings with Amazon Route 53. The example domain used is `Yourprojects.click`.

---

## 1. Prerequisites
- An active AWS account.
- A registered domain name (`Yourprojects.click`,clikc is the cheapest domain for $3.00/yr)
- Basic knowledge of AWS services: S3 and Route 53.

---

## 2. Create and Configure the S3 Bucket

### Create a Bucket:
1. Navigate to the [Amazon S3 Console](https://console.aws.amazon.com/s3/).
2. Click **Create bucket**.
3. Enter the bucket name as `Yourprojects.click`.
4. Select the AWS Region( closeest to you.)
5. **Uncheck** "Block all public access" to allow public access.
6. Acknowledge the warning and proceed to create the bucket.

### Upload Website Files:
1. Open the newly created bucket.
2. Click **Upload**, then **Add files**.
3. Select your `index.html` file and upload it.

### Enable Static Website Hosting:
1. Go to the **Properties** tab of the bucket.
2. Scroll to **Static website hosting** and click **Edit**.
3. Select **Enable**, and set the **Index document** to `index.html`.
4. Save changes.

### Set Bucket Policy for Public Access:
1. Navigate to the **Permissions** tab.
2. Click **Bucket policy** and add the following policy [View the Bucket Policy JSON](./bucket-policy.json)


3. Save the policy.

---

## 3. Configure Route 53 DNS Settings

### Create a Hosted Zone:
1. Navigate to the [Route 53 Console](https://console.aws.amazon.com/route53/).
2. Click **Hosted zones**, then **Create hosted zone**.
3. Enter your domain name (`Yourprojects.click`) and select **Public hosted zone**.
4. Click **Create hosted zone**.

### Update Name Servers:
- In the hosted zone details, note the **NS (Name Server)** records.
- If your domain is registered outside AWS, update the domain's name servers to match these NS records.
- If registered with AWS, this step is handled automatically.

### Create DNS Records:

#### A Record for Root Domain:
1. Click **Create record**.
2. Set **Record name** to leave blank (represents the root domain).
3. Choose **Record type** as `A – IPv4 address`.
4. Select **Alias** as `Yes`.
5. For **Alias target**, enter your S3 website endpoint (e.g., `projectsbyjayla.click.s3-website-us-east-2.amazonaws.com`).
6. Click **Create records**.

#### A Record for www Subdomain:
1. Click **Create record**.
2. Set **Record name** to `www`.
3. Repeat the same steps as above, setting the alias target to the same S3 endpoint.

---

## 4. Test the Website
- Open a web browser and navigate to:
  - `http://Yourprojects.click`
  - `http://www.Yourprojects.click`
- You should see your static website's content.

---

## 5. Common Issues and Troubleshooting

### DNS_PROBE_FINISHED_NXDOMAIN:
- Ensure that the domain is correctly registered and that the name servers are properly set.

### NoSuchKey Error:
- Verify that the `index.html` file is correctly named and uploaded to the S3 bucket.

### Access Denied:
- Check the bucket policy to ensure public read access is granted.

---

> ✅ **Tip:** You can add additional files like `styles.css`, images, or custom error pages to the bucket for a more advanced website.
