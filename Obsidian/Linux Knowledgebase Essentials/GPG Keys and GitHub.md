To use a GPG key to sign your Git commits and get the "Verified" badge on GitHub, follow this step-by-step guide to generate, add, and configure your key. [1] (https://medium.com/codebrace/signing-commits-with-gpg-in-github-a-complete-guide-b5c930302961), [2] (https://github.com/md8-habibullah/GPG-keys-with-GitHub)

Step 1: [[Generate a GPG Key]]

If you don't have a key yet, open your terminal (or Git Bash on Windows) and run the following command: [1] (https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key), [2] (https://dev.to/ashwingopalsamy/git-github-gpg-key-windows-2016)
```
# Fill in the info command asks for
gpg --full-generate-key


```
Follow the interactive prompts: 
1. Kind of key: Select RSA and RSA (or ECC/Curve 25519 if you prefer).
2. Key size: Choose 4096 bits for security. 
3. Validity: Choose how long you want the key to last (e.g., 0 for never expires). 
4. User ID details: Enter your name and the exact email address associated with your GitHub account. 
5. Passphrase: Enter a secure passphrase to protect your key. 

Step 2: Get Your Key ID and Export It

6. Find your GPG key ID by listing your secret keys: [1] (https://dev.to/ashwingopalsamy/git-github-gpg-key-windows-2016), [2] (https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
bash
gpg --list-secret-keys --keyid-format=long
Use code with caution.
2. Look for the line starting with sec. The string of characters after the key size (e.g., after rsa4096/) is your GPG Key ID.
	• Example: In sec   rsa4096/3AA5C34371567BD2, the ID is 3AA5C34371567BD2. [1] (https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key), [2] (https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
3. Export your public key using your Key ID: [1] (https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key), [2] (https://www.youtube.com/watch?v=xj9OiJL56pM&t=187)
bash
gpg --armor --export YOUR_KEY_ID
Use code with caution.
4. Copy the entire output block, including the -----BEGIN PGP PUBLIC KEY BLOCK----- and -----END PGP PUBLIC KEY BLOCK----- lines. [1] (https://www.youtube.com/watch?v=xj9OiJL56pM&t=187), [2] (https://www.youtube.com/watch?v=Uqb-6s6h75w)

Step 3: Add the Key to Your GitHub Account

1. Go to GitHub and click your profile picture in the top-right corner, then select Settings.
2. In the left sidebar, click SSH and GPG keys.
3. Click the New GPG key button.
4. Give it a descriptive Title (e.g., "Personal Laptop").
5. Paste your copied public key block into the Key field.
6. Click Add GPG key and authenticate if prompted. [1] (https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account), [2] (https://www.youtube.com/watch?v=Uqb-6s6h75w), [3] (https://www.youtube.com/watch?v=l-XZi8LM0yM)

Step 4: Configure Git to Sign Your Commits

Now, tell Git on your local computer to use this key when committing. Run these commands in your terminal: [1] (https://medium.com/codebrace/signing-commits-with-gpg-in-github-a-complete-guide-b5c930302961)
bash
# Tell Git which key to use
git config --global user.signingkey YOUR_KEY_ID

# (Optional but recommended) Tell Git to sign all commits automatically
git config --global commit.gpgsign true

# (Optional) Tell Git to sign all tags automatically
git config --global tag.gpgsign true
Use code with caution.
(Note: Ensure your local Git email matches your GitHub account email by verifying with git config --global user.email.) [1] (https://dev.to/rose1845/how-to-set-up-gpg-keys-for-an-existing-github-account-step-by-step-2fj7)

Step 5: Test and Verify

If you didn't enable automatic signing above, you can sign an individual commit by adding the -S flag: [1] (https://medium.com/codebrace/signing-commits-with-gpg-in-github-a-complete-guide-b5c930302961)
bash
git commit -S -m "Your signed commit message"
Use code with caution.
When you push this commit to GitHub, you will see a green Verified badge next to it on the repository commit history! [1] (https://medium.com/codebrace/signing-commits-with-gpg-in-github-a-complete-guide-b5c930302961), [2] (https://github.com/md8-habibullah/GPG-keys-with-GitHub)
If you encounter an error like "gpg: signing failed: secret key not available" or if you are configuring this on a specific OS, let me know. Are you setting this up on Mac, Windows, or Linux?
