# USAGE

1. Fork repo
2. Run the following command to run DependencyTrack locally
```bash
curl -LO https://dependencytrack.org/docker-compose.yml
docker-compose up -d
```
3. DependencyTrack will use port 8080(frontend) and 8081(backend). Expose backend port using `ngrok` or `localtunnel`
4. Default username and password for DependancyTrack is `admin` and `admin` respectively.
5. In DependancyTrack, navigate to `Administration` > `Access Management` > `Teams` > `Automation` to get API key
6. Visit [OSS Index Sonatype](https://ossindex.sonatype.org/) to register and get yourself an API key
7. In DependencyTrack, navigate to `Administration` > `Analyzers` > `Sonatype OSS Index`. Enable and fill in the appropiate details. (This is for scanning RubyGems based on Sonatype OSS Index)
8. Create a project in DependencyTrack and take note of the UUID.
9. In the forked repo, set secrets with the following
    - `DT_API_KEY`
    - `DT_API_URL` (Exposed URL)
    - `DT_APPLICATION_UUID`
10. Make some changes and push. `bom.xml` will be generated and upload to DependancyTrack in the pipeline.

# NOTES
1. There will be a dependancy check in the pipeline using `bundle-audit`. Pipeline will fail if there is existing vulnerability.
2. DependancyTrack will monitor projects for every 6 hours and will alert (if notification is set) if there is a new vulnerability.