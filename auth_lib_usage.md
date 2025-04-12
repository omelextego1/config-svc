---
sidebar_position: 2
sidebar_label: auth-lib usage
title: How the Auth Library is used
date: 2025-04-09
author: Ome Chukwuemeka
SPDX-License-Identifier: (c) LexTego Ltd
---

## Introduction

The `auth-lib` is used within the `config-svc-be` service to validate JWT tokens and determine whether a user has the required privileges to access a specific endpoint. This validation process is critical in ensuring secure role-based access control across both the frontend and backend services in the platform.

## Core Usage Flow

The authentication and authorization process is driven by three primary components:

- **JwtAuthGuard**: Responsible for decoding the token sent from the frontend.
- **PrivilegeService**: Implements `validateTokenAndClaims` to verify if the decoded token includes the required privileges.
- **RolesGuard**: Applied at controller-level to enforce access control based on the results from the PrivilegeService.

## Access Control Flow

```mermaid
sequenceDiagram
Title: Token Validation and Privilege Check
autonumber

actor user as Authenticated User
participant fe as Frontend
participant be as Backend (config-svc-be)
participant jwt as JwtAuthGuard
participant priv as PrivilegeService
participant ctrl as RolesGuard

user->>fe: Accesses a protected page
fe->>fe: Check if user has privilege<br/>for the page (UI-level)
alt No privilege
    fe->>user: Access Denied (UI Block)
else Has privilege
    fe->>be: Send request with JWT token<br/>in Authorization header
    activate be
    be->>jwt: Decode JWT Token
    jwt->>fe: Attach user profile
    be->>priv: validateTokenAndClaims(token, requiredPrivileges[])
    alt Token invalid or missing privileges
        priv->>ctrl: return false
        ctrl->>be: Deny request
        be->>fe: 403 Forbidden
        fe->>user: Access Denied
    else Privilege matched
        priv->>ctrl: return true
        ctrl->>be: Allow request
        be->>fe: Return protected data
        fe->>user: Page loaded successfully
    end
end
```

## Template Key Verification

**Current Issue**

There is a known issue related to template keys, but the root cause remains unclear due to insufficient documentation on the key creation process.

 - Verification of test keys received from Tazama works correctly using the auth-lib.

 - Manually created template keys do not work, despite appearing structurally correct.

 - No formal documentation currently exists that explains how template keys should be generated, what claims they should include, or what signing logic is required.

**Statement of Problem**

"There is an issue related to template keys, but it is unclear whether the problem is with key verification or key creation."

"Ability to test template key functionality is critical to resolving this issue."

This indicates that both areas — key creation and key verification — are potentially at fault.

**Findings So Far**

 - Keys received from Tazama validate correctly using validateTokenAndClaims.
 - Keys created manually based on assumptions fail validation.
 - Lack of documentation makes it impossible to confirm if keys are being constructed correctly or verified using the right logic.

