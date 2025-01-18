# AutoPkg GitHub Actions for Jamf Integration

This repository is designed to automate the process of running AutoPkg recipes and integrating them with Jamf Pro using GitHub Actions. Follow the steps below to set up and use this repository.

---

## Implementation Steps

### 1. Create a New Repository in GitHub
- Create a new repository with **Actions** enabled.
- Clone the repository locally to your machine.

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

### 2. Set Up the Workflows Directory
- Create the `.github/workflows` directory:

```bash
mkdir -p .github/workflows
```

- Use **CMD + Shift + Period** on macOS to view hidden directories if using Finder.

### 3. Add the Workflow File
- Copy or create the `autopkg.yml` file in the `.github/workflows` directory of your repository.

### 4. Review and Customize the Workflow
- Open the `autopkg.yml` file and configure it based on your requirements:
  - Schedule using `cron`.
  - Run manually using `workflow_dispatch`.
  - Automatically trigger on repository changes.

### 5. Set Up the Required Files and Directories
- Create the following files and directories in your repository:

```bash
mkdir overrides
```

- Create the necessary files:

```bash
touch autopkg_tools.py recipe_list.json repo_list.txt requirements.txt
```

**Descriptions of Files:**
- `overrides/`: Directory for override recipes and templates.
- `autopkg_tools.py`: Helper Python script for AutoPkg workflows.
- `recipe_list.json`: JSON file listing recipes to run.
- `repo_list.txt`: Text file containing URLs of parent repositories for AutoPkg.
- `requirements.txt`: Python dependencies for the project.

### 6. Configure GitHub Secrets
- Add your Jamf Pro credentials as **Secrets** in GitHub:
  1. Navigate to **Settings > Secrets and Variables > Actions** in your repository.
  2. Add the following secrets:
     - `JAMF_URL`: Jamf Pro server URL (e.g., `https://yourcompany.jamfcloud.com`).
     - `JAMF_API_USERNAME`: Jamf Pro API username.
     - `JAMF_API_PASSWORD`: Jamf Pro API password.
  3. Optionally, add a Slack Webhook URL (`SLACK_WEBHOOK_URL`) for notifications.

### 7. Grant Permissions for JamfUploader
- Ensure the Jamf Pro API user has permissions for:
  - Creating and updating policies.
  - Uploading and managing packages.
  - Managing computer groups.

### 8. Create Override Recipes
- Place custom override recipes in the `overrides/` directory.
- Include templates like `JamfPolicyTemplate.xml` if needed.

### 9. Add Recipes and Repositories
- **Update `recipe_list.json`**: Add override recipe paths.

```json
[
  "overrides/AWSCLI.jamf.recipe.yaml"
]
```

- **Update `repo_list.txt`**: Add URLs of parent repositories:

```txt
https://github.com/autopkg/grahampugh-recipes
https://github.com/autopkg/homebysix-recipes
```

### 10. Run the Workflow
- Push changes to GitHub:

```bash
git add .
git commit -m "Initial setup for AutoPkg with Jamf integration"
git push origin main
```

- Go to the **Actions** tab in GitHub.
- Select your workflow and click **Run Workflow**.
- Optionally, provide the path to a single recipe or leave it blank to run all recipes listed in `recipe_list.json`.

### 11. Monitor Workflow Execution
- Review the workflow logs in GitHub Actions.
- Ensure:
  - Recipes are processed.
  - Packages are uploaded to Jamf Pro.
  - Policies or smart groups are created as expected.

### 12. Verify Results in Jamf Pro
- Log in to Jamf Pro and verify:
  - Uploaded packages.
  - Created or updated policies.
  - Any other changes specified by the recipes.

### 13. Iterate and Automate
- Refine the workflow by:
  - Adding error handling in `autopkg_tools.py`.
  - Customizing workflow schedules.
  - Expanding the list of recipes and repositories.

---

## References
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [JAMF-AutoPkg Documentation][(https://github.com/autopkg/autopkg)](https://github.com/bolaussen/fastly-autopkg)
- [JamfUploader Documentation](https://github.com/grahampugh/jamf-upload)
