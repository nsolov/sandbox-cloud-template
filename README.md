# Sandbox Cloud Template

This repository is a template for deploying an InterSystems IRIS application to the InterSystems Developer Sandbox (https://cloud.sandbox.developer.intersystems.com/) with GitHub Actions.

## Deployment Instructions

1. Sign in to GitHub.

2. Open the template repository:

   <https://github.com/nsolov/sandbox-cloud-template>

3. Click **Use this template** in the upper-right corner, then select **Create a new repository**.

4. Fill in the repository creation form.

   You can create either a public or a private repository. After submitting the form, GitHub will open your newly created repository.

   You may receive a **Run failed** email notification from GitHub. This is expected at this stage because the deployment settings have not been configured yet.

5. Open the InterSystems Developer Sandbox deployments page:

   <https://cloud.sandbox.developer.intersystems.com/portal/deployments>

6. Create a new deployment and generate a service account key.

7. Save the service account key in GitHub:

   - In your repository, open **Settings**.
   - In the left menu, select **Secrets and variables**, then **Actions**.
   - Click **New repository secret**.
   - Set **Name** to:

     ```text
     SERVICE_ACCOUNT_KEY
     ```

   - In **Secret**, paste the complete contents of the key file created in the previous step.

8. Configure the deployment workflow:

   - In your repository, open the **Code** tab.
   - Open the `.github/workflows` folder.
   - Open `deploy.yml`.
   - The file is initially empty.
   - Click the pencil icon to edit the file.
   - Paste the full contents of the `deploy.yml` block from the deployment creation page.
   - Recommended, but optional: uncomment the following line to allocate 1 GiB of memory:

     ```yaml
     memory: 1Gi
     ```

   - Click **Commit changes**.
   - Use **Commit directly to the master branch**.

9. Open the **Actions** tab in GitHub.

10. Wait until the latest workflow run completes successfully and turns green.

11. Check the status of your deployment. The deployment update may take several minutes:

    <https://cloud.sandbox.developer.intersystems.com/portal/deployments>

## Configuration Reference

For a reference explanation of the IRIS configuration merge file used by this template, see [What `myapp.cpf` Is For](MYAPP_CPF.md).
