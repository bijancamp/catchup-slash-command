---
description: Compare current branch to develop and provide comprehensive summary of changes
allowed-tools: Bash(git fetch:*), Bash(git branch:*), Bash(git diff:*), Bash(git log:*), Read
---

# Catch Up on Branch Changes

Analyze all changes between the current branch and develop branch, providing a comprehensive summary to help you understand what's been done.

## Context

Get current state:

```
!git branch --show-current
!git status --short
```

## Your Task

Follow these steps to analyze branch changes:

1. **Verify branch setup**:

   - Get current branch name with `git branch --show-current`
   - Ensure we're not on develop branch
   - If on develop, inform user and stop

2. **Fetch latest develop**:

   - Run `git fetch origin develop` to ensure we have the latest
   - Handle case where remote 'origin' may not exist

3. **Get change overview**:

   - Run `git diff origin/develop...HEAD --name-only` to list all changed files
   - Run `git diff origin/develop...HEAD --stat` for change statistics
   - Run `git log origin/develop..HEAD --oneline` for commit history

4. **Analyze changed files intelligently**:

   - Review the list of changed files
   - Select the most impactful files based on:
     - Size of changes (files with significant additions/deletions)
     - File type and location in the project structure
     - Relevance to overall branch purpose
   - Focus on 5-8 key files that tell the story of what changed

5. **Read and analyze selected files**:

   - Use Read tool to examine the selected files
   - Understand the purpose and impact of changes
   - Note any architectural patterns or significant logic changes

6. **Provide comprehensive summary**:

   Present findings in this structure:

   **Branch Overview**

   - Branch name and commit count
   - Overall scope (feature, bugfix, refactor, etc.)

   **Change Statistics**

   - Files changed, insertions, deletions
   - Breakdown by file type

   **Key Changes**

   - List most significant files with brief description of changes
   - Group by category (Backend, Frontend, Infrastructure, etc.)

   **Commit History**

   - List of commits with messages
   - Note any patterns (e.g., incremental feature work, bug fixes)

   **Architectural Impact**

   - New patterns or approaches introduced
   - Dependencies or integrations added/modified
   - Potential breaking changes

   **Review Focus Areas**

   - Suggest what reviewers should pay attention to
   - Flag any complex logic or security-sensitive changes
   - Note areas that may need extra testing

## Guidelines

- **Be thorough but concise**: Provide detailed analysis without overwhelming detail
- **Prioritize effectively**: Focus on files that matter most to understanding the changes
- **Think architecturally**: Look for patterns and design decisions, not just code changes
- **Be practical**: Provide actionable insights for code reviewers
- **Handle errors gracefully**: If develop branch doesn't exist locally, provide helpful guidance

## Success Criteria

- Clear understanding of branch purpose and scope
- Identification of all key changes and their significance
- Actionable insights for code review
- No assumptions about changes - base summary on actual file analysis

## Example Output Structure

```
🔍 Branch Analysis: feature/add-user-authentication

📊 Change Statistics:
- 15 files changed (+842, -156)
- Backend: 8 files
- Frontend: 5 files
- Tests: 2 files

🎯 Key Changes:

Backend:
- contracts/UserAuthentication.sol: New smart contract for user auth
- resolvers/auth.resolver.ts: GraphQL resolver for login/logout
- handlers/jwt.handler.ts: JWT token generation and validation

Frontend:
- components/login/login.component.ts: New login form component
- services/auth.service.ts: Authentication service with token management

📝 Commits (8 total):
- Add UserAuthentication smart contract
- Implement JWT handler
- Create GraphQL auth resolver
- Build login component
...

🏗️ Architectural Impact:
- Introduces JWT-based authentication pattern
- Adds dependency on jsonwebtoken library
- New authentication middleware in GraphQL layer

👀 Review Focus Areas:
- Security: JWT implementation and token expiration handling
- Smart contract: Gas optimization in UserAuthentication.sol
- Error handling: Auth service error states and user feedback
```
