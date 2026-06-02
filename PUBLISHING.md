# Publishing

NuGet package: `Vectorizer.AI`

Publishing uses NuGet Trusted Publishing from GitHub Actions. Configure the trusted publisher in NuGet with:

- Repository owner: `clv`
- Repository name: `vectorizer-ai-dotnet`
- Workflow filename: `publish.yml`
- Environment name: `nuget`

Add the GitHub Actions secret `NUGET_USER` with the NuGet account or organization name that owns the package.

After that, update the generated package version, commit it, and push a matching SemVer tag such as `v1.0.0`. The workflow verifies that the tag matches the `.csproj`, builds, packs, publishes to NuGet without a long-lived API key, and creates a GitHub release containing the `.nupkg`.
