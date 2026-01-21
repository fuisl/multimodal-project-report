FROM registry.gitlab.com/islandoftex/images/texlive:latest

# Install additional tools for development
RUN apt-get update && apt-get install -y \
    make \
    perl \
    latexmk \
    git \
    aspell \
    aspell-en \
    ghostscript \
    curl \
    wget \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /workdir

# Enable latexmk by renaming the configuration file
RUN if [ -f _latexmkrc ]; then mv _latexmkrc .latexmkrc; fi

CMD ["/bin/bash"]
