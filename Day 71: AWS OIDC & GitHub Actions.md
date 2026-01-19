# ☁️ AWS OIDC & GitHub Actions (ClickOps Guide)

This guide documents the manual "ClickOps" method to connect GitHub Actions to AWS without using long-term Access Keys.

## 🎯 The Goal
To allow GitHub Actions to "assume" an IAM Role in your AWS account temporarily using OpenID Connect (OIDC).

---

## 🛠 Step 1: Create the Identity Provider
*This tells AWS to trust tokens signed by GitHub.*

1.  Log in to the **AWS Console**.
2.  Navigate to **IAM** (Identity and Access Management).
3.  Click **Identity providers** in the left sidebar.
4.  Click the **Add provider** button.
5.  Select **OpenID Connect**.
6.  Fill in the details:
    * **Provider URL:** `https://token.actions.githubusercontent.com`
    * **Audience:** `sts.amazonaws.com`
7.  Click **Get thumbprint** (AWS verifies the certificate).
8.  Click **Add provider**.

---

## 🔐 Step 2: Create the IAM Role
*This creates the specific "hat" that GitHub Actions will wear.*

1.  Navigate to **Roles** in the IAM sidebar.
2.  Click **Create role**.
3.  **Trusted entity type:** Select **Web identity**.
4.  **Web identity settings:**
    * **Identity provider:** Choose the one you just created (`token.actions.githubusercontent.com`).
    * **Audience:** Choose `sts.amazonaws.com`.
    * **GitHub organization:** Enter your username (e.g., `iftekharchowdhuryJOY`).
    * **GitHub repository:** Enter your repo name (e.g., `my-tech-blog`).
5.  Click **Next**.
6.  **Add permissions:** Search for and select `AmazonS3ReadOnlyAccess` (safe for testing).
7.  Click **Next**.
8.  **Role name:** Give it a clear name like `GitHubActions-OIDC-Role`.
9.  Click **Create role**.

**⚠️ Important:** Once created, click on the role and copy the **ARN** (Amazon Resource Name). It looks like:
`arn:aws:iam::123456789012:role/GitHubActions-OIDC-Role`


## 🧪 Step 3: The GitHub Workflow
*This script tests the connection.*

Create a file in your repo at `.github/workflows/oidc-test.yml`:

```yaml
name: AWS OIDC Practice

on: [push]

permissions:
  id-token: write  # REQUIRED for OIDC
  contents: read

jobs:
  aws-login:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v3
        with:
          # PASTE YOUR ROLE ARN BELOW
          role-to-assume: arn:aws:iam::123456789012:role/GitHubActions-OIDC-Role
          aws-region: us-east-1

      - name: Verify Login
        run: aws sts get-caller-identity


```
# 🧹 Cleanup Guide (Manual/ClickOps)

Follow these steps to remove the OIDC resources you created manually.

## 🗑 Step 1: Delete the IAM Role
*You must delete the role before or after the provider; the order does not matter, but deleting the role first is good practice.*

1.  Log in to the **AWS Console**.
2.  Navigate to **IAM** -> **Roles**.
3.  Search for your role name (e.g., `GitHubActions-OIDC-Role`).
4.  Select the checkbox next to the role name.
5.  Click the **Delete** button.
6.  Confirm the deletion by typing the role name in the text box and clicking **Delete**.


## 🗑 Step 2: Delete the Identity Provider
*This removes the "handshake" trust between AWS and GitHub.*

1.  Navigate to **IAM** -> **Identity providers** (left sidebar).
2.  Select the button next to the provider URL: `token.actions.githubusercontent.com`.
3.  Click the **Delete** button at the top right.
4.  Confirm the deletion by clicking **Delete**.

## ✅ Verification
1.  Go to your GitHub Repository -> **Actions** tab.
2.  Re-run the **"AWS OIDC Practice"** workflow.
3.  **Expectation:** It should **FAIL** at the "Configure AWS Credentials" step because the role and trust no longer exist.

