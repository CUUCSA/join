# Join CUUCSA on GitHub

This repo handles membership requests for the **Cavendish University Uganda Computing Students' Association** GitHub organization.

## 👉 Want to join?

1. Sign in to GitHub (or create a free account at https://github.com/signup).
2. Open the join form: **https://github.com/cuucsa/join/issues/new?template=join.yml**
3. Fill it in and click **Create**.
4. Once an executive approves you, accept your invitation at **https://github.com/orgs/cuucsa/invitation**

---

## Setup (for org Owners)

### 1. Create the repo
Create a **public** repo named `join` in the `cuucsa` organization and upload these files, keeping the folder structure:

```
join/
├── README.md
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── join.yml
    │   └── config.yml
    └── workflows/
        └── membership.yml
```

### 2. Create the labels
Repo > **Issues** > **Labels** > **New label**:
- `join-request`: added automatically to every request by the form
- `approved`: an executive adds this to approve a request

The form only applies `join-request` if that label already exists, so create it before sharing the link.

### 3. Create the members team
Org > **Teams** > **New team** named `members`. If you use a different name, change `TEAM_SLUG` in `membership.yml`.

### 4. Create the admin token
The built-in Actions token cannot invite people, so an org Owner must create one:

1. GitHub > **Settings** > **Developer settings** > **Personal access tokens** > **Fine-grained tokens** > **Generate new token**
2. **Resource owner:** `cuucsa`
3. **Expiration:** up to one year (set a reminder to renew it)
4. **Organization permissions** > **Members:** Read and write
5. Generate and copy the token.

If the org requires approval for fine-grained tokens, approve it under Org > **Settings** > **Personal access tokens** > **Pending requests**.

### 5. Save the token as a secret
`join` repo > **Settings** > **Secrets and variables** > **Actions** > **New repository secret**
- Name: `ORG_ADMIN_TOKEN`
- Value: the token from step 4

### 6. Share the link
Post this in the CUUCSA group:

> Join CUUCSA on GitHub 👉 https://github.com/cuucsa/join/issues/new?template=join.yml

## How approvals work

- A student submits the form. The bot thanks them and the issue waits.
- An executive checks that the person is a real Cavendish student and adds the **`approved`** label.
- The bot invites them to the org and the `members` team, posts the invite link, and closes the issue.
- To reject a request, close the issue without the label, ideally with a short comment.

Only people with triage or write access to this repo can add labels, so students cannot approve themselves. Invites always go to the account that opened the issue, so nobody can request an invite for someone else.
