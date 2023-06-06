<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo-small.svg" width="200" alt="Nest Logo" /></a>
</p>

[circleci-image]: https://img.shields.io/circleci/build/github/nestjs/nest/master?token=abc123def456
[circleci-url]: https://circleci.com/gh/nestjs/nest

  <p align="center">A progressive <a href="http://nodejs.org" target="_blank">Node.js</a> framework for building efficient and scalable server-side applications.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/v/@nestjs/core.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/l/@nestjs/core.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/dm/@nestjs/common.svg" alt="NPM Downloads" /></a>
<a href="https://circleci.com/gh/nestjs/nest" target="_blank"><img src="https://img.shields.io/circleci/build/github/nestjs/nest/master" alt="CircleCI" /></a>
<a href="https://coveralls.io/github/nestjs/nest?branch=master" target="_blank"><img src="https://coveralls.io/repos/github/nestjs/nest/badge.svg?branch=master#9" alt="Coverage" /></a>
<a href="https://discord.gg/G7Qnnhy" target="_blank"><img src="https://img.shields.io/badge/discord-online-brightgreen.svg" alt="Discord"/></a>
<a href="https://opencollective.com/nest#backer" target="_blank"><img src="https://opencollective.com/nest/backers/badge.svg" alt="Backers on Open Collective" /></a>
<a href="https://opencollective.com/nest#sponsor" target="_blank"><img src="https://opencollective.com/nest/sponsors/badge.svg" alt="Sponsors on Open Collective" /></a>
  <a href="https://paypal.me/kamilmysliwiec" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-ff3f59.svg"/></a>
    <a href="https://opencollective.com/nest#sponsor"  target="_blank"><img src="https://img.shields.io/badge/Support%20us-Open%20Collective-41B883.svg" alt="Support us"></a>
  <a href="https://twitter.com/nestframework" target="_blank"><img src="https://img.shields.io/twitter/follow/nestframework.svg?style=social&label=Follow"></a>
</p>
  <!--[![Backers on Open Collective](https://opencollective.com/nest/backers/badge.svg)](https://opencollective.com/nest#backer)
  [![Sponsors on Open Collective](https://opencollective.com/nest/sponsors/badge.svg)](https://opencollective.com/nest#sponsor)-->

## Description

[Nest](https://github.com/nestjs/nest) framework TypeScript starter repository.

## Installation

```bash
$ npm install
```

## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## Stay in touch

- Author - [Kamil Myśliwiec](https://kamilmysliwiec.com)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)

## License

Nest is [MIT licensed](LICENSE).
# ZERO-TO-HERO-NESTJS

## NestJS  Modules 

+ Each application has at least one module - the root module. That is the starting point of the application.
+ Modules are an effective way to organzie components by a closely related set of capabilities (e.g. per feature).
+ It is a good practice to have a folder per module containing the module's components l
+  Modules are **singletons,** therefore a module can be inported by multiple other modules.

## Defining a module

A module is defined by annotating a class with the **@Module** decorator
The decorator provides metadata that Nest uses to organize the application structure.

## @Module Decorator Properties
+ **providers:**  Array of providers to be available within the module via dependency injection
+ **controllers:**  Array of controllers to be instantiated within the module.
+ **exports:**  Array of controllers to export to other modules.
+ **imports:**  List of modules required by this modules. Any exported provider by these modules will now be available in our module via dependency injection.

## Module Definition Example

```bash
@Module({
  providers: [ForumService],
  controllers: [ForumController],
  imports: [
      PostModule,
      CommentModule,
      AuthModule,
   ],
   exports: [ForumService]
 })
 
 export class ForumModule {}
    
```

## NestJS Controllers

+ Responsible for handling incoming **requests** and returning **responses** to the client.
+ Bound to a specific **path** (for example, "/tasks" for the task resource) .
+ Contain **handlers** which handle **endpoints** and **request methods** (GET, POST, DELETE etcetera).
+ can take advantage of **dependency injection** to consume providers within the same module.

## Defining a Controller 

+ Controllers are defined by decorating a class with the **@Controller** decorator.
+ The decorator accepts a string , which is the **path** to be handled by the controller.

```bash
@Controller('/tasks')
export class TasksController {
   //....
}
    
```

## Defining a Handler

Handlers are simply methods within the controller class, decorated with decorators such as **@Get, @Post, @Delete** etcetera.

```bash
@Controller('/tasks')
export class TasksController {
   @Get()
   getAllTasks() {
        # //do stuff
        return ...;
   }
   
   @Post()
   createTask() {
      # // do stuff
      return ...;
   }
}

```

## NestJS Providers

+ Can be injected into constructors if decorated as an **@Injectable** , via **dependency injection** .
+ Can be a plain value , a class, sync/async factory etc.
+ Providers must be provided to a module for them to be usable.
+ Can be exported from a module - and then be available to other modules that import it .


## What is a service ?

+ Defined as providers . **Not All providers are services.**
+ Common concept within software development and are not exclusive NestJS, JavaScript or back-end development .
+ Singleton when wrapped with **@Injectable()** and provided to a module. That means , the same instance will be shared across the application - acting as a single source of truth.
+ The main source of business logic. For example, a service will be called from a controller to validate data, create an item in the database and return a response .

### Providers in Modules

```bash
import {TasksControllers } from './tasks.controller';
import { TasksService } from './tasks.service' ;
import { LoggerService } from '../shared/logger.service' ;

@Module({
  controllers: [
    TasksControllers
  ],
  providers: [
    TasksService,
    LoggerService,
  ]
  
})
export class TaskModules

```

## Dependency Injection in NestJS
+ Any component within the NestJS ecosystem can inject a provider that is decorated with the **@Injectable** .
+ We define the dependencies in the constructor of the class . NestJS will take care of the injection for us, and it will then be available as a class property .

```bash
import { TasksService } from './tasks.service' ;

@Controller('/tasks')
export class TasksController {
  constructor (private tasksService: TasksService) {}
   
   @Get()
  async getAllTasks() {
      return await this.tasksService.getAllTasks();
  }
}

```

## Data Transfer Object (DTO)

+ Common concept in software development that is not specific to NestJS.
+ Result in more bulletproof code, as it can be used as a TypeScript Type .
+ Do not have any behavior except for storage, retrieval, serialization and deserilization of its own data.
+ Result in increased performance (allthough negligible in small applications ).
+ Can be useful for data validation.
+ A DTO is **NOT** a model definition . It defines the shape of data for a specific case , for example - creating a task . 
+ Can be defined using and **interface** or a **class** .


## Classes VS Interfaces for DTOs

+ Data Transfer Objects (DTOs) can be defined as classes or interfaces .
+ The recommended approach is to use **classes**, also clearly documented in the NestJS documentation.
+ The reason in that interfaces are a part of TypeScript and therefore are not preserved post-commilation.
+ NestJS cannot refer to interfaces in run-time, but can refer to classes.
**TLDR: Classes are the way to go for DTOs.**



