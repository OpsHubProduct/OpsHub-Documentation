## Overview

Sometimes your integration may use custom objects or third-party libraries that are not recognized by <code class="expression">space.vars.OIM</code> by default.
When this happens, the integration can fail with error:

```text
com.thoughtworks.xstream.security.ForbiddenClassException
```

You can configure the `allowed.xstream.classes` property to explicitly authorize trusted classes or packages that are required for your integration to work correctly.

> Only allow classes or packages from trusted sources.

## Availability

This configuration is supported from **<code class="expression">space.vars.OIM</code> version 7.234** onwards.

## When to Use This Property

Configure `allowed.xstream.classes` only when:

- Your integration relies on a third-party library that is not included in <code class="expression">space.vars.OIM</code>'s default allow list.
- An integration job fails with a `com.thoughtworks.xstream.security.ForbiddenClassException` error.
- You have reviewed the blocked class and confirmed it is from a trusted source.


## Applying the Configuration

1. Stop the <code class="expression">space.vars.OIM</code> server.
2. Go to <<code class="expression">space.vars.OIM</code> Installation Path\>/AppData/OpsHubData 
3. Open the `OIM_Config.properties` file.
4. Add or update the `allowed.xstream.classes` property with the required values. (Check the [Sample Scenario](#sample-scenario) section to know more.)
5. Save the file.
6. Restart the <code class="expression">space.vars.OIM</code> server.


## Sample Scenario

A custom connector uses objects from the Apache Commons library. During synchronization, <code class="expression">space.vars.OIM</code> blocks the object because it is not part of the default trusted list.
By adding the required class or package to the allowed.xstream.classes property, <code class="expression">space.vars.OIM</code> can process the data successfully and the integration continues without errors.

Below are the samples of how the `allowed.xstream.classes` property value can be set:

### Allow Specific Classes

```properties
allowed.xstream.classes=org.apache.commons.collections.BidiMap,org.apache.commons.collections.bidimap.DualHashBidiMap
```

### Allow an Entire Package Hierarchy

```properties
allowed.xstream.classes=org.apache.commons.**
```

### Allow Multiple Classes and Packages

```properties
allowed.xstream.classes=com.example.CustomObject,com.example.model.**,org.apache.commons.collections.BidiMap
```