# Transfer files from Google Drive to AWS S3

This document describes the process for transferring files from a Google Drive account to AWS S3.  

This is NOT a tutorial about using Google Colab. You are expected to know how to enter and execute commands in a Jupyter-style notebook.  

## Prerequisites
  
- Google account w/ access to Google Colaboratory
	- Note: You may need to request access to Colab.
- Amazon Web Services (AWS) account w/ permission to **write** to S3
	- You will also need an AWS Access Key ID and Secret Access Key (get this from the IAM section of AWS).
- AWS S3 bucket (this will be your destination)
  
## Preparation
  
1. Visit [Google Colaboratory](https://colab.research.google.com/)
2. Create a new notebook (it should open a fresh notebook)
3. Install the AWS CLI package:  
	``` !pip install awscli ```  
4. Gather your AWS **access key** and **secret acess key**, then execute:  
	``` !aws configure ```  
5. Import the drive library from Google Colab  
	``` from google.colab import drive ```  
6. You will need to grant access to your Google Drive when you run the following command (see the _Additional notes_ section below for more information):  
	``` drive.mount("/content/drive") ```  
7. Test your drive mount by listing files  
	``` ls "/content/drive/My Drive" ```  

## Copying files

The following command will start a file copy. Use of --recursive is optional. You can also specify specific source or destination directories.  
	``` !aws s3 cp "/content/drive/My Drive/" s3://<bucket-name>/ --recursive ```  

## Additional notes
  
- When you run the command ``` drive.mount("/content/drive") ```, it will generate a popup window asking you for permission to access your Google Drive files. You can select the first option 'google drive' and leave the rest unchecked.  
- This process will not convert Google proprietary documents (.gdoc, .gform, etc.) to Microsoft Office formats. To do that, you will need something like [Google Takeout](https://takeout.google.com).  
- You can create a new AWS IAM account or use an existing account, but that account will need permission to write to your S3 bucket.  
