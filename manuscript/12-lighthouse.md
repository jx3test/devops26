https://jenkins-x.io/docs/reference/components/lighthouse/

## Exploring The Basic Pull Request Process Through ChatOps

When we issued the command /assign, and since we were not specific, lighthouse made a decision who should it be assigned to.

We need to define who is allowed to review and who can approve our pull requests. We can do that by modifying the OWNERS file generated when we created the project through the Jenkins X quickstart. Since it would be insecure to allow a person who made the PR to change that file, the one that counts is the OWNERS file in the master branch. So, that''s the one we'll explore and modify.

## Exploring Additional Slash Commands

```bash
git checkout master
git pull
git checkout -b my-pr
```

Size labels are applied based on the total number of changed lines.

At this moment, you might wonder whether it is more efficient to create comments with slash commands that add labels, instead of merely creating them directly. It is not. We could just as easily create a label using GitHub console.



## How Do We Know Which Slash Commands Are Available?

https://github.com/jenkins-x/lighthouse/tree/master/pkg/plugins

`git clone https://github.com/jenkins-x/lighthouse`

`ls -l lighthouse/pkg/plugins`

The list of lighthouse plugins and their configuration is stored in ConfigMap plugins. Let's describe it and see what we'll get.

`kubectl --namespace jx describe cm plugins`

```yaml
...
plugins.yaml:
----
...
plugins:
  ...
  jx3test/api-gateway-mock:
  - approve
  - assign
  - blunderbuss
  - help
  - hold
  - lgtm
  - lifecycle
  - override
  - size
  - trigger
  - wip
  - heart
  - cat
  - dog
  - pony
...
```

We already used many of the available plugins (e.g., approve). 

Feel free to explore the plugins we're using through the [Prow Plugin Catalog](https://prow.k8s.io/plugins[) documentation.

