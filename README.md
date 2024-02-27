# Download by Colab

## Introduction

Whether it's Google Drive, OneDrive, or various external buckets, we often encounter situations where we cannot directly use wget from the internet or the proxy is unstable, resulting in slow downloads. Considering that Colab directly connects to Google, downloading this type of data is very fast. Therefore, we can leverage Colab's bandwidth to download data. This repository provides a file download demonstration that can be modified and used for high-speed downloads based on this foundation.

This notebook provides a step-by-step guide to set up the AWS and Rclone environment for downloading and uploading videos using Python.

## Installation Steps

### 1. Install AWS and Boto3

```shell
!pip install --user awscli boto3
```

### 2. Install Kora and Rclone

```shell
!pip install kora
!curl https://rclone.org/install.sh | sudo bash
!sudo bash install.sh
!rclone --version
```

## Configuration

### 1. Configure AWS and Rclone

```python
content="""
[default]
aws_access_key_id = XXX
aws_secret_access_key = XXX
region = cn-shanghai
s3 =
    addressing_style = virtual
    endpoint_url = http://tos-s3-cn-shanghai.ivolces.com
"""

os.makedirs("/root/.aws", exist_ok=True)

with open("/root/.aws/config",'w') as f:
  f.write("[default]")

with open("/root/.aws/credentials","w") as f:
  f.write(content)

config_content = """
[tos]
type = s3
provider = Other
access_key_id = XXX
secret_access_key = XXX
region = cn-shanghai
endpoint = http://tos-s3-cn-shanghai.ivolces.com
force_path_style = false
disable_http2 = true
"""

with open('/root/.config/rclone/rclone.conf', 'w') as f:
    f.write(config_content)


```

### 2. Test Configuration

```shell
!aws --endpoint-url http://tos-s3-cn-shanghai.volces.com s3 ls
```

## Video Download and Upload

### Download and Upload Script

The notebook includes a script to download and upload videos from a specified list.

### Usage

1. Define the download list file path, username, password, and S3 bucket name.
2. Run the script to download and upload videos.

**The complete code can be found in main.ipynb**