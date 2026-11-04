# Chat Application — Software Requirements Specification (SRS)

## 1. Introduction

### 1.1 Purpose

This document defines the functional and non-functional requirements for the Chat Application's Minimum Viable Product (MVP).

It provides a specification for system design, implementation, and software testing.

Requirements are derived from the Chat Application Customer Policy.

### 1.2 Product Scope

The Chat Application is a browser-based communication platform that allows registered users to exchange private text messages.

*The MVP will provide:*
- User registration and authentication.
- User profiles.
- User discovery through username search.
- One-to-one text messaging.
- Persistent conversation history.
- Access control for private conversations.

## 2. Overall Description

### 2.1 Product Overview

The Chat Application allows users to create accounts, discover other users, initiate direct conversations, and exchange text messages.

Each pair of users may share only one direct conversation.

Conversations are created upon sending the first message and remain accessible to both participants through their conversation lists.

Only participants may access the messages belonging to their conversations.

### 2.2 Assumptions and Dependencies

*The following are preliminary assumptions requiring confirmation:*
- Users have access to a supported web browser and internet connection.
- Users provide an email address, username, and password during registration.
- Users must authenticate before accessing their account, searching for users, or messaging.
- Messages are stored persistently so conversation history can be retrieved across sessions.
- The initial release supports only one-to-one conversations.

## 3. Functional Requirements

Functional requirements describe the specific behaviours the system must provide.

Each requirement has a unique identifier and references its originating customer policy.

### 3.1 Account Management

| ID | Requirement | Source | Description|
| -- | ------------| ------ | ---------- | 
|FR-01|User Registration|CP-01|The system shall allow users to register an account by providing a username, email address, and password.|
|FR-02|Unique Email Address|CP-02|The system shall prevent the registration of multiple accounts associated with the same email address.|
|FR-03|Unique Username|CP-03|The system shall prevent the registration of multiple accounts with the same username.|
|FR-04|User Authentication|CP-04|The system shall allow registered users to authenticate using valid account credentials and establish an authenticated session.|
|FR-05|Invalid Login Handling|CP-04|The system shall reject authentication attempts when invalid credentials are provided.|
|FR-06|User Logout|CP-05, CP-09|The system shall allow authenticated users to sign out and invalidate their current authenticated session.|

### 3.2 User Profiles

| ID | Requirement | Source | Description |
|---|---|---|---|
| FR-07 | Default Profile Icon | [CP-06](./01-client-policy.md) | The system shall assign a default profile icon displaying the user's initials when an account is created. |
| FR-08 | Profile Navigation | [CP-07](./01-client-policy.md) | The system shall allow authenticated users to access their profile page by selecting their profile icon. |
| FR-09 | Profile Information | [CP-08](./01-client-policy.md) | The system shall display the user's username, profile icon, and account creation date on their profile page. |
| FR-10 | Profile Logout | [CP-09](./01-client-policy.md) | The system shall provide a sign-out option on the authenticated user's own profile page. |

### 3.3 User Discovery

| ID | Requirement | Source | Description |
|---|---|---|---|
| FR-11 | Username Search | [CP-11](./01-client-policy.md) | The system shall allow authenticated users to search for other registered users by username. |
| FR-12 | Search Results | [CP-11](./01-client-policy.md) | The system shall display matching users in the search results and allow the searching user to access their profiles. |
| FR-13 | Initiate Direct Messaging | [CP-10](./01-client-policy.md), [CP-12](./01-client-policy.md) | The system shall allow authenticated users to open a direct messaging interface from another user's profile. If a conversation already exists between the two users, the system shall display its message history. |

### 3.4 Conversation Management

| ID | Requirement | Source | Description |
|---|---|---|---|
| FR-14 | Conversation List | [CP-14](./01-client-policy.md) | The system shall display all existing conversations in which the authenticated user is a participant. |
| FR-15 | Conversation Creation | [CP-15](./01-client-policy.md) | When a user sends a message to another user for the first time, the system shall create a conversation if one does not already exist between them. Opening a messaging interface without sending a message shall not create a conversation. |
| FR-16 | Conversation Uniqueness | [CP-16](./01-client-policy.md) | The system shall prevent the creation of multiple one-to-one conversations between the same pair of users. |
| FR-17 | Existing Conversation Reuse | [CP-15](./01-client-policy.md), [CP-16](./01-client-policy.md) | When a message is sent between two users who already share a conversation, the system shall associate the new message with that existing conversation. |

### 3.5 Text Messaging

| ID | Requirement | Source | Description |
|---|---|---|---|
| FR-18 | Send Text Messages | [CP-13](./01-client-policy.md), [CP-17](./01-client-policy.md) | The system shall allow participants to send text messages within their conversations. |
| FR-19 | Message Validation | [CP-13](./01-client-policy.md), [CP-17](./01-client-policy.md) | The system shall reject messages that contain no non-whitespace text content. |
| FR-20 | Message Persistence | [CP-18](./01-client-policy.md) | The system shall persist successfully sent messages so they remain available for future retrieval. |
| FR-21 | Conversation History | [CP-18](./01-client-policy.md) | The system shall allow conversation participants to retrieve previously sent messages. Messages shall be displayed in chronological order. |

### 3.6 Authorization and Access Control

| ID | Requirement | Source | Description |
|---|---|---|---|
| FR-22 | Conversation Access Control | [CP-19](./01-client-policy.md), [C-02](./01-client-policy.md) | The system shall verify that an authenticated user is a participant in a conversation before allowing access to its message history. |
| FR-23 | Message Authorization | [CP-17](./01-client-policy.md), [CP-19](./01-client-policy.md), [C-02](./01-client-policy.md) | The system shall prevent users from sending messages to existing conversations in which they are not participants. |
| FR-24 | Unauthorized Access Handling | [CP-19](./01-client-policy.md), [C-02](./01-client-policy.md) | The system shall reject unauthorized requests for conversation information without exposing private message contents. |

