---
name: verify-shipped-artifact
description: Verify a release candidate or published installer, package, or updater from the consumer's entry point. Use when a release claim depends on what users actually receive, not for routine source tests.
license: MIT
---

# Verify the shipped artifact

Answer a concrete question: can a user on a supported system get the intended version and use the change? Keep build, delivery, and use as separate results. This check does not authorize a deployment.

1. Identify the release, source revision, platform, distribution channel, and one action that distinguishes the candidate from the previous version. Obtain the expected digest from a trusted build record or signed manifest, not from the downloaded file itself. A matching version string is insufficient.
2. Fetch from the same entry point a user would use, into an empty directory. Record the response status, actual byte count, and digest. Follow the real redirect chain. A successful HEAD request, a cached partial response, or a matching local build does not prove delivery.
3. Apply the platform's normal signature or package verification to the fetched bytes. Exercise the actual consumer in a disposable environment: install from the downloaded package, or feed the archive to the supported updater starting at the previous version. Listing an archive does not exercise its extractor. Do not install over a user's working copy.
4. Run the distinguishing action on that installation. Record the observable output and exit status. When piping logs through another program, preserve the status of the command under test. A green summary or a stamp from another checkout is not proof that a check ran.

Report the tested channel and platform, expected and observed artifact identity, action and result. If the package is only on staging, say “verified on staging”; if no supported runner is available, identify the untested step. Don't infer automatic updates from a successful fresh installation.

Example: a package downloads and installs, but the previous version's updater refuses one archive member. Report a passing fresh install and a failing update. Keep the update channel out of the success claim.
