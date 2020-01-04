# Permissions
A new, role-based access control tool in Node.JS.

## Current Status
This project is still in the initial design phase

## Design Goals
A comprehensive access control tool, similar to Onur Yıldırım's [accesscontrol](https://www.npmjs.com/package/accesscontrol) tool that strives to be a little more flexible and easier to use.

Towards this goal, we have several requirements:
- Query permissions with chainable, easy-to-use commands
- Manage permissions easily with rules loaded from a file or changed dynamically in code
- Determine roles automatically from a user's profile or account
- Determine resource ownership automatically
- Customize user and resource processing easily
- Filter JSON resources based on permissions
- Filter/Reject changes when creating/updating/deleting resources

A basic permissions query should look something like this:
```javascript
const user = {
    uid: 'user-01',
    name: 'James Tanner',
    roles: ['Developer']
};
const resource = {
    type: 'Secret',
    owner: 'user-01',
    secretCode: 'correct horse battery staple'
};
const userAllowedTo = permissions.can(user).read(resource);
```

## Implementation
In order to determine permissions, we need the answer to several questions:
- Who is making the request? (Roles)
- What resource are they accessing? (Resource)
- Do they own it? (Ownership)
- What do they want to do with it? (Action)
- Which properties are they allowed to access? (Filtering)

Grants and configuration are pre-defined.

A query needs to include the following information, which can then be extrapolated into the necessary answers:
- User
    - Parse Roles
- Action
- Resource
    - Parse Ownership
