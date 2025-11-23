Upgrade to Java 21 (LTS)
=========================

Background
----------
I attempted to run the automated GitHub Copilot app-modernize Java upgrade tool, but the service is unavailable for this account. Because of that, I added a minimal `pom.xml` that configures the project to build with Java 21 and wrote manual upgrade instructions below.

What I added
------------
- `pom.xml` — Minimal Maven configuration that sets the compiler `release` to `21`.

Recommended steps (Windows / PowerShell)
---------------------------------------
1. Install JDK 21 (Temurin/Eclipse Adoptium recommended):

```powershell
winget install --exact --id EclipseAdoptium.Temurin.21.JDK
# If winget can't find the package, download from: https://adoptium.net/
```

2. (Optional) Set `JAVA_HOME` and update `PATH` for the current user (replace path if different):

```powershell
# Example path — confirm exact install folder under "C:\Program Files\"
setx JAVA_HOME "C:\Program Files\Eclipse Adoptium\jdk-21"
# Restart PowerShell or sign out/in for setx to take effect; for current shell:
$env:JAVA_HOME = "C:\Program Files\Eclipse Adoptium\jdk-21"
$env:Path = "$env:JAVA_HOME\bin;$env:Path"
```

3. Build with Maven (uses the added `pom.xml`):

```powershell
cd "c:\Users\user\Documents\AD_D\Term_03\COMP-3021 Secure Coding and Testing\fernandez_aubrey_assignment_03"
mvn -B -DskipTests package
```

4. Compile/run a single file using JDK 21 directly (no Maven):

```powershell
javac --release 21 VulnerableApp.java
java VulnerableApp
```

Notes and next steps
--------------------
- If your project uses Gradle, set the toolchain or `sourceCompatibility`/`targetCompatibility` to 21 in `build.gradle`.
- The automated GitHub Copilot upgrade tool requires a Pro/Enterprise plan and is not available for this account; if you want, I can:
  - Convert the project fully into a Maven project (add source layout and a simple test harness).
  - Attempt automated code migrations using OpenRewrite locally if you provide permission to run such tools.
  - Run `mvn package` here in the workspace after you confirm installing JDK 21 or want me to run with the system JDK.

If you'd like me to proceed with any of the above, tell me which option to run next.
