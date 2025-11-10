# AWS S3 Static Website Hosting with Terraform

This project demonstrates how to deploy a static website on AWS S3 using Terraform. It creates an S3 bucket configured for static website hosting with public access and uploads HTML files.

## 🏗️ Architecture

- **AWS S3 Bucket**: Configured for static website hosting
- **Public Access**: Enabled with public-read ACL
- **Website Files**: `index.html` and `error.html` uploaded automatically
- **Region**: US East 1 (us-east-1)

## 📋 Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) (v1.0+)
- [AWS CLI](https://aws.amazon.com/cli/) configured with appropriate credentials
- AWS Account with permissions to create S3 buckets

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone <repository-url>
cd s3_staticfile_hosting
```

### 2. Configure Variables

The default bucket name is set in `variables.tf`:
```hcl
bucketname = "myterraformprojectwebsiteproject2025"
```

To customize the bucket name, you can:
- Modify the default value in `variables.tf`
- Or pass it at runtime: `terraform apply -var="bucketname=your-bucket-name"`

### 3. Initialize Terraform

```bash
terraform init
```

### 4. Review the Plan

```bash
terraform plan
```

### 5. Deploy the Infrastructure

```bash
terraform apply
```

Type `yes` when prompted to confirm the deployment.

### 6. Access Your Website

After deployment, Terraform will output the website endpoint:

```bash
terraform output websiteendpoint
```

Open the URL in your browser to view your static website.

## 📁 Project Structure

```
.
├── main.tf              # Main infrastructure configuration
├── provider.tf          # AWS provider configuration
├── variables.tf         # Variable definitions
├── outputs.tf           # Output definitions
├── index.html           # Homepage
├── error.html           # Error page
└── README.md            # This file
```

## 🔧 Configuration Details

### Resources Created

1. **S3 Bucket**: The main storage bucket
2. **Bucket Ownership Controls**: Sets ownership to bucket owner
3. **Public Access Block**: Disables public access blocking
4. **Bucket ACL**: Configured for public-read access
5. **S3 Objects**: Uploads index.html and error.html
6. **Website Configuration**: Enables static website hosting

### AWS Provider

- **Provider**: `hashicorp/aws` (v6.20.0)
- **Region**: `us-east-1`

## 📤 Outputs

- `websiteendpoint`: The S3 website endpoint URL where your site is accessible

## 🧹 Cleanup

To destroy all resources created by this project:

```bash
terraform destroy
```

Type `yes` when prompted to confirm the destruction.

## ⚠️ Important Notes

- The S3 bucket is configured with **public-read** access to allow website hosting
- Ensure your bucket name is globally unique across AWS
- The bucket may incur minimal AWS charges
- Remember to destroy resources when no longer needed to avoid costs

## 🔒 Security Considerations

- This configuration makes the S3 bucket and its contents publicly accessible
- Only use this setup for static website hosting with public content
- Do not store sensitive information in this bucket
- Consider adding CloudFront and Route 53 for production deployments

## 📝 Customization

### Adding More Files

To add more files to your website:

1. Create the file in the project directory
2. Add a new `aws_s3_object` resource in `main.tf`:

```hcl
resource "aws_s3_object" "new_file" {
  bucket       = aws_s3_bucket.mybucket.id
  key          = "filename.html"
  source       = "filename.html"
  content_type = "text/html"
  acl          = "public-read"
}
```

3. Run `terraform apply` to upload the new file

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

This project is provided as-is for educational and demonstration purposes.