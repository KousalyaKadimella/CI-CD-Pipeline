# CI/CD with Maven and GitHub Actions (Course Project)

A course project for **Advanced Software Engineering** (M.S. Computer Science, California State University, Dominguez Hills, spring 2024). It shows how a Java project is built, style-checked and tested automatically with **Maven** and **GitHub Actions**.

> **Where the code is:** the Java project and workflow live in [KousalyaK03/Maven](https://github.com/KousalyaK03/Maven).
> This repository holds the written assignment (`MavenAssignment.docx`) explaining the Maven build lifecycle.

---

## What the project does

Every push or pull request to `main` triggers a GitHub Actions workflow that:

1. Checks out the code on an Ubuntu runner
2. Installs **JDK 11** (AdoptOpenJDK)
3. Runs `mvn -B package` to compile the code and build a `.jar`
4. Runs `mvn -B test` to run the JUnit tests

If any step fails, the run is marked as failed on GitHub, so problems show up on every change instead of later.

## Tech used

| Tool | What it's used for |
|---|---|
| Java | A simple sample application (`App.java`) |
| Maven (`pom.xml`) | Build, dependencies and the build lifecycle |
| JUnit 3.8.1 | Unit test (`AppTest.java`) |
| Maven Checkstyle plugin | Code-style checks, bound to the `verify` phase (run locally; the CI workflow runs `package` and `test`) |
| GitHub Actions (`.github/workflows/main.yml`) | Runs the build and tests automatically on every push and PR |
| Apache Commons Lang 3.12.0 | Example dependency managed by Maven |

## Repository contents

```text
KousalyaK03/Maven                     (code)
├── .github/workflows/main.yml        # GitHub Actions: build + test on push / PR to main
├── pom.xml                           # Maven config, Checkstyle plugin, java11 profile
├── checkstyle.xml                    # Checkstyle rules
└── src/
    ├── main/java/com/example/App.java
    └── test/java/com/example/AppTest.java

KousalyaKadimella/CI-CD-Pipeline      (this repo)
└── MavenAssignment.docx              # Write-up: Maven default, clean and site lifecycles
```

## Maven lifecycle (summary of the write-up)

- **Default lifecycle:** `validate → compile → test → package → verify → install → deploy`. Running a phase runs every phase before it, so `mvn package` also compiles and tests.
- **Clean lifecycle:** `pre-clean → clean → post-clean` removes files from earlier builds.
- **Site lifecycle:** generates project documentation.

## Run it locally

```bash
git clone https://github.com/KousalyaK03/Maven.git
cd Maven
mvn package    # compile, test and build the jar
mvn verify     # also runs Checkstyle (see note below)
```

Requires Java and Maven installed locally.

> **Note:** in `pom.xml`, the Checkstyle `configLocation` points to a path on my own laptop. To run `mvn verify` on another machine, change it to `checkstyle.xml`.

## Notes and limitations

- The application is a small "Hello World" sample. The focus of the assignment is the **build and automation**, not the app.
- The code compiles to Java 1.8. The workflow runs on JDK 11, and the `pom.xml` includes a `java11` profile.
- There is no deployment step (no Jenkins, SonarQube or cloud deployment). Natural next steps would be a test-coverage report and deploying the built `.jar`.

## What I learned

How Maven's lifecycle phases chain together, how plugins like Checkstyle attach to a phase, and how a CI workflow gives fast, automatic feedback on every change.

---

**Kousalya Kadimella** · M.S. Computer Science, CSU Dominguez Hills
