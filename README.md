## 0. Install Eclipse Modelling Tools

You can follow these steps to have the environment work:
## 1. Install the following plugins
1. [xtext](https://www.eclipse.org/Xtext/download.html)
2. [xtend](https://www.eclipse.org/xtend/download.html)
3. [sirius](https://www.eclipse.org/sirius/download.html)

## 2. Download the repository into your workspace
You should see the following packages 
1. mde.iot.ucm4iot 
2. mde.iot.ucm4iot.dsl 
3. mde.iot.ucm4iot.dsl.ide 
4. mde.iot.ucm4iot.tests
5. mde.iot.ucm4iot.ui
6. mde.iot.ucm4iot.ui.tests

## 3. Right-click on any of the above packages and click on Run As >> Eclipse Application

## 4. A new Eclipse Window should open running the UCM4IoT environment
You can tell if the eclipse application is running if you see a tab called UCM4IoT on the toolbar.
1. Click on *UCM4IoT >> Instantiate UCM4IoT File*

## IMPORTANT - READ THIS
Due to how Eclipse works, it does not automatically register some folders from the listed packages above. Eclipse will throw error messages even though it can clearly see that the folders exists. Follow these steps to fix this problem.
1. Open the **Problems** window (Opened by defult, but you can open it from *Window >> Show View >> Problems* if you can't find it)
2. You'll see a list of errors, only look at the ones related to the src and xtend-gen folders (the others will resolve themselves)

The errors will look like the following:
- Project 'mde.iot.ucm4iot.dsl.ide' is missing required source folder: 'xtend-gen'	mde.iot.ucm4iot.dsl.ide		Build path	Build Path Problem
- Project 'mde.iot.ucm4iot.dsl.ui.tests' is missing required source folder: 'src'	mde.iot.ucm4iot.dsl.ui.tests		Build path	Build Path Problem
- Project 'mde.iot.ucm4iot.dsl.ui.tests' is missing required source folder: 'xtend-gen'	mde.iot.ucm4iot.dsl.ui.tests		Build path	Build Path Problem
- Project 'mde.iot.ucm4iot.dsl.ui' is missing required source folder: 'xtend-gen'	mde.iot.ucm4iot.dsl.ui		Build path	Build Path Problem

3. Right-click on one of those error messages. 
4. Select **Quick Fix**
5. In the window that pops up, select **Configure Build Path**
6. Select **Finish**
7. In the window that pops up, select **Apply and Close**
8. Repeat steps 3-7 for each error message.

## Note: in case you're still not able to run the environment
* Make sure the plugins are installed correctly
* Make sure that the packages have been added into your Eclipse workspace correctly

## Template:

```
/* Optional */
!Standard Mode: off

/* Optional */
!List Modes: 
	NORMAL::NormalModeName::default,
	RESTRICTED::RestrictedModeName, 
	EMERGENCY::EmergencyModeName, 
	DEGRADED::DegradedModeName

/* Optional */
!List Exceptions: 
	{HARDWARE_EXCEPTION::HardwareExceptionName},
	{SOFTWARE_EXCEPTION::SoftwareExceptionName},
	{NETWORK_EXCEPTION::NetworkExceptionName},
	{ENVIRONMENT_EXCEPTION::EnvironmentExceptionName},
	{HARDWARE_EXCEPTION::GlobalHardwareExceptionName::global},
	{SOFTWARE_EXCEPTION::GlobalSoftwareExceptionName::global},
	{NETWORK_EXCEPTION::GlobalNetworkExceptionName::global},
	{ENVIRONMENT_EXCEPTION::GlobalEnvironmentExceptionName::global}

/* Use Case Template */

use case: UseCaseName
scope:	  SystemName
level:	  SUMMARY
intention:     "insert intention text here."
multiplicity:  "insert multiplicity text here."
primary actor: HUMAN::ActorName::0..*
secondary actor: 
	PHYSICAL_ENTITY::PhysicalEntityActorName::1..1, 
	SOFTWARE::SoftwareActorName::*..*, 
	SENSOR::SensorActorName::1..10, 
	ACTUATOR::ActuatorActorName::1..10,
	TAG::TagActorName::1..10,
	READER::ReaderActorName::1..10
main success scenario:
	"Condition or Control Flow Step."
	1. "Interaction step between ActorName and System."
	2. [InvokedUseCase1] "Invocation step text."
	3. [InvokedUseCase2] "Invocation step text."
	4.^ "Internal step text."
	5.^ timeout:10ms  "Timeout step text."
	6.^ timeout:10s   "Timeout step text."
	7.^ timeout:10min "Timeout step text."
	8.^ timeout:10h   "Timeout step text."
	use case ends in: SUCCESS
extensions:
	alternative for (1-3):
		(1-3)a. "Interaction step between ActorName and System."
		use case ends in: SUCCESS
	alternative for (1-3):
		(1-3)b. "Interaction step between ActorName and System."
		use case ends in: FAILURE
	exception for 1:
		1a. {HARDWARE_EXCEPTION::HardwareExceptionName} ##
		use case continues at Step: 6
	exception for 1:
		1b. {SOFTWARE_EXCEPTION::SoftwareExceptionName} ##
		use case ends in: FAILURE

/* Invoked Use Cases */

use case: InvokedUseCase1
scope:	  SystemName
level:	  USER_GOAL
intention:     "insert intention text here."
multiplicity:  "insert multiplicity text here."
primary actor: HUMAN::ActorName::0..*
main success scenario:
	1. "Interaction step between ActorName and System."
	use case ends in: SUCCESS


use case: InvokedUseCase2
scope:	  SystemName
level:	  SUB_FUNCTION
intention:     "insert intention text here."
multiplicity:  "insert multiplicity text here."
primary actor: None
main success scenario:
	1. "Interaction step between ActorName and System."
	use case ends in: SUCCESS

/* Handler Use Cases */

handler use case: HandlerUseCaseName
scope:	  SystemName
level:	  USER_GOAL
intention:     "insert intention text here."
multiplicity:  "insert multiplicity text here."
primary actor: HUMAN::ActorName::0..*
contexts and exceptions:
	UseCaseName {HARDWARE_EXCEPTION::HardwareExceptionName},
	UseCaseName {SOFTWARE_EXCEPTION::SoftwareExceptionName}
main success scenario:
	1. "Interaction step between ActorName and System."
	use case ends in: SUCCESS
```
