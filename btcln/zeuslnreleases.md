# Zeus LN - verifying Android APKs on Mac OSX

### Download the release files:
- you can find the ZeusLN files on their release page (https://github.com/ZeusLN/zeus/releases):

- PGP.txt
- APK
- APK signature (the .asc file)
- Signed manifest

> Note: keep all files in the same directory when running below commands
---
### Verify signatures - run these commands:
- Run the following commands to verify the APK was signed by the author/devs (based on their published PGP key)
    ```bash
    # import PGP key into your GPG keychain
    gpg --import PGP.txt
    ```
    ```bash
    # verify it
    gpg --verify zeus-v0.7.2.apk.asc zeus-v0.7.2.apk

    # should output something similar to this indicating "Good signature":
    gpg: Signature made Tue Jan 31 20:54:47 2023 CST
    gpg:                using RSA key 96C225207F2137E278C31CF7AAC48DE8AB8DEE84
    gpg:                issuer "zeusln@tutanota.com"
    gpg: Good signature from "Zeus LN <zeusln@tutanota.com>" [full]
    ```

- You can also check SHA256 sums of the release files using manifest.txt using the "shasum" command with "--check" option:
    ```bash
    shasum --check manifest-v0.7.2.txt

    # will output something similar to this:
    zeus-v0.7.2.apk: OK
    zeus-v0.7.2.apk.asc: OK
    ```
---
### Bonus one liner instead of the above 🔥:
```bash
# if you wanna do it faster 🤙 in single line
gpg --verify zeus-v0.7.2.apk.asc zeus-v0.7.2.apk && shasum --check manifest-v0.7.2.txt

# expected output
gpg: Signature made Tue Jan 31 20:54:47 2023 CST
gpg:                using RSA key 96C225207F2137E278C31CF7AAC48DE8AB8DEE84
gpg:                issuer "zeusln@tutanota.com"
gpg: Good signature from "Zeus LN <zeusln@tutanota.com>" [full]
zeus-v0.7.2.apk: OK
zeus-v0.7.2.apk.asc: OK
```