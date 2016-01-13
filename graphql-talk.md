footer: Ember London *@arkham*

# [fit] No *REST* for the Wicked

---

## A gentle introduction to GraphQL

---

* I'm Ju 🙇🏻
* I work for [AlphaSights](engineering.alphasights.com)
* We build ambitious apps in Ruby & Ember

---

## What's this GraphQL thing?

---

* A **Graph** **Q**uery **L**anguage
* Invented by Facebook in 2012, now made open
* Powers most of the Facebook iOS and Android apps

---

# A simple example

---

We have a `users` table like this one

```
+----+------+---------------+-----+-----------+
| id | name |    twitter    | age |  country  |
+----+------+---------------+-----+-----------+
|  1 | Ju   | arkh4m        |  29 | Italy     |
|  2 | Will | willrax       | 268 | Australia |
|  3 | Matz | yukihiro_matz |  50 | Japan     |
+----+------+---------------+-----+-----------+
```

---

# Get all users - Query string

```
{
  users {
    id,
    name
  }
}
```

---

# Get all users - JSON response

```
{
  "data": {
    "users": [
      { "id": "1", "name": "Ju" },
      { "id": "2", "name": "Will" },
      { "id": "3", "name": "Matz" }
    ]
  }
}
```

---

# Get one user - Query string

```
{
  user(id: 1) {
    id,
    name
  }
}
```

---

# Get one user - JSON response

```
{
  "data": {
    "user": {
      "id": "1",
      "name": "Ju"
    }
  }
}
```

---

# Create a user - Query string

```
mutation {
  createUser(
    name: "Tom",
    twitter: "tomdale",
    country: "USA"
  ) {
    id,
    name
  }
}
```

---

# Create a user - JSON response

```
{
  "data": {
    "user": {
      "id": "4",
      "name": "Tom"
    }
  }
}
```

---

Now imagine we have a `company` table like this one

```
+----+-------------+---------------+
| id |    name     |     city      |
+----+-------------+---------------+
|  1 | AlphaSights | London        |
|  2 | Heroku      | San Francisco |
+----+-------------+---------------+
```

---

And we add a `company_id` to each user

```
+----+------+---------------+-----+-----------+------------+
| id | name |    twitter    | age |  country  | company_id |
+----+------+---------------+-----+-----------+------------+
|  1 | Ju   | arkham        |  29 | Italy     |          1 |
|  2 | Will | willrax       | 268 | Australia |          1 |
|  3 | Matz | yukihiro_matz |  50 | Japan     |          2 |
+----+------+---------------+-----+-----------+------------+
```

---

# Relationships - Query string

```
{
  user(id: 1) {
    id,
    name,
    company {
      name
    }
  }
}
```

---

# Relationships - JSON response

```
{
  "data": {
    "user": {
      "id": "1",
      "name": "Ju",
      "company": {
        "name": "AlphaSights"
      }
    }
  }
}
```

---

# But why???

---

* Hierarchical
* Product-centric
* Client-specifies queries
* Backwards Compatible
* Structured, Arbitrary Code
* Application-Layer Protocol
* Strongly-typed
* Introspective

---

