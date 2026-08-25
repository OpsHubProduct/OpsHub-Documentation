## Overview

<code class="expression">space.vars.OIM</code> uses XStream for XML serialization and deserialization in certain product workflows. To maintain a secure execution environment, <code class="expression">space.vars.OIM</code> internally maintains a default allow list of classes that covers standard product functionality and supported integration scenarios.

In most deployments, no additional configuration is required.

However, in certain custom implementations or integrations involving third-party libraries, XStream may encounter a class that is not present in the default allow list. In such cases, the operation may fail with an error similar to:

```text
com.thoughtworks.xstream.security.ForbiddenClassException
```

If the blocked class is trusted and required for your use case, you can configure the `allowed.xstream.classes` property to explicitly allow the class or package for XStream serialization and deserialization.

> Only allow classes or packages from trusted sources.

## Availability

This configuration is supported from **<code class="expression">space.vars.OIM</code> version 7.234** onwards.

## When to Use This Property

Configure `allowed.xstream.classes` only when:

- An operation fails with a `com.thoughtworks.xstream.security.ForbiddenClassException`.
- The exception indicates a trusted class that is required for your integration or customization.

## Configuration

Add the following property to the `OIM_Config.properties` file:

```properties
allowed.xstream.classes=
```

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

## Applying the Configuration

1. Stop the <code class="expression">space.vars.OIM</code> server.
2. Go to <<code class="expression">space.vars.OIM</code> Installation Path\>/AppData/OpsHubData 
3. Open the `OIM_Config.properties` file.
4. Add or update the `allowed.xstream.classes` property with the required values.
5. Save the file.
6. Restart the <code class="expression">space.vars.OIM</code> server.