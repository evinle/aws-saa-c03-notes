- AWS::CloudFormation::Init
- Complex bootstrapping 
- cfn-init helper script - installed on EC2 OS
- Simple configuration management system
- Procedural (User Data) vs Desired State (cfn-init)
- Packages, Groups, Users, Sources, Files, Commands and Services
- Provided with directives via Metadata and AWS::CloudFormation::Init on a CFN resource

- Executed from the UserData passed into that instance
- Can watch for changes in the template's metadata and run again
	- UserData can't do this
	- ![[Pasted image 20261016225546.png]]

- Creation Policy
	- Logical Resource
	- CFN waits for cfn-signal from the EC2
	- -e $? (state of the previous command) - can report errors as well
	- ![[Pasted image 20261016225943.png]]