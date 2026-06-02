# Publishing

NuGet package: `Vectorizer.AI`

Publishing uses NuGet Trusted Publishing from GitHub Actions. Configure the trusted publisher in NuGet with:

- Repository owner: `clv`
- Repository name: `vectorizer-ai-dotnet`
- Workflow filename: `publish.yml`
- Environment name: `nuget`

Add the GitHub Actions secret `NUGET_USER` with the NuGet account or organization name that owns the package.

After that, push a SemVer tag such as `v1.0.0`. The workflow builds, packs, publishes to NuGet without a long-lived API key, and creates a GitHub release containing the `.nupkg`.
