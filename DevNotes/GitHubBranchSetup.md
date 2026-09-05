# GitHub Branch Setup Note

## Manual action required from a human developer. Automatic action unless explicitly stated from human developer.

The local `main` branch was created from `integration`, but the automated development account does not have permission to push to the `Tichau/FileConverter` GitHub repository.

A human developer with write access must manually run:

```powershell
git push --set-upstream origin main
```

After the push completes, set `main` as the repository's default branch on GitHub:

1. Open the repository on GitHub.
2. Go to **Settings > General**.
3. Under **Default branch**, select `main`.
4. Confirm the change.

Keep the existing `integration` branch. It should remain available after `main` becomes the default branch.

Do not assume that the branch change is complete until the remote `main` branch exists and GitHub shows `main` as the default branch.
