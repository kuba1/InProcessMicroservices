# In-process microservice-like architecture

This page describes a way of building console applications or system services that was successfully used in enterprise environment to build a system service.

This architecture was designed with following prerequisites in mind:
1. Needs to be long-term maintainable. Fixing bugs cannot take significantly more time later in the project's life as it does at its beginning.
2. Needs to be long-term extensible. Similarly as for bugs, adding new features should be as easy when the project is mature as it is when the project is started.
3. Needs to maintain long-term quality. Project needs to be easily testable in terms of automated tests. It should be simple to add new tests and when something breaks, only tests related to this functionality should fail.

# A way to solve those challenges

Above challenges can be effectively solved by transplanting ideas from web/SaaS applications, namely microservice architecture into console (service) application.
In particular, we can:
1. Use Dependency Injection - allows for testability in terms of unit tests - classes that depend on interfaces, can have those interfaces replaced with mocked versions of dependendencies for testing.
2. Split the application into well-isolated parts (microservices) - allows for separation of concerns - splitting of business logic into independent parts that can be individually developed and tested with integration tests. This way of organizing the app also makes it much easier to limit impact of changes - changes made to one microservice will never impact any other microservice unless events behavior is somehow affected.
3. Facilitate event bus with POCO events - further promotes separation of concerns - individual microservices only depend on events coming from other microservices. Each microservice can be modified or even completely rewritten and if it still produces and handles events in the same way, the application is going to work as it should. Events offer even stronger separation than interfaces.
4. Use unit, integration and regression/E2E testing.

# Implemenation
1. DI - application hosting support using `Microsoft.Extensions.Hosting.Host`.
2. Microservices - can be done with `Microsoft.Extensions.Hosting.BackgroundService`.
3. Event bus - any simple event bus, preferably an in-memory one, so events don't need to be serializable - you can try out https://github.com/kuba1/EventBus.
4. Automated testing - unit testing and mocking libraries, e.g. Xunit and Moq or any of the alternatives.
