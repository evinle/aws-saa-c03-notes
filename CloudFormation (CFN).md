-  infrastructure as Code (IaC)
- Defined by templates
	- Lets to manage resources with a declarative template
	- Create, Update and Delete 
- Basically Terraform but AWS only
- Can either be in YML or JSON

## Template makeup
- Has list of `Resources`, at least 1
	- Only mandatory part 
- Description
	- Immediately follows AWSTemplateFormatVersion (if there's any)
- Metadata: controls the Console UI
- Parameters: define dropdown options
- Mappings: lookup tables
- Conditions: decision making, things only occur when a condition is met
	- ![[Pasted image 20260411185417.png]]
- Outputs: what is returned after the task

## How it works
- The list of resources inside `Resources` is referred to as "Logical Resources"
- When you you apply a template, it will create/update the stack, which is the living representation of that template
- The stack then applies the changes to the physical resources on AWS
- ![[Pasted image 20260411185824.png]]
- ![[Pasted image 20260411185940.png]]
- Automate Infrastructure
	- Can also be used in change management
