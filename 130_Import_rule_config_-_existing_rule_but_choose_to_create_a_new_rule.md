## Story

As a **Rules analyst**,
I want to **import an existing Rule Config json file, and although there is an existing rule, I elect to create a new rule and config file**,
so I can **import configurations from other deployments**

## Background

A detailed flow is available [here](https://github.com/lextego/projectmgt/blob/main/polly/config-svc/01-product/overview/10_import_rule_configuration.md)
In the second scenario, I want to be able to import a file, with the assumption that there is an existing rule but I choose to create new rule and config. (this flow covers the ```Simple Import``` and ```Existing rule Process``` with ```Use Existing rule - No``` sub process

Rule match is based on ```name``` in Arango = ```text to left of @``` in imported file and ```desc```  in Arango = ```desc``` in imported file, and Rule Configuration based on the ```cfg``` in Arango = ```cfg``` in imported file and the ```ruleID``` to link to the Rule

Dependent on [Import Rule Config File - no existing rule](https://github.com/lextego/projectmgt/issues/129)

When I am importing the option on screen should be:

- The rule name and description matches an existing rule, how would you like to proceed?

The buttons would be
1. Use existing rule
2. Create new rule and rule config (this story)
3. Cancel Import

With the colours for action being the same, with the Cancel Import being red.

If I select Create new rule and rule config, I should be asked:

- Is this version update a:

1. Major Change
2. Minor Change
3. Patch Change

The logic needs to consider the X.Y.Z of the version of the rule, and the change would be

1. X+1.0.0
2. X.Y+1.0
3. X.Y.Z+1

The rule configuration version would be 1.0.0

## Definition of Done

- [ ] There is a check that the uploaded file is a valid JSON and does not contain malicious code
- [ ] Only people with the Privileges to Import Configuration files are able to Import
- [ ] I can import a file, that checks to see if a rule exists, and when a rule is found, I can create a new rule (instead of using the existing rule). Then the rule and rule config are available to edit,
  - [ ] the rule number is incremented to the next highest number of the rule as per the choice
- [ ] Automated tests to validate all the above
- [ ] updated sequence diagram

[Import_rule_config_-_existing_rule_but_choose_to_create_a_new_rule](https://github.com/lextego/projectmgt/issues/130)
