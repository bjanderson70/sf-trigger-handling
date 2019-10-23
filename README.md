# sf-trigger-handling
First and foremost, **THIS IS NOT A TRIGGER FRAMEWORK**.

The goal is to provide the ability to instantiate various trigger handlers (i.e., classes) at run time (control order,handle exceptions and provide perf metrics). **Before you can load and use the trigger handling you **MUST** install the  [sf-cross-cutting concerns](https://github.com/bjanderson70/sf-cross-cutting-concerns).**

## Overview

Let us take an example. Lets say you have various functionality performed on trigger actions (before/after) related to the **Account**. Let us also say, you have a single-point of entry into the Account Trigger which invokes the Account Domain (i.e. FFLIB, SFDC Trigger Framework, etc.). Once you are inside the Account Domain that handles the various actions, you find over time you new updates, or multiple development groups are adding new functionality. This is where this framework comes into play. Instead of multiple entities making changes to  one class or creating multiple instantiations in various Before/After events, why not allow a developer (or team) develop there functionality in isolation and then wire them together in a Test, Debug or Production environment, such that, they behave as ONE. In addition, why not allow you to control the order of execution, continuation on exceptions or not, and provide performance information. This framework brings all these aspects to fluition.

Thus, when a trigger fires on an event those individual classes will be instantiated and called serially. For example, lets say I have three groups (mutually exclusive of context) creating functionality around the Account Object. Team 1, defines a class, **AccountBillingHandler**, Team 2, defines a class **AccountNotificationHandler**, Team 3, defines a class **AccountUpdateHandler**. Within the **SAME** teams could develop and test this functionality without stepping on each others work; and when tested, can be setup to call handlers, like **AccountBillingHandler,AccountUpdateHandler,AccountNotificationHandler** or **AccountUpdateHandler,AccountBillingHandler,AccountNotificationHandler**; any order you choose. Furthermore, a **TRIGGER DOES NOT** have to exists to test.

The basic design works on the premise of a Base class which defines the Before/After events ( which you inherit from an override as needed), and hidden from the developer is the fact these classes are apart of **Chain of Responsibility** controlled by a **Mediator**.

![HighLevel View](https://github.com/bjanderson70/sf-trigger-handling/blob/master/imgs/th_highlevel.png)

![HighLevel Flow](https://github.com/bjanderson70/sf-trigger-handling/blob/master/imgs/th_flow.png)

## Getting Started

These instructions will provide you information of the project and running on your local machine for development and as well as the testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

You **MUST** install the  [sf-cross-cutting concerns](https://github.com/bjanderson70/sf-cross-cutting-concerns) otherwise, it WILL NOT install.

## Running the tests

The unit tests should have an overall minimum of 90% code coverage. Tests can be invoked from favortite case tool.
In Salesforce Org, navigate to **Setup->Apex Classes** and run all tests.

## Versioning

version 1.0.0.0

## Authors

* **Bill Anderson** 

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details

## Deploy

<a href="https://githubsfdeploy.herokuapp.com">
  <img alt="Deploy to Salesforce"
       src="https://raw.githubusercontent.com/afawcett/githubsfdeploy/master/deploy.png">
</a>

## Quick Start

See the [Wiki](https://github.com/bjanderson70/sf-trigger-handling/wiki)
 
## Acknowledgments
