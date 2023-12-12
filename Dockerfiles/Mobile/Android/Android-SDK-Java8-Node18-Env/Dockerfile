# Use a base image with OpenJDK 8
FROM openjdk:8

# Set environment variables for Android SDK
ENV ANDROID_HOME /usr/local/android-sdk
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

# Update, install necessary tools, and clean up in one layer
RUN apt-get update && apt-get install -y \
    git \
    curl \
    unzip \
    && curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

# Install Android SDK and tools, then clean up downloaded files in one layer
RUN mkdir -p $ANDROID_HOME && cd $ANDROID_HOME \
    && curl -o sdk.zip 'https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip' \
    && unzip sdk.zip \
    && rm sdk.zip \
    && yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses \
    && $ANDROID_HOME/tools/bin/sdkmanager "platform-tools" "platforms;android-28" "build-tools;28.0.3"

# Check Node.js and npm versions
RUN node -v \
    && npm -v

# Set up ADB server
EXPOSE 5037

