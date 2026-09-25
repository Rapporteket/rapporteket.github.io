FROM linuxserver/code-server:latest

# Install Ruby and compilation dependencies for Jekyll gems
RUN apt-get update && apt-get install -y \
    ruby-full \
    build-essential \
    zlib1g-dev \
    git \
    && rm -rf /var/lib/apt/lists/*

# Configure Ruby Gems to install to the user directory to avoid permission issues
ENV GEM_HOME="$HOME/.gems"
ENV PATH="$HOME/.gems/bin:$PATH"

# Update system gems and install Bundler/Jekyll
RUN gem install bundler jekyll

EXPOSE 8443 4000
