# In-process microservice-like architecture

This page describes a way of building console applications or system services that was successfully used in enterprise environment to build a system service.

This architecture was created with following prerequisites in mind:
1. Needs to be long-term maintainable. Fixing bugs cannot take significantly more time later in the project's life as it does at its beggining.
2. Needs to be long-term extensible. Similarly as for bugs, adding new features should be as easy when the project is mature as it is when the project is started.
3. Needs to maintain long-term quality. Project needs to be easily testable in terms of automated tests. It should be simple to add new tests and when something breaks, only tests related to this functionality should fail.
