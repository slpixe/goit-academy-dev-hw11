# Cattivity Time Servlet Project

Welcome to **Cattivity Time**! This Java servlet-based web app is
purrfect for anyone who wants to know the time—and see what our 
feline friends might be up to based on the time of day. 
Pick your time zone, and get a glimpse of the time with a related cat
image and activity message. It even remembers your last selected 
time zone with cookies, so it’s like your own personal time-keeping cat friend!

## Table of Contents
1. **[Tools and Technologies](#tools-and-technologies)**
2. **[Setup and Deployment Instructions](#setup-and-deployment-instructions)**
   - **[Prerequisites](#prerequisites)**
   - **[Setup Instructions](#setup-instructions)**
   - **[Deploying the WAR file](#deploying-the-war-file)**
   - **[Optional: Run with Docker](#optional-run-with-docker-remote)**
3. **[Functionality](#functionality)**
4. **[Project Structure](#project-structure)**
5. **[Usage Instructions](#usage-instructions)**
   - **[Using the Application](#using-the-application)**
   - **[Example URLs](#example-urls)**


## Tools and Technologies

We’ve got some cool tech in our cat basket:

- **Java 21**: The core programming language used for the project.
- **Jakarta Servlet API**: For handling HTTP requests and responses.
- **Tomcat 10**: A servlet container to deploy and run the web application.
- **Thymeleaf**: For rendering dynamic HTML content, like a cozy cat box.
- **SLF4J and Logback**: For keeping track of all cattivities.
- **JUnit 5**: For making sure everything’s working purrfectly.
- **Mockito**: For mocking objects during testing.
- **JUnit & Mockito**: For writing and executing unit tests.
- **Gradle**: Used for dependency management and building the project as a WAR (Web Application Archive) file.
- **Docker**: To build the application container for easy deployment.
- **GitHub Actions**: Used for CI/CD, automating the build, test, and deployment.

## Setup and Deployment Instructions

### Prerequisites

- **Java 21** installed on your machine.
- **Gradle** installed or use the provided Gradle wrapper (`gradlew`).
- A **Java servlet container** like Apache Tomcat 10.

### Setup Instructions

1. **Clone the repository**:
```shell
git clone git@github.com:ruslanaprus/goit-academy-dev-hw11.git
cd goit-academy-dev-hw11
```

2. **Build the project using Gradle**:

```shell
./gradlew build
```
### Deploying the WAR file

1. The built `.war` file will be located in the `build/libs` directory.
2. Deploy the `.war` file to your servlet container (e.g., place it to the `webapps` directory of your Tomcat server).
3. **Start the server**:
   - Start your servlet container (e.g., `catalina.sh run` for Tomcat).
   - Visit `http://localhost:8080` to access the application.

### Optional: Run Using Docker

Alternatively, you can deploy the application using Docker with the official Tomcat 10 image from Docker Hub. You can modify the Dockerfile to use the latest image version if necessary.

1. To do it locally, build the Docker image:

```shell
docker build -t tomcat-time-servlet:1.0 .
```

To run the container:
```shell
docker run -d -p 8080:8080 --name time-cattivity tomcat-time-servlet:1.0
```

2. **Run with Docker remotely**

```bash
docker run -d -p 8080:8080 --name time-cattivity ghcr.io/ruslanaprus/goit-academy-dev-hw11/time-servlet
```

## Functionality

The application provides the following functionalities:

1. **Display Current Time**: Shows you the time in the time zone you choose. If you don’t specify one, it defaults to UTC—like a cat that always knows where the sun is.
2. **Time Zone Validation**: Checks if the time zone is valid using `TimezoneValidateFilter`. If it’s not, it’ll use a cookie-stored time zone if it finds one.
3. **Display Cat Activities**: Shows different cat images and activities based on the time of day—like naps, playtime, or midnight zoomies.
4. **Cookie Storage**: Remembers your chosen time zone in a cookie for the next time you visit.
5. **Error Handling**: Shows an intimidating, but cute error message if the time zone isn’t quite right.
6. **Formatted Time**: Displays the time in `yyyy-MM-dd HH:mm:ss` format, including the UTC offset.

## Project Structure

The project is organized into the following packages and components:

```shell
├── 󱧼 src
│   ├──  main
│   │   ├──  java
│   │   │   └──  org
│   │   │       └──  example
│   │   │           ├──  controller
│   │   │           │   ├──  TimeServlet.java
│   │   │           │   └──  TimezoneValidateFilter.java
│   │   │           ├──  listener
│   │   │           │   └──  TemplateEngineInitializer.java
│   │   │           ├──  service
│   │   │           │   ├──  TimeResponseBuilder.java
│   │   │           │   ├──  TimezoneCookieService.java
│   │   │           │   └──  TimezoneService.java
│   │   │           └──  util
│   │   │               └──  ThymeleafRenderer.java
│   │   ├──  resources
│   │   └──  webapp
│   │       ├──  fonts
│   │       ├──  images
│   │       ├──  index.html
│   │       └──  WEB-INF
│   │           ├──  templates
│   │           │   ├──  error.html
│   │           │   └──  time.html
│   │           └──  web.xml
│   └──  test
├──  build.gradle
├──  gradle
├──  gradlew
├──  gradlew.bat
└──  settings.gradle
```

## Usage Instructions

### Using the Application

**See What Cats Are Up To Now:**

1. Visit the main page http://localhost:8080/ to see a friendly greeting and a button to check the cat activities at the current time.
2. Click the `Show Cattivity` button to go the time page: http://localhost:8080/time
3. Enter your time zone in the text field and click button `Get Time`. Optionally, you can specify a time zone in the query parameter: http://localhost:8080/time?timezone=Europe/London
4. This will display the current time and a cat picture that matches the time of day.

The application stores your last selected time zone in a cookie. On the next visit, it will automatically display the time for the previously selected time zone, if you won't specify the new one.

**Handling Invalid Timezones**:

If you type in a time zone that doesn’t exist, you’ll see a friendly error page with a message that explains the issue (400 status code).

### Example URLs

To view the current time in UTC:
http://localhost:8080/time?timezone=UTC

To view the time in a specific offset:
http://localhost:8080/time?timezone=UTC+3

Invalid timezone example:
http://localhost:8080/time?timezone=InvalidZone]