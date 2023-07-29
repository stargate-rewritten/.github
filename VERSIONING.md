# Stargate Versioning Revision 5
## Requirements:
### Background:
Presently, the Stargate Rewritten project maintains five branches.<br>
Although the vast majority of changes are made to the Nightly branch, occasionally, hotfixes are required which push directly to a higher-level branch.<br>
The  branches, and the typical scope of their changes, are largely as follows:

- ESR
  - Hotfixes for critical issues discovered on older builds.
- Release
  - Hotfixes for major issues that somehow made it out of the beta cycle.
- Beta
  - Balance and design tweaks adding minor improvements to improve UE.
  - Hotfixes for major issues that somehow made it out of the alpha cycle.
  - Groups of fixes for minor issues that made it out ot the alpha cycle.
    - Development on these features will occur in the usual Nightly>Alpha cycle and will be packaged into betas.
- Alpha
  - Hotfixes for major issues when discovered.
  - Groups of minor fixes as and when discovered.
- Nightly
  - Day to day development efforts.
  
### Information needed from the release number.
For the release, beta, and alpha channels, a dedicated number detailing the most recent releases of each branch a revision pertains to is needed.<br>
  Moreover, it also is neccessary to directly communicate to the users the stream from which a build was produced.
  
  For nightly builds, dedicated numbers become problematic insofar as development in this branch is usually incomplete, builds are made arbitrarily, and commits are not neccessarily linear. It is, however, neccessary to be able to distinguish between different nightly builds on occasion.
  
  For ESR branches, it needs to be possible to make exceptions to this numbering system since they are, in effect, forks.
  
 ## Numbering Specification
 Therefore, when possible, we have decided to stick to the following numbering standard:
 
 ` {Rewrite}.{Release}.{Beta}.{Alpha}[-(BRANCH)[-<Nightly Increment>]]`
 
 The Rewrite, Release, Beta, and Alpha values are integers that get incremented on every release to that channel.<br>
 
 The branch is a string detailing the name of the channel for/from which this build was produced.<br>
 Note that Release and Rewrite do not need a branch label; when a branch tag is omitted, it is assumed to be a release or a superrelease (rewrite).
 <Br>If properly tested to release standards, hotfixes may be published as alpha and/or beta increments with the omitted label signifying a release.
 
 For the ESR branch, we have taken key releases from the past and appended the branch label ESR.
 <br>These builds will have their alpha number incremented for every new release. The Nightly Increment is excluded from these builds.
 
 The Nightly Increment is just a value used for internal development purposes whenever it is needed to distinguish between two development builds. <br>It may be a commit number, or just an arbitrary integer; ideally, when our build pipeline is established, it should always be a commit number.
 
 
### Examples
 ```
Release version two of the rewrite.
1.2.0.0
| |_____ Release Two
|_______ The Rewrite
 
The third release from the beta cycle following release 2, part of the rewrite.
1.2.3.0-BETA
| | |     |_ Released from the beta branch.
| | |___ Beta Release 3
| |_____ Based on Release Two
|_______ The Rewrite
 
The fourth alpha cycle following beta release 3, following release 2, part of the rewrite. 
1.2.3.4-ALPHA
| | | |  |_ Released from the alpha branch.
| | | |_ The fourth alpha cycle
| | |___ Based on the third beta cycle
| |_____ Based on Release Two
|_______ The Rewrite

A random commit made since the last alpha release (in preparation for the 1.2.3.5 alpha release)
1.2.3.4-NIGHTLY
| | | |  |_ Released from the nightly branch.
| | | |_ Following the fourth alpha cycle
| | |___ Based on the third beta cycle
| |_____ Based on Release Two
|_______ The Rewrite

A random commit made since the last alpha release (in preparation for the 1.2.3.5 alpha release)
1.2.3.4-NIGHTLY-4
| | | |  |      |_Arbitrarily differentiated with an integer.
| | | |  |_ Released from the nightly branch.
| | | |_ Following the fourth alpha cycle
| | |___ Based on the third beta cycle
| |_____ Based on Release Two
|_______ The Rewrite

A random commit made since the last alpha release (in preparation for the 1.2.3.5 alpha release)
1.2.3.4-NIGHTLY-9543809
| | | |  |      |_Arbitrarily differentiated with a commit number.
| | | |  |_ Released from the nightly branch.
| | | |_ Following the fourth alpha cycle
| | |___ Based on the third beta cycle
| |_____ Based on Release Two
|_______ The Rewrite

A hotfix published for release 1.2.0.0
1.2.1.0
| | |  |_ Omitted branch tag, signifying release.
| | |___ Increment to release two.
| |_____ Based on Release Two
|_______ The Rewrite

If 1.2.1.0 was the last release for that version, if 1.3.0.0 was the following release, and if 1.2.0.0 was forked for an ESR, this would be the correct numbering for revisions to said ESR.
1.2.1.1_ESR
| | | |_ The most recent hotfix revision made for/from the ESR.
|_|_|_ Numbers from the previous release cycle, kept for reference

If, for some reason, we decided to rewrite the codebase again, the rewrite number would be bumped.
2.0.0.0
|_____ The second rewrite.

Old legacy builds will be indicated with 0, for pre-rewrite.
0.10.8.1
|  |_|_|_ Old legacy versioning scheme.
|________ The legacy version of the plugin (before rewrite)
```
