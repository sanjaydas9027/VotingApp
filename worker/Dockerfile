# Use the SDK image to build
FROM mcr.microsoft.com/dotnet/sdk:7.0 as build

# Set the target and build platforms as arguments
ARG TARGETPLATFORM
ARG BUILDPLATFORM

# Print platform information
RUN echo "I am running on $BUILDPLATFORM, building for $TARGETPLATFORM"

# Set the working directory
WORKDIR /source

# Copy the project files
COPY *.csproj .

# Determine the architecture based on the target platform
RUN case ${TARGETPLATFORM} in \
         "linux/amd64")  ARCH=x64  ;; \
         "linux/arm64")  ARCH=arm64  ;; \
         "linux/arm64/v8")  ARCH=arm64  ;; \
         "linux/arm/v7") ARCH=arm  ;; \
    esac \
    && dotnet restore -r linux-${ARCH}

# Copy the rest of the source code
COPY . .

# Publish the application
RUN case ${TARGETPLATFORM} in \
         "linux/amd64")  ARCH=x64  ;; \
         "linux/arm64")  ARCH=arm64  ;; \
         "linux/arm64/v8")  ARCH=arm64  ;; \
         "linux/arm/v7") ARCH=arm  ;; \
    esac \
    && dotnet publish -c release -o /app -r linux-${ARCH} --self-contained false --no-restore

# Create the final runtime image
FROM mcr.microsoft.com/dotnet/runtime:7.0

# Set the working directory in the runtime image
WORKDIR /app

# Copy the published files from the build image
COPY --from=build /app .

# Set the entry point for the container
ENTRYPOINT ["dotnet", "Worker.dll"]
