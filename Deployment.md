# Introduction #
Using this library with guice isn't THAT simple due to the current stock implementation of the guice library (specifically it only being available in two flavours AOP, NO-AOP.

# Details #
Based on the conversation here some work needs to be done to use this:
[Issue 712](http://code.google.com/p/google-guice/issues/detail?id=712&colspec=ID%20Type%20Status%20Priority%20Milestone%20Owner%20Summary%20Component&start=100)

I would recommend the following:
  * the guice library come stock with all the AOP interfaces, but no implementation
  * three libraries should be created:
    1. Normal AOP: This is the normal AOP implementation in guice
    1. Dex AOP: This is the library that I am vending here
    1. Throwing AOP: This would be for people who don't want AOP. It would throw an UnsupportedOperationException if you try to bind method interceptors
  * Before creating your injector for the first time, you can call into the static AOPFactory.setFactory method to  set the factory that would be used to create your proxy classes.  This would be equivalent to the compiled statement [in guice](http://code.google.com/p/google-guice/source/browse/core/src/com/google/inject/internal/ConstructorInjectorStore.java#84)