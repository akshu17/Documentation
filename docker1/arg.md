What is ARG in Docker?
ARG is a Dockerfile instruction used to define build-time variables — values that are available only during the image build process, not inside the running container.

🛠️ Syntax
ARG <variable_name>[=<default_value>]
You can specify a default value, or pass a custom one at build time using --build-arg.

🧪 Example
Dockerfile:

FROM alpine
ARG APP_VERSION=1.0
RUN echo "Building version $APP_VERSION"
Build the image:

docker build -t myapp --build-arg APP_VERSION=2.5 .
Output:

Building version 2.5
If you don't pass --build-arg, the default (1.0) is used.

❗ Key Notes
ARG is only available during build time. It's not accessible inside the running container unless explicitly passed to ENV.
You can use ARG to conditionally install packages, control base images, or set metadata.
✅ Use Case Example
ARG NODE_ENV=production
ENV NODE_ENV=$NODE_ENV
RUN echo "Environment: $NODE_ENV"
Here, the ARG is used to set an ENV variable that persists into the running container.

🧠 Summary
Feature	Description
Scope	Build-time only
Overridable	✅ Yes, with --build-arg during build
Default Value	✅ Optional
Use Case	Controlling build logic, setting ENV vars
