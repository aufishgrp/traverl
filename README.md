# traverl
Configuration that allows travis-ci to manage deployment of erlang libraries.

## Usage
### Development Practices
Traverl is intended to be used with a specific git workflows. 

#### Typical usage
1. Work is done in a feature branch created from the dev branch.
2. Feature branch is goes through PR and is squashed and merged into dev.

#### Deploying
1. A PR is created to merge dev into master.
2. Dev is merged into master and a merge commit is created.
3. When travis see's that a new merge commit exists in master.
 1. A version number is generated in the format of VERSION.X. VERSION is the value within the file VERSION. X is the number of merge commits in master since VERSION.0.
 2. Release notes are generated based on the commits since the last merge commit.
 3. A tag for the version is created with the release notes generated.
4. When travis is asked to build a tag it validates the build and then deploys to hex.

### Travis configuration

Travis allows the user to make additional environment variables accessible to the build processes. The following values are expected to be set.

#### Git configuration
```
GIT_URL :: https://github.com/{GIT_OWNER}/{GIT_REPO}.git
```

##### GIT_REPO
The name of the git repository being used.

##### GIT_OWNER
The name of the entity that owns the git repo being used. 

##### GIT_KEY
A git personal access token that can be used to create tags.

#### Hex configuration
##### HEX_USERNAME
The username to use when pushing a package to hex.

##### HEX_KEY
The api key for hte hex repository.
