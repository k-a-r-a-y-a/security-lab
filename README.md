## security lab + stash and context switching
# Security Incident Lab - Secrets Removal & Stash Workflow

## Scenario
Developer accidentally committed API keys, passwords, and `.env` file during feature development.

## Part 1: Remove Secrets from History

### Simulate Accident

git checkout -b feature/payment-gateway
echo "API_KEY=sk_live_123456789" > .env
echo "DB_PASSWORD=admin123" > secrets.txt
echo "def process_payment(): return True" > payment.py
git add .
git commit -m "payment gateway "

git reset HEAD~1	Undo last commit (keep changes)
git add .gitignore	Prevent future leaks
git push --force	Overwrite remote history
git stash push -m "msg"	Save work temporarily
git stash pop	Restore and remove stash

##Security Best Practices
Rotate exposed credentials immediately

Add .env to .gitignore before first commit

Use git reset before pushing if secrets committed

Force push only on private branches

Use pre-commit hooks to scan for secrets

Deliverables
- Clean history (no secrets)
- .gitignore configured
- Stash workflow demonstrated
- Hotfix applied without losing feature work
