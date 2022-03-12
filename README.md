 # SPDX Catalog

Bundles the latest version of the [SPDX Licence List](https://spdx.org/licenses/) in a JSON format
as provided [here](https://github.com/spdx/license-list-data/tree/master/json).

Additionaly, it comes with a small [Kotlin](https://kotlinlang.org/) library powered by Jackson ObjectMapper
which provides a convenient and typed access to that catalog.

So for example, for the `Apache-2.0` license you have access to the following data:

```
SpdxLicense(
    reference=https://spdx.org/licenses/Apache-2.0.html, 
    isDeprecatedLicenseId=false, 
    detailsUrl=https://spdx.org/licenses/Apache-2.0.json, 
    referenceNumber=382, 
    name=Apache License 2.0, 
    licenseId=Apache-2.0, 
    seeAlso=[https://www.apache.org/licenses/LICENSE-2.0, https://opensource.org/licenses/Apache-2.0], 
    isOsiApproved=true, 
    isFsfLibre=true
)
```

## How to install

This library is being pushed to Maven Central, so you can grab it i.e. with Gradle:

````groovy
repositories {
    mavenCentral()
}

dependencies {
    implementation('io.cloudflight.license.spdx:spdx-catalog:3.16')
}
````

## How to use

Your entry class is the singleton `io.cloudflight.license.spdx.SpdxLicenses`.

For example:

````kotlin
import io.cloudflight.license.spdx.SpdxLicenses

println(SpdxLicenses.getById("0BSD"))

val license = SpdxLicenses.getByDescription("The Apache Software License, Version 2.0")
println(license?.licenseId)
````

will print `BSD Zero Clause License` 

and

````kotlin
import io.cloudflight.license.spdx.SpdxLicenses

val license = SpdxLicenses.getByDescription("The Apache Software License, Version 2.0")
println(license?.licenseId)
````

will print `Apache-2.0`.

The library also normalizes different variants of license description names, therefore also the following code works:

````kotlin
import io.cloudflight.license.spdx.SpdxLicenses

val license = SpdxLicenses.getByDescription("Apache License v2.0")
println(license?.licenseId)
````

This will print `Apache-2.0` as well.

## How to contribute

Always keep the version of that [SPDX list](https://github.com/spdx/license-list-data/tree/master/json) in sync with the version of this module.
