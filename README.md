# 🚀 devops-terraform-services-netlify

[![Terraform](https://img.shields.io/badge/Terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)](https://www.terraform.io/)
[![Netlify](https://img.shields.io/badge/Netlify-%2300C7B7.svg?style=for-the-badge&logo=netlify&logoColor=white)](https://www.netlify.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

[![Terraform Version](https://img.shields.io/badge/terraform-%3E%3D1.0.0-blue)](https://www.terraform.io/)
[![Netlify Provider](https://img.shields.io/badge/netlify_provider-%3E%3D0.13.0-00C7B7)](https://registry.terraform.io/providers/netlify/netlify/latest)
![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)

---

## 📋 Overview

Infrastructure as Code (IaC) repository for managing Netlify resources using Terraform. This module provides a declarative way to provision and manage Netlify sites, DNS, environment variables, and deployment configurations.

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🌐 **Site Management** | Create and configure Netlify sites |
| 🔒 **Environment Variables** | Securely manage environment variables |
| 📡 **DNS Configuration** | Manage DNS zones and records |
| 🔗 **Deploy Hooks** | Configure build and deploy hooks |
| 🛡️ **Access Control** | Manage team access and permissions |
| 📦 **Build Settings** | Configure build commands and publish directories |

## 📁 Repository Structure

```
.
├── 📄 main.tf              # Primary resource definitions
├── 📄 variables.tf         # Input variable declarations
├── 📄 outputs.tf           # Output value definitions
├── 📄 providers.tf         # Provider configuration
├── 📄 versions.tf          # Terraform version constraints
├── 📄 terraform.tfvars     # Variable values (git-ignored)
├── 📁 modules/             # Reusable Terraform modules
│   ├── 📁 site/            # Netlify site module
│   ├── 📁 dns/             # DNS configuration module
│   └── 📁 deploy-hooks/    # Deploy hooks module
├── 📁 environments/        # Environment-specific configs
│   ├── 📁 dev/
│   ├── 📁 staging/
│   └── 📁 prod/
└── 📄 README.md
```

## 🚦 Prerequisites

- [![Terraform](https://img.shields.io/badge/Terraform-≥1.0.0-5835CC?logo=terraform)](https://www.terraform.io/downloads) installed
- [![Netlify](https://img.shields.io/badge/Netlify-Account-00C7B7?logo=netlify)](https://app.netlify.com/signup) with API access
- Netlify Personal Access Token

## 🔧 Quick Start

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/your-org/netlify-terraform.git
cd netlify-terraform
```

### 2️⃣ Configure Authentication

```bash
export NETLIFY_TOKEN="your-netlify-personal-access-token"
```

Or add to `terraform.tfvars`:

```hcl
netlify_token = "your-netlify-personal-access-token"
```

### 3️⃣ Initialize Terraform

```bash
terraform init
```

### 4️⃣ Plan and Apply

```bash
terraform plan
terraform apply
```

## 📝 Usage Examples

### Basic Site Configuration

```hcl
module "netlify_site" {
  source = "./modules/site"

  name              = "my-awesome-site"
  repo_url          = "https://github.com/your-org/your-repo"
  repo_branch       = "main"
  build_command     = "npm run build"
  publish_directory = "dist"

  environment_variables = {
    NODE_VERSION = "18"
    API_URL      = "https://api.example.com"
  }
}
```

### DNS Configuration

```hcl
module "netlify_dns" {
  source = "./modules/dns"

  domain = "example.com"
  
  records = [
    {
      type     = "A"
      hostname = "@"
      value    = "75.2.60.5"
    },
    {
      type     = "CNAME"
      hostname = "www"
      value    = "example.netlify.app"
    }
  ]
}
```

## 📥 Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| `netlify_token` | Netlify Personal Access Token | `string` | n/a | ✅ |
| `site_name` | Name of the Netlify site | `string` | n/a | ✅ |
| `repo_url` | Repository URL for the site | `string` | n/a | ✅ |
| `repo_branch` | Branch to deploy | `string` | `"main"` | ❌ |
| `build_command` | Build command | `string` | `""` | ❌ |
| `publish_directory` | Publish directory | `string` | `"."` | ❌ |
| `environment_variables` | Environment variables map | `map(string)` | `{}` | ❌ |

## 📤 Outputs

| Name | Description |
|------|-------------|
| `site_id` | The unique ID of the Netlify site |
| `site_url` | The URL of the deployed site |
| `deploy_url` | The deploy-specific URL |
| `ssl_url` | The SSL URL of the site |
| `admin_url` | The Netlify admin URL |

## 🔐 Security

> ⚠️ **Important**: Never commit sensitive values to version control!

- Store `terraform.tfvars` in `.gitignore`
- Use environment variables for tokens
- Consider using HashiCorp Vault or AWS Secrets Manager for production

```bash
# .gitignore
*.tfvars
*.tfstate
*.tfstate.*
.terraform/
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. 🍴 Fork the repository
2. 🌿 Create a feature branch (`git checkout -b feature/amazing-feature`)
3. 💾 Commit your changes (`git commit -m 'Add amazing feature'`)
4. 📤 Push to the branch (`git push origin feature/amazing-feature`)
5. 🔃 Open a Pull Request

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**[📖 Documentation](https://docs.netlify.com/)** · **[🐛 Report Bug](https://github.com/your-org/netlify-terraform/issues)** · **[✨ Request Feature](https://github.com/your-org/netlify-terraform/issues)**

Made with ❤️ by Your Team

</div>
