### Why?
    * The cost of a feature is the cost of the essential complication plus the cost of the
    accidental complication
        `cost = f(g(e), h(a)) = g(e) + h(a)`
    * If a cost from accidental complication dominates the cost of the feature, then you arrive
    at the fundamental theorem of agile software dvevelopment
        `h(a) >> g(e) `
    * The fundamental theorem of agile software dvevelopment says:
        - If you want to estimate little things, you have to refactor.
        - Because refactoring is how you reduce accidental complication, and only
        by driving accidental complication down as far as you possibly can will your
        relative estimates have any meaning.


### Cycle
    - Think about what you want to do 
    - Write a failing test;
	- Observe the failing test;
	- Write the minimum amount of code to make the test pass, NOT the code you want you have to write;
	- Observe the passing test;
	- Refactor code;

### Testing options
    * Manual testing: checking code through an user's perspective.
    * Automated testing: writing code to verify code. Several things can be tested, faster than manual tests.
	    - Unit tests
            - Level of software testing where individual units / components of a software are tested.
            - The purpose is to validate that each smallest testable part  of the software performs
            as designed.
	    - E2E
            - Technique that tests the entire software product from beginning to end to ensure
            the application flow behaves as expected.
            -  It defines the product’s system dependencies and ensures all integrated
            pieces work together as expected.
