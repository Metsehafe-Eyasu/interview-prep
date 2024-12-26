# How to Contribute

Welcome! We appreciate your interest in contributing to this interview prep repository. This document will guide you through our **branching workflow**, **file structure**, and **content templates**.

## Table of Contents
1. [Repository Overview](#repository-overview)
2. [Branching & Pull Request Workflow](#branching--pull-request-workflow)
3. [Folder Structure & Examples](#folder-structure--examples)
4. [Adding a New Company](#adding-a-new-company)
5. [Adding a Technical or System Design Question](#adding-a-technical-or-system-design-question)
6. [Adding Behavioral Questions (One File for Multiple Questions)](#adding-behavioral-questions-one-file-for-multiple-questions)
7. [Role Field (New Grad vs. Internship)](#role-field-new-grad-vs-internship)
8. [Updating the MkDocs Navigation](#updating-the-mkdocs-navigation)
9. [Submitting Your Pull Request](#submitting-your-pull-request)
10. [Need Help?](#need-help)

---

## Repository Overview

- We use **MkDocs** to generate a static site from the `docs/` folder.
- The **`docs/example/`** folder contains **placeholder files** showing how to structure:
  - `guide.md` (company guide)
  - `technical/` questions (LeetCode-like)
  - `system-design/` questions
  - `behavioral/` questions
- Each **company** has a folder under `docs/`, e.g., `docs/google`, `docs/bloomberg`, etc.

> **Important**: Our **`main`** branch is **protected**. You **cannot** push directly to `main`. Instead, create a branch, commit your changes, and open a **Pull Request**.

---

## Branching & Pull Request Workflow

1. **Clone or Fork** the Repository  
   - If you’re an external contributor, [Fork the repo](https://docs.github.com/en/get-started/quickstart/fork-a-repo).  
   - If you’re part of the core team, clone it directly and create new branches in the **same** repository.

2. **Create a Branch**  
   - From your local repo, create a branch off of `main`:
     ```bash
     git checkout main
     git pull origin main
     git checkout -b your-feature-branch
     ```

3. **Make Your Changes**  
   - Add or modify files under `docs/`.
   - Update `mkdocs.yml` navigation if necessary.

4. **Commit & Push**  
   ```bash
   git add .
   git commit -m "Add new Google system design question"
   git push origin your-feature-branch
   ```

5. **Open a Pull Request**  
   - On GitHub, navigate to **Pull Requests** and click **“New Pull Request”**.
   - Compare **your-feature-branch** to **main**.
   - Fill out the PR template, describing your changes.

6. **Review & Merge**  
   - A maintainer or other collaborators will review your PR.
   - Once approved, the PR is merged into `main`, triggering an automatic MkDocs build and deployment.

---

## Folder Structure & Examples

Here’s a simplified view of our `docs/` folder:

```
docs/
├── example/
│   ├── guide.md
│   ├── technical/
│   │   └── example-technical-question.md
│   ├── system-design/
│   │   └── example-system-design-question.md
│   └── behavioral/
│       └── example-behavioral-questions.md
├── google/
│   ├── guide.md
│   ├── technical/
│   ├── system-design/
│   └── behavioral/
├── bloomberg/
│   ├── guide.md
│   ├── technical/
│   ├── system-design/
│   └── behavioral/
└── ... (other companies)
```

Use the **`example/`** folder to see how front matter and formatting should look.  

---

## Adding a New Company

If you want to create a folder for a **new company** (e.g., `meta`), follow these steps:

1. **Create the Folder**:  
   ```bash
   mkdir -p docs/meta/{technical,system-design,behavioral}
   ```
   Then add `guide.md` under `docs/meta/`.

2. **Copy Placeholders** from `docs/example/`  
   - For each subfolder (`technical/`, `system-design/`, `behavioral/`), you can copy the example files, rename them, and adjust the content.

3. **Update** the front matter in each file to match the new company name:
   ```yaml
   company: "Meta"
   ```

4. **Add** the new company to `mkdocs.yml` under `nav:` so it shows in the site navigation.

---

## Adding a Technical or System Design Question

1. **Decide Which Company** (e.g., Google).
2. **Create a Markdown File** in either `technical/` or `system-design/`:
   ```bash
   docs/google/technical/max-subarray.md
   ```
3. **Use the Example Template** from `docs/example/technical/example-technical-question.md` or `docs/example/system-design/example-system-design-question.md`.
4. **Front Matter** example for a technical question:
   ```yaml
   ---
   title: "Max Subarray Problem"
   company: "Google"
   category: "technical"
   role: "new-grad"
   date: "2025-01-01"
   ---
   ```
5. **Write the Content**: Problem statement, approach, complexity analysis, code snippet, etc.
6. **Update `mkdocs.yml`**:
   ```yaml
   nav:
     - Google:
       - Technical:
         - Max Subarray: google/technical/max-subarray.md
   ```
7. **Commit & Open a PR** (see the [Branching & Pull Request Workflow](#branching--pull-request-workflow) above).

---

## Adding Behavioral Questions (One File for Multiple Questions)

We use **one Markdown file** per contributor or per interview experience. That means **all** the behavioral questions you want to share from a single session or personal experience go into **one** file.

1. **Create** a file in `docs/<company>/behavioral/`, e.g.:  
   ```bash
   docs/google/behavioral/jane-summer-2025-questions.md
   ```
2. **Use** the front matter from the `example/behavioral/example-behavioral-questions.md`. Example:
   ```yaml
   ---
   title: "Behavioral Questions from My Summer 2025 Google Interview"
   company: "Google"
   category: "behavioral"
   role: "internship"
   date: "2025-05-01"
   ---
   ```
3. **Add** multiple questions in the file:
   ```markdown
   ## Question 1: "Tell me about a time you overcame a big challenge."
   ### Situation
   ...
   ### Task
   ...
   ### Action
   ...
   ### Result
   ...
   
   ## Question 2: "Describe a conflict with a team member and how you resolved it."
   ...
   ```
4. **Update `mkdocs.yml`**:
   ```yaml
   nav:
     - Google:
       - Behavioral:
         - Jane's Summer 2025 Questions: google/behavioral/jane-summer-2025-questions.md
   ```
5. **Commit & Pull Request**.

---

## Role Field (New Grad vs. Internship)

In the front matter of **any** question (technical, system-design, or behavioral), use `role: "new-grad"` or `role: "internship"` so readers know which audience the content is intended for. Example:

```yaml
---
title: "Max Subarray Problem"
company: "Google"
category: "technical"
role: "new-grad"
date: "2025-01-01"
---
```

---

## Updating the MkDocs Navigation

Whenever you add or rename files:

1. Open `mkdocs.yml` in the repository root.
2. Scroll to the `nav:` section.
3. Add your new page under the correct company and category. For example:
   ```yaml
   nav:
     - Home: index.md
     - Google:
       - Guide: google/guide.md
       - Technical:
         - Max Subarray: google/technical/max-subarray.md
       - Behavioral:
         - Jane's Summer 2025 Questions: google/behavioral/jane-summer-2025-questions.md
   ```
4. **Save** and **commit**.

This ensures your new content appears in the site’s navigation menu.

---

## Submitting Your Pull Request

Here’s a **quick recap** of the PR process:

1. **Create** or **switch to** your branch:
   ```bash
   git checkout -b add-google-tech-q
   ```
2. **Make Changes** (add/edit files).
3. **Commit**:
   ```bash
   git add .
   git commit -m "Add new Google technical question on max subarray"
   ```
4. **Push** to remote:
   ```bash
   git push origin add-google-tech-q
   ```
5. **Open a Pull Request** on GitHub:
   - Compare your branch (`add-google-tech-q`) with `main`.
   - Fill in the PR template, describing the changes.
6. **Request Reviews** if needed. Once approved, your PR will be merged, and the site will be automatically rebuilt.

> **Note**: Please keep your PRs focused on one topic. For example, **don’t** add a brand-new company and a major reorganization of existing content in one PR. Smaller, focused PRs are easier to review and merge.

---

## Need Help?

- **Open an Issue** in the GitHub repo if you need clarification or encounter problems.
- Tag maintainers or other contributors in your PR if you need a review or have specific questions.

Thank you for contributing! Together, we’re building a valuable resource for technical and behavioral interview preparation.