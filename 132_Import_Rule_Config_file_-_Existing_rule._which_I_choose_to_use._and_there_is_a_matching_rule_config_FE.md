## Story

As a **Rules analyst**,
I want to **import an existing Rule Config json file, there is an existing rule, and an existing config file**,
so I can **import configurations from other deployments**

## Background

A detailed flow is available [here](https://github.com/lextego/projectmgt/blob/main/polly/config-svc/01-product/overview/10_import_rule_configuration.md)
In the fourth scenario, I want to be able to import a file, with the assumption that there is an existing rule, I want to use the existing rule and then check to see if the existing config matches, as they match I am given an option to keep the existing rule config, or create a new version. This flow covers the ```Simple Import``` and ```Existing rule Process``` with ```Use Existing rule - Yes, Existing rule config``` sub process and ```Existing Rule and Rule Config``` sub process

Rule match is based on ```name``` in Arango = ```text to left of @``` in imported file and ```desc```  in Arango = ```desc``` in imported file, and Rule Configuration based on the ```cfg``` in Arango = ```cfg``` in imported file and the ```ruleID``` to link to the Rule

Dependent on [Import_Rule_Config_file_-_Existing_rule,_choose_to_use,_but_there_is_not_a_matching_rule_config](https://github.com/lextego/projectmgt/issues/131)

When I am importing the option on screen should be:

- The rule name and description matches an existing rule, how would you like to proceed?

The buttons would be

1. Use existing rule? (this story)
2. Create new rule and rule config?
3. Cancel Import

With the colours for action being the same, with the Cancel Import being red.

You would then be presented with an update that there is not an existing rule configuraiton

- There is not an existing rule configuration would you like to:

1. Create new rule configuration? (this story)
2. Cancel Import

If you select create new rule configuration, you will be asked

- Is this rule configuration version update a:

1. Major Change
2. Minor Change
3. Patch Change

The logic needs to consider the X.Y.Z of the version of the rule configuration, and the change would be

1. X+1.0.0
2. X.Y+1.0
3. X.Y.Z+1

## Definition of Done

- [ ] There is a check that the uploaded file is a valid JSON and does not contain malicious code
- [ ] Only people with the Privileges to Import Configuration files are able to Import
- [ ] I can import a file, that checks to see if a rule exists, and when a rule is found, it checks to see if there is a rule config available to edit.
  - [ ] I can choose to use the existing rule config, or
  - [ ] the rule configuration version is incremented to the next highest number of the rule configuration as per the choice
- [ ] Automated tests to validate all the above
- [ ] updated sequence diagram

[Import_Rule_Config_file_-_Existing_rule,_choose_to_use,_and_there_is_a_matching_rule_config](https://github.com/lextego/projectmgt/issues/132)
