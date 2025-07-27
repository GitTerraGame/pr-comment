# GitTerra PR Comment Action

This GitHub Action adds a comment to a pull request wiht a link to map generated using Play GitTerra Action published to GitHub Pages site for your repo.

## Usage

Include this action as a last step of your `.github/workflows/gitterra.yml` file:

```yaml
name: Play GitTerra
run-name: Playing 🌎 GitTerra on ${{ github.repository }} 🗺️

  ...

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  ...
  id-token: write # Allows the action to request an ID token for authentication
  pull-requests: write # Allows the action to add a comment to the pull request

jobs:
  play-gitterra: ...
  deploy-gitterra-to-gh-pages: ...
  add-pr-comment:
    name: Add PR comment with GitTerra map link
    runs-on: ubuntu-latest
    needs: deploy-gitterra-to-gh-pages # Ensures this job runs after deployment job
    steps:
      - name: Leave a 💬 comment on PR with preview 🗺️ image and 🔗 link to the site
        uses: GitTerraGame/pr-comment@main # Calls the PR Comment action
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }} # Provide the GitHub token to authenticate with the GitHub API
```

This only shows the relevant part of the workflow file, you can find the full example in the [Play GitTerra Action](https://github.com/GitTerraGame/Play-GitTerra-Action?tab=readme-ov-file#deploy-the-map-to-github-pages) repository

### Permissions

The action requires `id-token: write` permission to request an ID token for authentication and `pull-requests: write` permission to be able to add a comment to the pull request.

These permissions are set in the `permissions` section of the workflow file.
