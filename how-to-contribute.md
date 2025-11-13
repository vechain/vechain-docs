---
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
  metadata:
    visible: true
---

# How to contribute

## Create Issues

If you've identified an issue in the documentation, have a suggestion for additional content, or see an opportunity for improvement, please raise an issue:

1. Navigate to the main page of the GitHub repository.
2. Click the "Issues" button.
3. Click "New Issue".
4. Provide an informative "Title".
5. Provide a description of your issue / suggestion / improvement in the comment body field.
6. When you are finished click "Submit new issue".

## Submitting Pull Requests

To propose changes to the documentation directly, you can submit a pull request. Here's the general process:

1. Fork the project.
2. Create a topic branch from `master`.
3. Make some commits to improve the project. **Please make sure that if you are creating a new page/section you update the summary.md file or the navbar will not be updated and the new page/section will not be visible.**
4. Push this branch to your GitHub project.
5. Open a Pull Request on GitHub.
6. Discuss, and optionally continue committing.
7. The project owner merges or closes the Pull Request.
8. Sync the updated `master` back to your fork.

## Step-by-Step Guide for Pull Requests

1. Fork the repository: Click the "Fork" button at the top right of the repository page.
2. Clone your fork: git clone https://github.com/YOUR-USERNAME/REPOSITORY-NAME.git
3. Create a new branch: `git checkout -b your-feature-branch`
4. Make your changes: Edit the necessary files.
5. Commit your changes: `git commit -am "Add a descriptive commit message"`
6. Push to your fork: `git push origin your-feature-branch`
7. Create a Pull Request: Go to the original repository and click "New pull request". Choose your fork and the branch containing your changes.
8. Describe your changes: Provide a clear title and description for your pull request.
9. Submit the Pull Request: Click "Create pull request".

Remember to keep your fork synchronized with the original repository to avoid conflicts. You can do this by adding the original repository as a remote and pulling from it regularly:

```bash
git remote add upstream https://github.com/ORIGINAL-OWNER/ORIGINAL-REPOSITORY.git
git fetch upstream
git merge upstream/master
```

Your contributions help improve the documentation for everyone. Thank you for your effort!