![autoplay](https://www.youtube.com/watch?v=e8xUObI32es)

---

## No REST for the wicked

---

# REST request

```
GET /users/1
```

---

# REST response

```
???
```

---

# [fit] What You See Is What You Get

---

# GraphQL request

```
{
  user(id: 1) { id, name }
}
```

---

# GraphQL response

```
{
  "data": {
    "user": { "id": "1", "name": "Ju" }
  }
}
```

---

# [fit] Every GraphQL query is a contract

---

# [fit] Every GraphQL query is
# [fit] a *frontend-driven* contract

---

# [fit] SOL*I*D

---

# [fit] Interface Segregation Principle

---

* Clients should not be forced to depend on methods that they do not use.

---

* Clients should not be forced to depend on methods that they do not use.
* Many client specific interfaces are better than one general purpose interface.

---

* Clients should not be forced to depend on methods that they do not use.
* Many client specific interfaces are better than one general purpose interface.
* The dependency of one class to another one should depend on the smallest possible interface.

---

* Clients should not be forced to depend on methods that they do not use.
* Many client specific interfaces are better than one general purpose interface.
* The dependency of one class to another one should depend on the smallest possible interface.
* Make fine grained interfaces that are client specific.

---

## REST request

---

```
POST /users/

{
  "name": "Hello-World",
  "description": "This is your first example",
  "homepage": "https://example.com",
  "private": false,
  "has_issues": true,
  "has_wiki": true,
  "has_downloads": true
}
```

---

## REST response

```
{
  "id": 1296269,
  "owner": {
    "login": "octocat",
    "id": 1,
    "avatar_url": "https://example.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "url": "https://api.example.com/users/octocat",
    "html_url": "https://example.com/octocat",
    "followers_url": "https://api.example.com/users/octocat/followers",
    "following_url": "https://api.example.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.example.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.example.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.example.com/users/octocat/subscriptions",
    "organizations_url": "https://api.example.com/users/octocat/orgs",
    "repos_url": "https://api.example.com/users/octocat/repos",
    "events_url": "https://api.example.com/users/octocat/events{/privacy}",
    "received_events_url": "https://api.example.com/users/octocat/received_events",
    "type": "User",
    "site_admin": false
  },
  "name": "Hello-World",
  "full_name": "octocat/Hello-World",
  "description": "This your first repo!",
  "private": false,
  "fork": true,
  "url": "https://api.example.com/repos/octocat/Hello-World",
  "html_url": "https://example.com/octocat/Hello-World",
  "archive_url": "http://api.example.com/repos/octocat/Hello-World/{archive_format}{/ref}",
  "assignees_url": "http://api.example.com/repos/octocat/Hello-World/assignees{/user}",
  "blobs_url": "http://api.example.com/repos/octocat/Hello-World/git/blobs{/sha}",
  "branches_url": "http://api.example.com/repos/octocat/Hello-World/branches{/branch}",
  "clone_url": "https://example.com/octocat/Hello-World.git",
  "collaborators_url": "http://api.example.com/repos/octocat/Hello-World/collaborators{/collaborator}",
  "comments_url": "http://api.example.com/repos/octocat/Hello-World/comments{/number}",
  "commits_url": "http://api.example.com/repos/octocat/Hello-World/commits{/sha}",
  "compare_url": "http://api.example.com/repos/octocat/Hello-World/compare/{base}...{head}",
  "contents_url": "http://api.example.com/repos/octocat/Hello-World/contents/{+path}",
  "contributors_url": "http://api.example.com/repos/octocat/Hello-World/contributors",
  "downloads_url": "http://api.example.com/repos/octocat/Hello-World/downloads",
  "events_url": "http://api.example.com/repos/octocat/Hello-World/events",
  "forks_url": "http://api.example.com/repos/octocat/Hello-World/forks",
  "git_commits_url": "http://api.example.com/repos/octocat/Hello-World/git/commits{/sha}",
  "git_refs_url": "http://api.example.com/repos/octocat/Hello-World/git/refs{/sha}",
  "git_tags_url": "http://api.example.com/repos/octocat/Hello-World/git/tags{/sha}",
  "git_url": "git:example.com/octocat/Hello-World.git",
  "hooks_url": "http://api.example.com/repos/octocat/Hello-World/hooks",
  "issue_comment_url": "http://api.example.com/repos/octocat/Hello-World/issues/comments{/number}",
  "issue_events_url": "http://api.example.com/repos/octocat/Hello-World/issues/events{/number}",
  "issues_url": "http://api.example.com/repos/octocat/Hello-World/issues{/number}",
  "keys_url": "http://api.example.com/repos/octocat/Hello-World/keys{/key_id}",
  "labels_url": "http://api.example.com/repos/octocat/Hello-World/labels{/name}",
  "languages_url": "http://api.example.com/repos/octocat/Hello-World/languages",
  "merges_url": "http://api.example.com/repos/octocat/Hello-World/merges",
  "milestones_url": "http://api.example.com/repos/octocat/Hello-World/milestones{/number}",
  "mirror_url": "git:git.example.com/octocat/Hello-World",
  "notifications_url": "http://api.example.com/repos/octocat/Hello-World/notifications{?since, all, participating}",
  "pulls_url": "http://api.example.com/repos/octocat/Hello-World/pulls{/number}",
  "releases_url": "http://api.example.com/repos/octocat/Hello-World/releases{/id}",
  "ssh_url": "git@example.com:octocat/Hello-World.git",
  "stargazers_url": "http://api.example.com/repos/octocat/Hello-World/stargazers",
  "statuses_url": "http://api.example.com/repos/octocat/Hello-World/statuses/{sha}",
  "subscribers_url": "http://api.example.com/repos/octocat/Hello-World/subscribers",
  "subscription_url": "http://api.example.com/repos/octocat/Hello-World/subscription",
  "svn_url": "https://svn.example.com/octocat/Hello-World",
  "tags_url": "http://api.example.com/repos/octocat/Hello-World/tags",
  "teams_url": "http://api.example.com/repos/octocat/Hello-World/teams",
  "trees_url": "http://api.example.com/repos/octocat/Hello-World/git/trees{/sha}",
  "homepage": "https://example.com",
  "language": null,
  "forks_count": 9,
  "stargazers_count": 80,
  "watchers_count": 80,
  "size": 108,
  "default_branch": "master",
  "open_issues_count": 0,
  "has_issues": true,
  "has_wiki": true,
  "has_pages": false,
  "has_downloads": true,
  "pushed_at": "2011-01-26T19:06:43Z",
  "created_at": "2011-01-26T19:01:12Z",
  "updated_at": "2011-01-26T19:14:43Z",
  "permissions": {
    "admin": false,
    "push": false,
    "pull": true
  }
}
```

---

![](./images/bilbo-rest-isp.jpg)

---

## GraphQL request

---

```
mutation {
  createRepo(
    name: "Hello-World",
    description: "This is your first example",
    homepage: "https://example.com",
    private: false,
    has_issues: true,
    has_wiki: true,
    has_downloads: true
  ) {
    id
    name
    clone_url
    user: owner {
      avatar_url
    }
  }
}
```

---

## GraphQL response

---

```
{
  "data": {
    repo: {
      "id": 1296269,
      "name": "Hello-World",
      "clone_url": "https://example.com/octocat/Hello-World.git",
      "user": {
        "avatar_url": "https://example.com/images/error/octocat_happy.gif",
      }
    }
  }
}
```

---

# [fit] Hmm, okay.. But can I use it in Ember?

---

# [fit] YES
# [fit] github.com/alphasights/ember-graphql-adapter

---

# Adapter

```js
import GraphQLAdapter from 'ember-graphql-adapter';

export default GraphQLAdapter.extend({
  endpoint: `${EmberENV.apiBaseUrl}/graph`
});
```

---

# Serializer

```js
import { Serializer } from 'ember-graphql-adapter';

export default Serializer.extend({});
```

---

# Rails

[github.com/rmosolgo/graphql-ruby](https://github.com/rmosolgo/graphql-ruby)

---

# [fit] Ember Data is amazing

---

# [fit] You can just replace *one* resource

---

# [fit] You have no excuses, go and try *GraphQL*!

---

# Thanks! Questions?

* Ju Liu [@arkham](https://twitter.com/arkh4m)
* [engineering.alphasights.com](https://engineering.alphasights.com)
* [github.com/alphasights/ember-graphql-adapter](https://github.com/alphasights/ember-graphql-adapter)

---

# Extras

--- 

# Field aliases - Query string

```
{
  user(id: 1) {
    id,
    name,
    age_in_years: age
  }
}
```

---

# Field aliases - Query string

```
{
  "data": {
    "user": {
      "id": "1",
      "name": "Ju",
      "age_in_years": "29"
    }
  }
}
```

---

# References

* [https://learngraphql.com](https://learngraphql.com)
* [https://facebook.github.io/react/blog/2015/05/01/graphql-introduction.html](https://facebook.github.io/react/blog/2015/05/01/graphql-introduction.html)