## 4. Non-Functional Requirements

Non-functional requirements describe the system's quality attributes and operational expectations.

### 4.1 Security

| ID | Requirement | Source | Description |
|---|---|---|---|
| NFR-01 | Password Protection | [C-02](./01-client-policy.md) | The system shall store passwords using an established password-hashing algorithm suitable for password storage. Plaintext passwords shall not be stored. |
| NFR-02 | Secure Communication | [C-02](./01-client-policy.md) | The system shall protect authenticated client-server communication using HTTPS in deployed environments. |
| NFR-03 | Access Control | [CP-19](./01-client-policy.md), [C-02](./01-client-policy.md) | The system shall enforce conversation authorization independently of client-side interface restrictions. |

### 4.2 Performance

| ID | Requirement | Source | Description |
|---|---|---|---|
| NFR-04 | Application Responsiveness | Proposed engineering quality requirement | The application should provide responsive interaction during normal usage. Specific response-time targets, expected concurrent-user counts, and the conditions under which performance will be measured remain to be defined. |

### 4.3 Accessibility and Usability

| ID | Requirement | Source | Description |
|---|---|---|---|
| NFR-05 | Accessible Interface | [C-03](./01-client-policy.md) | The application shall support keyboard navigation and provide accessible labels for interactive controls. The specific accessibility standard and conformance level remain to be confirmed. |
| NFR-06 | Responsive Layout | [C-03](./01-client-policy.md) | The application shall provide a usable layout on supported mobile and desktop screen sizes. |

### 4.4 Browser Compatibility

| ID | Requirement | Source | Description |
|---|---|---|---|
| NFR-07 | Browser Support | [C-01](./01-client-policy.md) | The application shall function on supported modern web browsers. The exact browser versions and compatibility testing matrix remain to be determined. |

### 4.5 Maintainability

| ID | Requirement | Source | Description |
|---|---|---|---|
| NFR-08 | Maintainable System Design | Proposed engineering quality requirement | The application shall be organized into components or modules with defined responsibilities. Changes to individual modules should minimize unnecessary effects on unrelated functionality. The architecture and associated validation practices will be documented during system design. |

## 5. System Constraints

The following constraints originate from the [Chat Application Customer Policy](./01-client-policy.md).

| ID | Constraint | Source |
|---|---|---|
| SC-01 | The application must operate through modern web browsers. | [C-01](./01-client-policy.md) |
| SC-02 | The application must protect user account information and private conversations. | [C-02](./01-client-policy.md) |
| SC-03 | The application must provide an accessible and mobile-friendly user interface. | [C-03](./01-client-policy.md) |
| SC-04 | The MVP shall support text messaging only. | [CP-13](./01-client-policy.md) |
| SC-05 | The MVP shall support one-to-one conversations only. | [CP-15](./01-client-policy.md), [CP-16](./01-client-policy.md) |

## 6. Acceptance Criteria

Acceptance criteria define observable conditions used to verify whether the requirements have been satisfied.

The following criteria cover representative MVP behaviours.

### 6.1 AC-01: User Registration

Related requirements: FR-01, FR-02, FR-03

- Given valid registration information containing an unused email and username, when a user submits the registration form, then an account is created.

- Given an email address already associated with an account, when registration is attempted, then the system rejects the request.

- Given a username already in use, when registration is attempted, then the system rejects the request.

### 6.2 AC-02: Authentication

Related requirements: FR-04, FR-05, FR-06

- Given valid account credentials, when a user signs in, then an authenticated session is established.

- Given invalid credentials, when a user attempts to sign in, then access is denied.

- Given an authenticated session, when the user signs out, then that session can no longer be used to access protected resources.

### 6.3 AC-03: Profile Information

Related requirements: FR-07, FR-08, FR-09, FR-10

- Given a newly registered user, when their profile is viewed, then a default icon displaying their initials is present.

- Given a user profile, when it is opened, then the username, icon, and date joined are visible.

- Given the authenticated user's own profile, when it is opened, then a sign-out option is available.

### 6.4 AC-04: User Discovery

Related requirements: FR-11, FR-12, FR-13

- Given an existing registered username, when a user searches for it, then the matching user can be found.

- Given a matching search result, when it is selected, then the corresponding user's profile can be opened.

- Given another user's profile, when the chat icon is selected, then the direct messaging interface is displayed.

### 6.5 AC-05: Conversation Creation

Related requirements: FR-15, FR-16, FR-17

- Given two users without an existing conversation, when one sends the first valid message, then one conversation is created.

- Given two users with an existing conversation, when another message is sent, then the existing conversation is reused.

- Given a user who opens a chat interface but does not send a message, then no new conversation is created.

- Given two users sending their first messages concurrently, the system shall still maintain only one shared conversation.

### 6.6 AC-06: Text Messaging

Related requirements: FR-18, FR-19, FR-20, FR-21

- Given a valid text message from a participant, when it is submitted, then it is saved and becomes available in the conversation.

- Given an empty or whitespace-only message, when it is submitted, then the system rejects it without saving a message.

- Given an existing conversation with stored messages, when a participant opens it, then the message history is displayed in chronological order.

### 6.7 AC-07: Conversation Privacy

Related requirements: FR-22, FR-23, FR-24

- Given an authenticated conversation participant, when they request their conversation history, then the system allows access.

- Given an authenticated user who is not a participant, when they request that conversation's messages, then access is denied without disclosing message contents.

- Given a user who is not a participant, when they attempt to send a message through that existing conversation, then the system rejects the operation.
