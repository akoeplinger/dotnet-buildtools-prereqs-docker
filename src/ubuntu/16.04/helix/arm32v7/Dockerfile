FROM arm32v7/ubuntu:16.04

# Install Helix Dependencies 

# Can remove the mono preview repo when we no longer depend on pre-release libgdiplus

RUN apt-get update && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    apt-get install -y apt-transport-https ca-certificates && \
    echo "deb https://download.mono-project.com/repo/ubuntu preview-xenial main" | tee /etc/apt/sources.list.d/mono-official-preview.list  && \
    apt-get update && \
    apt-get install -y \
        gss-ntlmssp \
        iputils-ping \
        libcurl3 \
        libffi-dev \
        libgdiplus \
        libicu-dev \
        libssl-dev \
        libunwind8 \
        libunwind-dev \
        lldb-3.9 \
        locales \
        locales-all \
        python3-dev \ 
        python3-pip \
        sudo \
        tzdata \
        unzip \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LANG en_US.utf8

RUN ln -sf /usr/bin/python3 /usr/bin/python && \
    python -m pip install --upgrade pip==19.3.1 && \
    python -m pip install virtualenv==16.6.0 && \
    python -m pip install helix-scripts --extra-index-url https://dnceng.pkgs.visualstudio.com/public/_packaging/helix-client-prod/pypi/simple

RUN adduser --disabled-password --gecos '' --uid 1001 --shell /bin/bash --ingroup adm helixbot && \
    chmod -R +x /root && \
    echo 'helixbot ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER helixbot

RUN python -m virtualenv --no-site-packages /home/helixbot/.vsts-env


