
ssh-keygen -t ed25519 -C "deploy@server"

→ Enter
→ Enter (keine Passphrase)

cat ~/.ssh/id_ed25519.pub

Key kopieren und als deploy key ins Repo einfügen

testen:

ssh -T git@github.com