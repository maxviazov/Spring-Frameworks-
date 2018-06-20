
_The purpose of this page is to discuss logging practices in the Spring Framework._

# Development Logging

Logging in development needs to be selected and presented with care to maximize value and lower the noise-to-signal ratio. This section aims to define what that means more concretely.

**DEBUG vs TRACE**

DEBUG and TRACE log levels should work _together_ as a two-tier system. That doesn't mean having most messages at DEBUG level and some at TRACE, but rather having a definition of what belongs at each level, and in some cases having intelligently designed messages that show nuanced output for DEBUG vs TRACE.

The purpose of _DEBUG logging_ is to provide feedback on what's happening in a way that is a) minimal, b) presented in a compact way, and c) focused on high value bits of information that are generally useful over and over again, as opposed to being useful for a specific issue, i.e. the 80/20 rule. DEBUG level is the window display of the development experience. It should provide a reasonable, out-of-the-box experience, without the need to tweak settings by package to avoid a fire hose.

_TRACE logging_ follows the same mindset as DEBUG, except for the 80/20 rule. It should still aim to be minimal, compact, and focused on value, but also allow extended information to be logged, including for specific issues. Like DEBUG, TRACE aims to avoid a fire hose but it's expected that log settings by package may need to be customized to obtain the right amount of detail for the problem at hand.

**The Fine-Tuning Process**

Log messages can only be calibrated in the full context of log output for specific scenarios. It's impossible otherwise to spot issues such as duplication (e.g. request path logged in many places), inconsistent level of detail (vs other related components), verbosity, and other unintended consequences. We cannot gauge overall effectiveness in isolation either.

Duplication and verbosity may seem like small issues, surely we can err on the side of extra information. For once they add noise without value, but more importantly consider what is not done. To address those issues, we must consider where certain information is best shown relative to this and other scenarios. We must iterate over wording. We must think about the relative value of information, or what else we could show. 

All of that is extra work of course, but just like we need tests to prove code works, iterating over and reviewing actual logging output is the only way to create good logging and a good development experience.

**Questions To Ask**

**Q:** Is the information relevant when solving a specific issue (TRACE), or is it important enough to see all the time (DEBUG)?

For example, HTTP request mappings (request conditions, handlers, and methods with full signatures) is very useful information, but do you really want to see hundreds or thousands of those, on every startup in development mode? More likely, most of the time, we'll tune that out since it's not relevant, but in the process other important bits will get burried.

Instead we could show summary information by `HandlerMapping`:
```
17:04:11.919 [main] DEBUG RequestMappingHandlerMapping - Detected 84 mappings in 'requestMappingHandlerMapping'
17:04:11.941 [main] DEBUG SimpleUrlHandlerMapping - Patterns [/] in 'viewControllerHandlerMapping'
17:04:11.965 [main] DEBUG SimpleUrlHandlerMapping - Patterns [/resources/**] in 'resourceHandlerMapping'
```

That's minimal, compact, and aids with understanding. It gives assurance about what handler mappings are present, along with a bit of valuable data that can fit in such compact form, and also doesn't forget to add the bean name at the end, which is essential in order to know the function of each `HandlerMapping`. Note that `BeanNameHandlerMapping` was also configured but did not chime in at DEBUG level because it did not find any beans with mappings -- such information is left for TRACE level, if we suspect an issue, or want more information but we don't need to see it every time.

**Q:** What is the most compact way to present the information?

This requires iterating over a log message until it's compact, and verbosity is reduced without loss of meaning. 

For example:
```
Processing GET request for [/spring-mvc-showcase/data/param]
```
Becomes:
```
GET /spring-mvc-showcase/data/param
```
Or perhaps we can add more high value (request parameters at DEBUG, plus also headers at TRACE):
```
GET /spring-mvc-showcase/data/param, parameters={foo:[bar]}
```

**Q:** Is there an opportunity to add more value?

For example:
```
Successfully completed request
```
Becomes:
```
Completed 304 NOT_MODIFIED
```

**Q:** Does a word duplicate what is already known from the category name? If so, consider dropping it.

For example:
```
org.springframework.web.servlet.view.freemarker.FreeMarkerView - Rendering FreeMarker template [foo/bar.ftl]
```
Becomes:
```
org.springframework.web.servlet.view.freemarker.FreeMarkerView - Rendering [foo/bar.ftl]
```

**Q:** What value does a log message provide? Could, and should, it be left out?

For examples `FreeMarkerView` can be ordered ahead of `JstlView`, as it can check if a template is present and hence yield to the next strategy. Seeing the message "No FreeMarker view found for URL ..." seems useful on its own, but when followed by a message from `JstlView` forwarding to a JSP page, it adds unnecessary noise even at TRACE level. The only thing it helps to confirm is that FreeMarker is ordered ahead of JSPs which we don't need to re-confirm on every request. 

**Q:** How much volume does it add vs how much value does it bring?

Clearly if showing all request mappings for annotated methods at DEBUG is too much volume but showing all patterns for `SimpleUrlHandlerMapping` (but not handlers) is both feasible and valuable.

As another example, on a single HTML page there may have 20-30 or more static resources to load. Clearly for fine-grained components such as `CachingResourceResolver` we can't afford to show much, if anything at all, at DEBUG level. Showing cache add/remove operations creates a lot of noise even for TRACE level, with little value. We might however log a small message "Resource served from cache" when a resource is served from cache, which tells us the `ResourceResolver` chain was bypassed. We could show that at TRACE based on expected average volume.

