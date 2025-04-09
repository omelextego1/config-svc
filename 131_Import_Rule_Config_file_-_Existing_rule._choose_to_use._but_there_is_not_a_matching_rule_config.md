## Story

As a **Rules analyst**,
I want to **import an existing Rule Config json file, there is an existing rule, but not an existing config file**,
so I can **import configurations from other deployments**

## Background

A detailed flow is available [here](https://github.com/lextego/projectmgt/blob/main/polly/config-svc/01-product/overview/10_import_rule_configuration.md)
In the third scenario, I want to be able to import a file, with the assumption that there is an existing rule but I choose to create new rule and config. This flow covers the ```Simple Import``` and ```Existing rule Process``` with ```Use Existing rule - Yes, No Existing rule config``` sub process

Rule match is based on ```name``` in Arango = ```text to left of @``` in imported file and ```desc```  in Arango = ```desc``` in imported file, and Rule Configuration based on the ```cfg``` in Arango = ```cfg``` in imported file and the ```ruleID``` to link to the Rule

Dependent on [Import_rule_config_-_existing_rule_but_choose_to_create_a_new_rule](https://github.com/lextego/projectmgt/issues/130)

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

## Definition of Done

- [ ] There is a check that the uploaded file is a valid JSON and does not contain malicious code
- [ ] Only people with the Privileges to Import Configuration files are able to Import
- [ ] I can import a file, that checks to see if a rule exists, and when a rule is found, I can use the existing rule but as there is no matching config, I can create a new configuration. Then the rule and rule config are available to edit. The rule config would be 1.0.0
- [ ] Automated tests to validate all the above
- [ ] updated sequence diagram

[Import_Rule_Config_file_-_Existing_rule,_choose_to_use,_but_there_is_not_a_matching_rule_config](https://github.com/lextego/projectmgt/issues/131)
