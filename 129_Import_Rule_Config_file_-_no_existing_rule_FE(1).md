## Story

As a **Rules analyst**,
I want to **import an existing Rule Config json file**,
so I can **import configurations from other deployments**

## Background

A detailed flow is available [here](https://github.com/lextego/projectmgt/blob/main/polly/config-svc/01-product/overview/10_import_rule_configuration.md)
In the first scenario, I want to be able to import a file, with the assumption that there is not an existing rule or config. This flow covers the ```Simple Import``` and ```No existing rule Process```

Rule match is based on ```name``` in Arango = text to left of @ in ```id``` in imported file and ```desc```  in Arango = ```desc``` in imported file, and Rule Configuration based on the ```cfg``` in Arango = ```cfg``` in imported file and the ```ruleID``` to link to the Rule

After the check the user is updated:
- There is no existing rule would you like to create a new rule
Options
- Yes - Create new rule
- No - Cancel Import

## Definition of Done

- [ ] There is a check that the uploaded file is a valid JSON and does not contain malicious code
- [ ] Only people with the Privileges to Import Configuration files are able to Import
- [ ] I can import a file, that checks to see if a rule exists, and when no rule is found, the user is asked how they wish to proceed
  - [ ] if proceed the rule and rule config are available to edit and the rule and config are in the state of "Draft"
  - [ ] The created by is from the logged in user
  - [ ] The date and time is set to when the import is accepted
- [ ] Automated tests to validate all the above
- [ ] Updated Roles and Privileges Document

[Import Rule Config file - no existing rule](https://github.com/lextego/projectmgt/issues/129)
