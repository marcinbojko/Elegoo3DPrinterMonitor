FROM sickcodes/docker-osx:latest

# Install Node.js 20
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs

# Create a non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install global Node.js packages
RUN npm install -g npm@latest yarn

# Set up development environment
RUN apt-get update && apt-get install -y \
    git \
    curl \
    wget \
    unzip \
    && apt-get clean

# Switch to non-root user
USER $USERNAME

# Set up Node.js environment
ENV NODE_ENV=development
WORKDIR /workspace

# Add node_modules/.bin to PATH
ENV PATH=/workspace/node_modules/.bin:$PATH
