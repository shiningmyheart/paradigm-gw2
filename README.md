Function computing is an event driven service. Function execution can be event-driven, that is, when an event occurs, the event triggers the execution of the function. Now, function computing supports API gateway as an event source. When the request setup function calculates the API for the back-end service, the API gateway triggers the corresponding function, which returns the execution result to the API gateway.

API gateway connects to the Function Computing Engine, you can safely open your functions in the form of API, and realize the functins of authentication, flow control, data conversion and other issues.
